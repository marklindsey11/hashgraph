# Transfer cryptocurrency

`CryptoTransferTransaction()` transfers tinybars from one Hedera account to different Hedera account in the Hedera network. The amount is in **tinybars** \(not hbars\). The transaction must be signed by all the keys from all sender accounts. If the sender fails to have insufficient funds in their account to process the transaction, the transaction fails and the tinybars will not be transferred to the receiving account. The service fee will still be charged in the case of insufficient funds.

{% hint style="info" %}
There are `100_000_000` tinybars in one hbar. 
{% endhint %}

| Constructor | Description |
| :--- | :--- |
| `CryptoTransferTransaction()` | Initializes the CryptoTransferTransaction object |

```java
new CryptoTransferTransaction()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `addSender(<accountId>, <amount>)` | AccountId, long | The sender is the account ID of the account and the amount \(value\) of tinybars that will be withdrawn from that account. The amount being withdrawn from the sender has to equal the amount that will be deposited into the recipient account. This method can be called multple times. |
| `addRecipient(<accountId>, <amount>)` | AccountId, long | The recipient is account ID of the account the tinybars will be deposited into and the amount \(value\). The amount being withdrawn from the sender account has to equal the amount that will be deposited into the recipient account. |
| `addTransfer(accountId, value)` | AccountId, long | Transfer to an account with the provided value |

### Example

{% tabs %}
{% tab title="Java" %}
```java
TransactionId transactionId = new CryptoTransferTransaction()
    // .addSender and .addRecipient can be called as many times as you want as long as the total sum from
    // both sides is equivalent
    .addSender(OPERATOR_ID, amount)
    .addRecipient(recipientId, amount)
    .setTransactionMemo("transfer test")
    .execute(client);

System.out.println("transaction ID: " + transactionId);

TransactionRecord record = transactionId.getRecord(client);

System.out.println("transferred " + amount + "...");

Hbar senderBalanceAfter = new AccountBalanceQuery()
    .setAccountId(OPERATOR_ID)
    .execute(client);

Hbar receiptBalanceAfter = new AccountBalanceQuery()
    .setAccountId(recipientId)
    .execute(client);

System.out.println("" + OPERATOR_ID + " balance = " + senderBalanceAfter);
System.out.println("" + recipientId + " balance = " + receiptBalanceAfter);
System.out.println("Transfer memo: " + record.transactionMemo);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { Client, CryptoTransferTransaction } = require("@hashgraph/sdk");

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

    const receipt = await (await new CryptoTransferTransaction()
        .addSender(operatorAccount, 1)
        .addRecipient("0.0.3", 1)
        .setTransactionMemo("sdk example")
        .execute(client))
        .getReceipt(client);

    console.log(receipt);
}

main();
```
{% endtab %}
{% endtabs %}



