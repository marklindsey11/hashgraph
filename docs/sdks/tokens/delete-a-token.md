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
| `setTokenId(<tokenId>)` | TokenId | The ID of the token to delete | Required |

{% tabs %}
{% tab title="Java" %}
```java
//Delete a token
TokenDeleteTransaction transaction = new TokenDeleteTransaction()
    .setTokenId(newTokenId);

Status transactionStatus = transaction.build(client) //Build the unsigned transaction
    .sign(adminKey) //Sign with the admin private key of the token
    .execute(client) //Submit the transaction to the hedera network
    .getReceipt(client) //Request the receipt of the transaction
    .status; // Obtain the transaction consensus status

System.out.println("The transaction consensus status is " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Delete a token
const transaction = await new TokenDeleteTransaction()
    .setTokenId(newTokenId);

const transactionStatus = await (await (await transaction.build(client) //Build the unsigned transaction
    .sign(adminKey) //Sign with the admin private key of the token
    .execute(client)) //Submit the transaction to the hedera network
    .getReceipt(client)) //Request the receipt of the transaction
    .status; //Obtain the transaction consensus status

console.log("The transaction consensus status is " +transactionStatus);
//Version 1.4.1
```
{% endtab %}
{% endtabs %}





