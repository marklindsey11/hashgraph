# Enable KYC account flag

Grants KYC to the account for the given token. This transation must be signed by the token's KYC Key.

* If the provided account is not found, the transaction will resolve to INVALID\_ACCOUNT\_ID.
* If the provided account has been deleted, the transaction will resolve to ACCOUNT\_DELETED.
* If the provided token is not found, the transaction will resolve to INVALID\_TOKEN\_ID.
* If the provided token has been deleted, the transaction will resolve to TOKEN\_WAS\_DELETED.
* If an Association between the provided token and account is not found, the transaction will resolve to
* TOKEN\_NOT\_ASSOCIATED\_TO\_ACCOUNT.
* If no KYC Key is defined, the transaction will resolve to TOKEN\_HAS\_NO\_KYC\_KEY.
* Once executed the Account is marked as KYC Granted.

| Constructor | Description |
| :--- | :--- |
| `new TokenGrantKycTransaction()` | Initializes the TokenGrantKycTransaction object |

```java
new TokenGrantKycTransaction()
```

### Methods

| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | The token for this account to have passed KYC | Required |
| `setAccountId(<accountId>)` | AccountId | The account for this token to have passed KYC | Required |

{% tabs %}
{% tab title="Java" %}
```java
//Enable KYC flag on account
TokenGrantKycTransaction transaction = new TokenGrantKycTransaction()
    .setTokenId(newTokenId)
    .setAccountId(newAccountId);

Status transactionStatus = transaction.build(client) //Build the unsigned transaction
    .sign(kycKey) //Sign with the kyc private key
    .execute(client) //Submit the transaction to a Hedera network
    .getReceipt(client) //Request the receipt of the transaction
    .status; //Confirm that transaction reached consensus

System.out.println("The transaction consensus status is " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Enable KYC flag on account
const transaction = await new TokenGrantKycTransaction()
    .setTokenId(newTokenId)
    .setAccountId(newAccountId);

const transactionStatus = await (await (await transaction.build(client) //Build the unsigned transaction
    .sign(kycKey) //Sign with the kyc private key
    .execute(client)) //Submit the transaction to a Hedera network
    .getReceipt(client)) //Request the receipt of the transaction
    .status; //Confirm that transaction reached consensus

console.log("The transaction consensus status is " +transactionStatus);
//Version 1.4.1 
```
{% endtab %}
{% endtabs %}





