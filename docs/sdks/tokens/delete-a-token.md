# Delete a token

Deleting a token marks a token as deleted, though it will remain in the ledger. The operation must be signed by the specified Admin Key of the Token. If the Admin Key is not set, Transaction will result in TOKEN\_IS\_IMMUTABlE. Once deleted update, mint, burn, wipe, freeze, unfreeze, grant kyc, revoke kyc and token transfer transactions will resolve to TOKEN\_WAS\_DELETED.

| Constructor | Description |
| :--- | :--- |
| `new TokenDeleteTransaction()` | Initializes the TokenDeleteTransaction object |

```java
new TokenDeleteTransaction()
```

### Methods

| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | [TokenId](token-id.md) | The ID of the token to delete | Required |

{% tabs %}
{% tab title="Java" %}
```java
//Delete a token
TokenDeleteTransaction transaction = new TokenDeleteTransaction()
    .setTokenId(newTokenId);

//Build the unsigned transaction, sign with the admin private key of the account, submit the transaction to a Hedera network
TransactionId transactionId = transaction.build(client).sign(adminKey).execute(client);
    
//Request the receipt of the transaction
TransactionReceipt getReceipt = transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
Status transactionStatus = getReceipt.status;

System.out.println("The transaction consensus status is " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Delete a token
const transaction = new TokenDeleteTransaction()
    .setTokenId(newTokenId);

//Build the unsigned transaction, sign with admin private key of the token, submit the transaction to a Hedera network
const transactionId = await transaction.build(client).sign(adminKey).execute(client);
    
//Request the receipt of the transaction
const getReceipt = await transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
const transactionStatus = getReceipt.status;

console.log("The transaction consensus status is " +transactionStatus);
//Version 1.4.2
```
{% endtab %}
{% endtabs %}



