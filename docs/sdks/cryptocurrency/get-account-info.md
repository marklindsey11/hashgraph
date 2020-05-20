# Get account info

`AccountInfoQuery()` returns all of the information about an account. This **does not** include the list of records associated with the account.

This information includes:

* Account ID
* Key\(s\)
* Balance
* Expiration time
* AutoRenewPeriod
* Whether the account is deleted or not
* Whether the receiver signature is required or not
* The proxy account ID, if any

| Constructor | Description |
| :--- | :--- |
| `AccountInfoQuery()` | Initializes the AccountInfoQuery object |

```java
new AccountInfoQuery()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setAccountId(<accountId>)` | AccountId | The accountId of the account to return the information for |

## Example

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
    .setKey(newPublicKey)
    .setInitialBalance(Hbar.fromTinybar(1000))
    .execute(client);

// This will wait for the receipt to become available
TransactionReceipt receipt = txId.getReceipt(client);

AccountId newAccountId = receipt.getAccountId();

System.out.println("account = " + newAccountId);

AccountInfo accountInfo = new AccountInfoQuery()
    .setAccountId(newAccountId)
    .execute(client);

System.out.println("The public key returned by requesting the account info is: " +accountInfo.key);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { Client, AccountInfoQuery } = require("@hashgraph/sdk");
require("dotenv").config();

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

    const info = await new AccountInfoQuery()
        .setAccountId(operatorAccount)
        .execute(client);

    console.log(`${operatorAccount} info = ${JSON.stringify(info, null, 4)}`);
}

main();
```
{% endtab %}
{% endtabs %}

