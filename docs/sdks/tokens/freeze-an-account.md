# Freeze an account

Freezes transfers of the specified token for the account. Must be signed by the token's Freeze Key. 

* If the provided account is not found, the transaction will resolve to INVALID\_ACCOUNT\_ID. If the provided account has been deleted, the transaction will resolve to ACCOUNT\_DELETED.
* If the provided token is not found, the transaction will resolve to INVALID\_TOKEN\_ID.
* If the provided token has been deleted, the transaction will resolve to TOKEN\_WAS\_DELETED.
* If an Association between the provided token and account is not found, the transaction will resolve to TOKEN\_NOT\_ASSOCIATED\_TO\_ACCOUNT.
* If no Freeze Key is defined, the transaction will resolve to TOKEN\_HAS\_NO\_FREEZE\_KEY.
* Once executed the Account is marked as Frozen and will not be able to receive or send tokens unless unfrozen.
* The operation is idempotent

| Constructor | Description |
| :--- | :--- |
| `new TokenFreezeTransaction()` | Initializes the TokenFreezeTransaction object |

```java
new TokenFreezeTransaction()
```

### Methods

| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | The token for this account to be frozen | Required |
| `setAccountId(<accountId>)` | AccountId | The account to be frozen | Required |

{% tabs %}
{% tab title="Java" %}
```java
//Freeze an account from transferring a token
TokenFreezeTransaction transaction = new TokenFreezeTransaction()
    .setAccountId(newAccountId)
    .setTokenId(newTokenId);

Status transactionStatus = transaction.build(client) //Build the unsigned transaction
    .sign(freezeKey) //Sign with the token's freeze private key
    .execute(client) //Submit the transaction to a Hedera network
    .getReceipt(client) //Request the receipt of the transaction
    .status; //Obtain the transaction consensus status
    
System.out.print("The transaction consensus status is " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Freeze an account from transferring a token
const transaction = await new TokenFreezeTransaction()
    .setAccountId(newAccountId)
    .setTokenId(newTokenId);

const transactionStatus = await (await (await transaction.build(client) //Build the unsigned transaction
    .sign(freezeKey) //Sign with the token's freeze private key
    .execute(client)) //Submit the transaction to a Hedera network
    .getReceipt(client)) //Request the receipt of the transaction
    .status; //Obtain the transaction consensus status
    
console.log("The transaction consensus status is " +transactionStatus);
//Version 1.4.1
```
{% endtab %}
{% endtabs %}





