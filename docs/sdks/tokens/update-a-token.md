# Update a token

Updates the properties of an existing token. The Admin Key must sign this transaction to update any of the token properties. If no value is given for a field, that field is left unchanged. For an immutable tokens \(that is, a token created without an Admin Key\), only the expiry may be updated. Setting any other field in that case will cause the transaction status to resolve to TOKEN\_IS\_IMMUTABlE.

| Property | Description |
| :--- | :--- |
| **Name** | The new Name of the Token. Must be a string of ASCII characters. Is not required to be unique. |
| **Symbol** | The new Symbol of the Token. Must be UTF-8 capitalized alphabetical string identifying the token. Is not required to be unique. |
| **Treasury Account** | The new Treasury account of the Token. If the provided treasury account is not existing or deleted, the response will be INVALID\_TREASURY\_ACCOUNT\_FOR\_TOKEN. If successful, the Token balance held in the previous Treasury Account is transferred to the new one. |
| **Admin Key** | The new Admin Key of the Token. If Token is immutable \(no Admin Key was assigned during token creation\), transaction will resolve to TOKEN\_IS\_IMMUTABlE. |
| **KYC Key** | The new KYC Key of the Token. If Token does not have currently a KYC Key, transaction will resolve to TOKEN\_HAS\_NO\_KYC\_KEY. |
| **Freeze Key** | The new Freeze Key of the Token. If the Token does not have currently a Freeze Key, transaction will resolve to TOKEN\_HAS\_NO\_FREEZE\_KEY. |
| **Wipe Key** | The new Wipe Key of the Token. If the Token does not have currently a Wipe Key, transaction will resolve to TOKEN\_HAS\_NO\_WIPE\_KEY. |
| **Supply Key** | The new Supply Key of the Token. If the Token does not have currently a Supply Key, transaction will resolve to TOKEN\_HAS\_NO\_SUPPLY\_KEY. |
| **Expiration Time** | The new expiry time of the token. Expiry can be updated even if the Admin Key is not set. If the provided expiry is earlier than the current token expiry, transaction wil resolve to INVALID\_EXPIRATION\_TIME.  |
| **Auto Renew Account** | The new account which will be automatically charged to renew the token's expiration, at autoRenewPeriod interval. |
| **Auto Renew Period** | The new interval at which the auto-renew account will be charged to extend the token's expiry. Default:  |

| Constructor | Description |
| :--- | :--- |
| `new TokenUpdateTransaction()` | Initializes a TokenUpdateTransaction object |

```java
new TokenUpdateTransaction()
```

### Methods

| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | Required  |
| `setName(<name>)` | String | Optional |
| `setSybmol(<symbol>)` | String | Optional |
| `setTreasury(<treasury>)` | AccountId | Optional |
| `setAdminKey(<key>)` | [PublicKey](../keys/) | Optional |
| `setKycKey(<key>)` | [PublicKey](../keys/) | Optional |
| `setFreezeKey(<key>)` | [PublicKey](../keys/) | Optional |
| `setWipeKey(<key>)` | [PublicKey](../keys/) | Optional |
| `setSupplyKey(<key>)` | [PublicKey](../keys/) | Optional |
| `setFreezeDefault(<freeze>`\) | boolean | Optional |
| `setExpirationTime(<expirationTime>)` | Instant | Optional |
| `setAutoRenewAccount(<account>)` | [AccountId](../specialized-types.md#accountid) | Optional |
| `setAutoRenewPeriod(<period>)` | Duration | Optional |

{% tabs %}
{% tab title="Java" %}
```java
//Update the name of the token
TokenUpdateTransaction transaction = new TokenUpdateTransaction()
    .setTokenId(newTokenId)
    .setName("Your New Token Name");

//Build the unsigned transaction, sign with the admin private key of the token, submit the transaction to a Hedera network
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
//Update the name of the token
const transaction = new TokenUpdateTransaction()
    .setTokenId(newTokenId)
    .setName("Your New Token Name");
    
//Build the unsigned transaction, sign with the token admin private key of the token, submit the transaction to a Hedera network
const transactionId = await transaction.build(client).sign(adminKey).execute(client);
    
//Request the receipt of the transaction
const getReceipt = await transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
const transactionStatus = getReceipt.status;

console.log("The transaction consensus status is " +transactionStatus);
//Version: 1.4.2
```
{% endtab %}
{% endtabs %}





