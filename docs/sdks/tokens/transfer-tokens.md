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
| `addSender(<tokenId, accountId, amount>)` | TokenId, AccountId, long | Negative token amount is withdrawn from this account |
| `addRecipient(<tokenId, accountId, amount>)` | TokenId, AccountId, long | Postive token amount is added to this account |
| `addTransfer(<tokenId, accountId, amount>)` | TokenId, AccountId, long | Transfer tokens between accounts |

{% tabs %}
{% tab title="Java" %}
```java
//Transfer 100 tokens between two accounts
TokenTransferTransaction transaction = new TokenTransferTransaction()
    .addSender(newTokenId,newAccountId,100)
    .addRecipient(newTokenId, OPERATOR_ID,100);

Status transactionStatus = transaction.build(client) //Build the unsigned transaction
    .sign(senderKey) // Sign with the sending account private key
    .execute(client)//Submit the transaction to the Hedera network
    .getReceipt(client) //Request the receipt of the transaction
    .status; //Obtain the transaction consensus status

System.out.println("The transaction consensus status " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Transfer 100 tokens between two accounts
const transaction = await new TokenTransferTransaction()
    .addSender(newTokenId,newAccountId,100)
    .addRecipient(newTokenId, OPERATOR_ID,100);

const transactionStatus = await (await (await transaction.build(client) //Build the unsigned transaction
    .sign(senderKey) // Sign with the sending account private key
    .execute(client))//Submit the transaction to the Hedera network
    .getReceipt(client)) //Request the receipt of the transaction 
    .status; //Obtain the transaction consensus status

console.log("The transaction consensus status " +transactionStatus);
//Version 1.4.1
```
{% endtab %}
{% endtabs %}





