# Wipe a token

Wipes the provided amount of tokens from the specified Account. This transaction must be signed by the token's Wipe Key and the key of the account is being wiped. Wiping an accounts tokens burns the tokens and decreases the total supply.

* If the provided account is not found, the transaction will resolve to INVALID\_ACCOUNT\_ID.
*  If the provided account has been deleted, the transaction will resolve to ACCOUNT\_DELETED
*  If the provided token is not found, the transaction will resolve to INVALID\_TOKEN\_ID.
*  If the provided token has been deleted, the transaction will resolve to TOKEN\_WAS\_DELETED.
* If an Association between the provided token and account is not found, the transaction will resolve to TOKEN\_NOT\_ASSOCIATED\_TO\_ACCOUNT.
* If Wipe Key is not present in the Token, transaction results in TOKEN\_HAS\_NO\_WIPE\_KEY.
* If the provided account is the token's Treasury Account, transaction results in CANNOT\_WIPE\_TOKEN\_TREASURY\_ACCOUNT
* On success, tokens are removed from the account and the total supply of the token is decreased by the wiped amount.
* The amount provided is in the lowest denomination possible. 
* Example: Token A has 2 decimals. In order to wipe 100 tokens from account, one must provide amount of 10000. In order to wipe 100.55 tokens, one must provide amount of 10055.

| Constructor | Description |
| :--- | :--- |
| `new TokenWipeTransaction()` | Initializes a TokenWipeAccountTransaction object |

```java
new TokenWipeAccountTransaction()
```

### Methods

| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | The ID of the token to wipe from the account | Required |
| `setAmount(<amount>)` | long | The amount of token to wipe from the specified account. Amount must be a positive non-zero number in the lowest denomination possible, not bigger than the token balance of the account \(0; balance\] | Required |
| `setAccount(<accountId>)` | AccountId | The account ID to wipe the tokens from | Required |

{% tabs %}
{% tab title="Java" %}
```java
//Wipe 100 tokens from an account
TokenWipeTransaction transaction = new TokenWipeTransaction()
    .setAccountId(accountId)
    .setTokenId(tokenId)
    .setAmount(100);

Status transactionStatus = transaction.build(client) //Build the unsigned transaction
    .sign(wipeKey) //Sign with the wipe private key
    .sign(accountKey) //Sign with the account private key
    .execute(client) //Submit the transaction to the Hedera network
    .getReceipt(client) //Request the receipt of the transaction
    .status; //Obtain the consensus status of the transaction

System.out.println("The transaction consensus status is " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Wipe 100 tokens from an account
const transaction = await new TokenWipeTransaction()
    .setAccountId(accountId)
    .setTokenId(tokenId)
    .setAmount(100);

const transactionStatus = await (await (await transaction.build(client) //Build the unsigned transaction
    .sign(wipeKey) //Sign with the wipe private key
    .sign(accountKey) //Sign with the account private key
    .execute(client)) //Submit the transaction to the Hedera network
    .getReceipt(client)) //Request the receipt of the transaction
    .status; //Obtain the consensus status of the transaction

console.log("The transaction consensus status is " +transactionStatus);
//Version 1.4.1
```
{% endtab %}
{% endtabs %}





