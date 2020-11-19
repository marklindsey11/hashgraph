# Transfer tokens

Transfer tokens from some accounts to other accounts. The transaction must be signed by the sending account. Each negative amount is withdrawn from the corresponding account \(a **sender**\), and each positive one is added to the corresponding account \(a **receiver**\). All amounts must have sum of zero. Each amount is a number with the lowest denomination possible for a token. Example: Token X has 2 decimals. Account A transfers amountof 100 tokens by providing 10000 as amount in the TransferList. If Account A wants to send 100.55 tokens, he must provide 10055 as amount. If any sender account fails to have sufficient token balance, then the entire transaction fails and none of the transfers occur, though transaction fee is still charged.

{% hint style="info" %}
The account must be associated to the token prior to transfering tokens to that account. See TokenAssociateTransaction.
{% endhint %}

| Constructor | Description |
| :--- | :--- |
| `new TokenTransferTransaction()` | Initializes a TokenTransferTransaction object |

```java
new TokenTransferTransaction()
```

### Methods

| Method | Type | Description |
| :--- | :--- | :--- |
| `addSender(<tokenId, accountId, amount>)` | [TokenId](token-id.md), [AccountId](../specialized-types.md#accountid), long | Negative token amount is withdrawn from this account |
| `addRecipient(<tokenId, accountId, amount>)` | [TokenId](token-id.md), [AccountId](../specialized-types.md#accountid), long | Postive token amount is added to this account |
| `addTransfer(<tokenId, accountId, amount>)` | [TokenId](token-id.md), [AccountId](../specialized-types.md#accountid), long | Transfer tokens between accounts |

{% tabs %}
{% tab title="Java" %}
```java
//Transfer 100 tokens between two accounts
TokenTransferTransaction transaction = new TokenTransferTransaction()
    .addSender(newTokenId,newAccountId,100)
    .addRecipient(newTokenId, OPERATOR_ID,100);

//Build the unsigned transaction, sign with the sender account private key, submit the transaction to a Hedera network
TransacionId transactionId = transaction.build(client).sign(senderKey).execute(client);
    
//Request the receipt of the transaction
TransactionReceipt getReceipt = transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
Status transactionStatus = getReceipt.status;

System.out.println("The transaction consensus status " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Transfer 100 tokens between two accounts
const transaction = new TokenTransferTransaction()
    .addSender(newTokenId,newAccountId,100)
    .addRecipient(newTokenId, OPERATOR_ID,100);

//Build the unsigned transaction, sign with sender account private key, submit the transaction to a Hedera network
const transactionId = await transaction.build(client).sign(senderKey).execute(client);
    
//Request the receipt of the transaction
const getReceipt = await transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
const transactionStatus = getReceipt.status;

console.log("The transaction consensus status " +transactionStatus);
//Version 1.4.2
```
{% endtab %}
{% endtabs %}





