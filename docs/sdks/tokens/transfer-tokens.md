# Transfer tokens

Transfer tokens from some accounts to other accounts. The transaction must be signed by the sending account. Each negative amount is withdrawn from the corresponding account \(a **sender**\), and each positive one is added to the corresponding account \(a **receiver**\). All amounts must have sum of zero. Each amount is a number with the lowest denomination possible for a token. Example: Token X has 2 decimals. Account A transfers amountof 100 tokens by providing 10000 as amount in the TransferList. If Account A wants to send 100.55 tokens, he must provide 10055 as amount. If any sender account fails to have sufficient token balance, then the entire transaction fails and none of the transfers occur, though transaction fee is still charged.

{% hint style="info" %}
The account must be associated to the token prior to transfering tokens to that account. See TokenAssociateTransaction.
{% endhint %}

| Constructor | Description |
| :--- | :--- |
| `new TransferTransaction()` | Initializes a TokenTransferTransaction object |

```java
new TransferTransaction()
```

### Methods

| Method | Type | Description |
| :--- | :--- | :--- |
| `addHbarTransfer(<accountId, value>)` | AccountID, Hbar/long | The account the transfer is being debited from. The sending account must sign the transaction. The sender and recipient values must net zero. |
| `addTokenTransfer(<tokenId, accountId,value>)` | [TokenId](token-id.md), [AccountId](../specialized-types.md#accountid), long | The ID of the token, the account ID to transfer the tokens from, value of the token to transfer |

{% tabs %}
{% tab title="Java" %}
```java
//Create the transfer transaction
TransferTransaction transaction = new TransferTransaction()
    .addTokenTransfer(tokenId, OPERATOR_ID, new Hbar(10))
    .addTokenTransfer(tokenId, accountId, new Hbar(10));


//Sign with the client operator key and submit the transaction to a Hedera network
TransactionId txId = transaction.execute(client);
        
//Request the receipt of the transaction
TransactionReceipt receipt = txId.getReceipt(client);

//Get the transaction consensus status
Status transactionStatus = receipt.status;

System.out.println("The transaction consensus status is " +transactionStatus);

//v1.3.2

```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Transfer 100 tokens between two accounts
const transaction = new TransferTransaction()
    .addTokenTransfer(tokenId,accountId,100)
    .addTokenTransfer(tokenId, OPERATOR_ID,100);

//Build the unsigned transaction, sign with sender account private key, submit the transaction to a Hedera network
const transactionId = await transaction.build(client).sign(senderKey).execute(client);
    
//Request the receipt of the transaction
const getReceipt = await transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
const transactionStatus = getReceipt.status;

console.log("The transaction consensus status " +transactionStatus);
//Version 1.3.2
```
{% endtab %}
{% endtabs %}





