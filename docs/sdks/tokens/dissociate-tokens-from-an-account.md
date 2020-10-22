# Dissociate tokens from an account

Disassociates the provided account from the provided tokens. This transaction must be signed by the provided Account's Key. Once the association is removed, no token related operation can be performed to that account. AccountBalanceQuery and AccountInfoQuery will not return anything related to the token that was disassociated.

*  If the provided account is not found, the transaction will resolve to INVALID\_ACCOUNT\_ID.
*  If the provided account has been deleted, the transaction will resolve to ACCOUNT\_DELETED.
*  If any of the provided tokens is not found, the transaction will resolve to INVALID\_TOKEN\_REF.
* If any of the provided tokens has been deleted, the transaction will resolve to TOKEN\_WAS\_DELETED.
* If an association between the provided account and any of the tokens does not exist, the transaction will resolve to TOKEN\_NOT\_ASSOCIATED\_TO\_ACCOUNT.
* If the provided account has a nonzero balance with any of the provided tokens, the transaction will resolve to TRANSACTION\_REQUIRES\_ZERO\_TOKEN\_BALANCES.
* On success, associations between the provided account and tokens are removed.

{% hint style="info" %}
The account is required to have a zero balance of the token you wish disassociates. If a token balance is present, you will receieve a TRANSACTION\_REQUIRES\_ZERO\_TOKEN\_BALANCES error.
{% endhint %}

| Constructor | Description |
| :--- | :--- |
| `new TokenDissociateTransaction()` | Initializes the TokenDissociateTransaction object |

```java
new TokenDissociateTransaction()
```

### Methods

| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | The tokens to be dissociated with the provided account | Required |
| `setAccountId(<accountId>)` | AccountId | The account to be dissociated with the provided tokens | Required |

{% tabs %}
{% tab title="Java" %}
```java
//Disassociate a token from an account
TokenDissociateTransaction transaction = new TokenDissociateTransaction()
    .setAccountId(accountId)
    .addTokenId(tokenId);
        
Status transactionStatus = transaction.build(client) //Build the unsigned transaction
    .sign(accountKey) //Sign with the account private key
    .execute(client) //Submit the transaction to the Hedera network
    .getReceipt(client) //Request the transaction receipt
    .status; //Obtain the consensus status of the transaction

System.out.println("The transaction consensus status is: " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Disassociate a token from an account
const transaction = await new TokenDissociateTransaction()
    .setAccountId(accountId)
    .addTokenId(tokenId);
        
const transactionStatus = await (await (await transaction.build(client) //Build the unsigned transaction
    .sign(accountKey) //Sign with the account private key
    .execute(client)) //Submit the transaction to the Hedera network
    .getReceipt(client)) //Request the transaction receipt
    .status; //Obtain the consensus status of the transaction

console.log("The transaction consensus status is: " +transactionStatus);
//Version 1.4.1
```
{% endtab %}
{% endtabs %}





