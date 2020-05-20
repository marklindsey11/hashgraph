# Delete an account

`AccountDeleteTransaction()` deletes an existing account from the Hedera network. Before deleting an account, the existing hbars must be transferred to another account. If you fail to transfer the hbars, you will receive an error message "setTransferAccountId\(\) required." Transfers cannot be made into a deleted account. A record of the deleted account will remain in the ledger until it expires.The expiration of a deleted account can be extended. 

{% hint style="info" %}
Note: Deleting an account requires you to call the `setTransactionId()` and use the accountId of the account that is going to be deleted. Please see example below. 
{% endhint %}

| Constructor | Description |
| :--- | :--- |
| `AccountDeleteTransaction()` | Initializes the AccountDeleteTransaction object |

```java
new AccountDeleteTransaction()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setTransferAccountId(<accountId>)` | AccountId | The ID of the account the tinybars will be transferred to from the account that will be deleted |
| `setDeleteAccountId(<accountId>)` | AccountId | The ID of the account to be deleted from the Hedera network |

##  Example

{% tabs %}
{% tab title="Java" %}
```java
// Generate a Ed25519 private, public key pair
Ed25519PrivateKey newKey = Ed25519PrivateKey.generate();
Ed25519PublicKey newPublicKey = newKey.publicKey;

System.out.println("private key = " + newKey);
System.out.println("public key = " + newPublicKey);

// `Client.forMainnet()` is provided for connecting to Hedera mainnet
Client client = Client.forTestnet();

// Defaults the operator account ID and key such that all generated transactions will be paid for
// by this account and be signed by this key
client.setOperator(OPERATOR_ID, OPERATOR_KEY);

TransactionId txId = new AccountCreateTransaction()
    // The only _required_ property here is `key`
    .setKey(newKey.publicKey)
    .setInitialBalance(new Hbar(2))
    .execute(client);

// This will wait for the receipt to become available
TransactionReceipt receipt = txId.getReceipt(client);

AccountId newAccountId = receipt.getAccountId();

System.out.println("account = " + newAccountId);

new AccountDeleteTransaction()
    // note the transaction ID has to use the ID of the account being deleted
    .setTransactionId(new TransactionId(newAccountId))
    .setDeleteAccountId(newAccountId)
    .setTransferAccountId(OPERATOR_ID)
    .build(client)
    .sign(newKey)
    .execute(client)
    .getReceipt(client);

final AccountInfo accountInfo = new AccountInfoQuery()
    .setAccountId(newAccountId)
    .setQueryPayment(25)
    .execute(client);

// note the above accountInfo will fail with ACCOUNT_DELETED due to a known issue on Hedera

System.out.println("account info: " + accountInfo);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { Client, Ed25519PrivateKey, AccountCreateTransaction, AccountDeleteTransaction, Hbar, TransactionId } = require("@hashgraph/sdk");

async function main() {
    const operatorPrivateKey = process.env.OPERATOR_KEY;
    const operatorAccount = process.env.OPERATOR_ID;

    if (operatorPrivateKey == null || operatorAccount == null) {
        throw new Error("environment variables OPERATOR_KEY and OPERATOR_ID must be present");
    }

    const client = new Client({
        network: { "0.testnet.hedera.com:50211": "0.0.3" },
        operator: {
            account: operatorAccount,
            privateKey: operatorPrivateKey
        }
    });

    const privateKey = await Ed25519PrivateKey.generate();

    console.log("Creating an account to delete");
    console.log(`private = ${privateKey.toString()}`);
    console.log(`public = ${privateKey.publicKey.toString()}`);

    let transactionId = await new AccountCreateTransaction()
        .setKey(privateKey.publicKey)
        .setInitialBalance(new Hbar(2))
        .execute(client);

    let transactionReceipt = await transactionId.getReceipt(client);
    const newAccountId = transactionReceipt.getAccountId();

    console.log(`account = ${newAccountId}`);
    console.log("Deleting created account");

    // To delete an account you **MUST** do the following:
    transactionId = await new AccountDeleteTransaction()
        // Set which account to delete.
        .setDeleteAccountId(newAccountId)
        // Set which account to transfer the remaining balance to.
        .setTransferAccountId("0.0.3")
        // Manually set a `TransactionId` constructed from the `AccountId` you are  deleting.
        .setTransactionId(new TransactionId(newAccountId))
        .build(client)
        // Sign the transaction with the same key as on the acount being deleted.
        .sign(privateKey)
        // Finally, execute the transaction with `Transaction.execute()`
        .execute(client);

    transactionReceipt = await transactionId.getReceipt(client);

    console.log(`status: ${transactionReceipt.status}`);
}

main();
```
{% endtab %}
{% endtabs %}



