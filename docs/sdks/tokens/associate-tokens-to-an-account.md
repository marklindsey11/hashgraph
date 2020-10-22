# Associate tokens to an account

Associates the provided account with the provided tokens. Accounts must be associated with a token first before you can transfer tokens to that account. 

* If the provided account is not found, the transaction will resolve to INVALID\_ACCOUNT\_ID.
* If the provided account has been deleted, the transaction will resolve to ACCOUNT\_DELETED.
* If any of the provided tokens is not found, the transaction will resolve to INVALID\_TOKEN\_REF.
* If any of the provided tokens has been deleted, the transaction will resolve to TOKEN\_WAS\_DELETED.
* If an association between the provided account and any of the tokens already exists, the transaction will resolve to TOKEN\_ALREADY\_ASSOCIATED\_TO\_ACCOUNT.
* If the provided account's associations count exceed the constraint of maximum token associations per account, the transaction will resolve to TOKENS\_PER\_ACCOUNT\_LIMIT\_EXCEEDED.
* On success, associations between the provided account and tokens are made and the account is ready to interact with the tokens.

| Constructor | Description |
| :--- | :--- |
| `new TokenAssociateTransaction()` | Initializes a TokenAssociateTransaction object |

```java
new TokenAssociateTransaction()
```

### Methods

| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setAccountId(<accountId>)` | AccountId | The account to be associated with the provided tokens | Required |
| `addTokenId(<tokenId>)` | TokenId | The tokens to be associated with the provided account | Required |

{% tabs %}
{% tab title="Java" %}
```java
//Associate a token to an account
TokenAssociateTransaction transaction = new TokenAssociateTransaction()
        .setAccountId(accountId)
        .addTokenId(tokenId);

Status transactionStatus = transaction.build(client) //Build the unsigned transaction
         .sign(accountKey) //Sign with the account key
         .execute(client) //Submit the transaction to the Hedera network 
         .getReceipt(client) //Request the transaction receipt
         .status; //Obtain the transaction consensus status

System.out.println("The transaction consensus status " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Associate a token to an account 
const transaction = await new TokenAssociateTransaction()
        .setAccountId(accountId)
        .setTokenIds(tokenId); //Will change to addTokenId()

const transactionStatus = await (await (await transaction.build(client) //Build the unsigned transaction
         .sign(accountKey) //Sign with the account key
         .execute(client)) //Submit the transaction to the Hedera network 
         .getReceipt(client)) //Request the transaction receipt
         .status; //Obtain the transaction consensus status

console.log("The transaction consensus status " +transactionStatus);
//Version 1.4.1
```
{% endtab %}
{% endtabs %}





