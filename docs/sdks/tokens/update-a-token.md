# Update a token

Updates the properties of an existing token. The Admin Key must sign this transaction to update any of the token properties. If no value is given for a field, that field is left unchanged. For an immutable tokens \(that is, a token created without an Admin Key\), only the expiry may be updated. Setting any other field in that case will cause the transaction status to resolve to TOKEN\_IS\_IMMUTABlE.

| Property | Description |
| :--- | :--- |
| **Name** | The new name of the token. Must be a string of ASCII characters. Is not required to be unique. |
| **Symbol** | The new symbol of the token. Must be UTF-8 capitalized alphabetical string identifying the token. Is not required to be unique. |
| **Treasury Account** | The new treasury account of the token. If the provided treasury account is not existing or deleted, the response will be INVALID\_TREASURY\_ACCOUNT\_FOR\_TOKEN. If successful, the Token balance held in the previous Treasury Account is transferred to the new one. |
| **Admin Key** | The new admin key of the token. If token is immutable \(no Admin Key was assigned during token creation\), transaction will resolve to TOKEN\_IS\_IMMUTABlE. |
| **KYC Key** | The new KYC key of the token. If token does not have currently a KYC key, transaction will resolve to TOKEN\_HAS\_NO\_KYC\_KEY. |
| **Freeze Key** | The new freeze key of the token. If the token does not have currently a freeze key, transaction will resolve to TOKEN\_HAS\_NO\_FREEZE\_KEY. |
| **Wipe Key** | The new wipe key of the token. If the token does not have currently a wipe key, transaction will resolve to TOKEN\_HAS\_NO\_WIPE\_KEY. |
| **Supply Key** | The new supply key of the token. If the token does not have currently a supply key, transaction will resolve to TOKEN\_HAS\_NO\_SUPPLY\_KEY. |
| **Expiration Time** | The new expiry time of the token. Expiry can be updated even if the admin key is not set. If the provided expiry is earlier than the current token expiry, transaction wil resolve to INVALID\_EXPIRATION\_TIME.  |
| **Auto Renew Account** | The new account which will be automatically charged to renew the token's expiration, at autoRenewPeriod interval. |
| **Auto Renew Period** | The new interval at which the auto-renew account will be charged to extend the token's expiry. The default auto renew period is 131,500 minutes. |

| Constructor | Description |
| :--- | :--- |
| `new TokenUpdateTransaction()` | Initializes a TokenUpdateTransaction object |

```java
new TokenUpdateTransaction()
```

### Methods

{% tabs %}
{% tab title="V2" %}


| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | Required |
| `setTokenName(<name>)` | String | Optional |
| `setTokenSybmol(<symbol>)` | String | Optional |
| `setTreasuryAccountId(<treasury>)` | AccountId | Optional |
| `setAdminKey(<key>)` | PublicKey | Optional |
| `setKycKey(<key>)` | PublicKey | Optional |
| `setFreezeKey(<key>)` | PublicKey | Optional |
| `setWipeKey(<key>)` | PublicKey | Optional |
| `setSupplyKey(<key>)` | PublicKey | Optional |
| `setFreezeDefault(<freeze>`\) | boolean | Optional |
| `setExpirationTime(<expirationTime>)` | Instant | Optional |
| `setAutoRenewAccountId(<account>)` | AccountId | Disabled |
| `setAutoRenewPeriod(<period>)` | Duration | Disabled |

{% code title="Java" %}
```java
//Create the transaction 
TokenUpdateTransaction transaction = new TokenUpdateTransaction()
     .setTokenId(tokenId)
     .setTokenName("Your New Token Name");

//Freeze the unsigned transaction, sign with the admin private key of the token, submit the transaction to a Hedera network
TransactionResponse txResponse = transaction.freezeWith(client).sign(adminKey).execute(client);

//Request the receipt of the transaction
TransactionReceipt receipt = txResponse.getReceipt(client);

//Get the transaction consensus status
Status transactionStatus = receipt.status;

System.out.println("The transaction consensus status is " +transactionStatus);

//v2.0.1
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create the transaction and freeze for manual signing
const transaction = await new TokenUpdateTransaction()
     .setTokenId(tokenId)
     .setTokenName("Your New Token Name")
     .freezeWith(client);

//Sign the transaction with the admin key
const signTx = await transaction.sign(adminKey);

//Submit the signed transaction to a Hedera network
const txResponse = await signTx.execute(client);

//Request the receipt of the transaction
const receipt = await txResponse.getReceipt(client);

//Get the transaction consensus status
const transactionStatus = receipt.status.toString();

console.log("The transaction consensus status is " +transactionStatus);

//v2.0.5
```
{% endcode %}

{% code title="Go" %}
```go
//Create the transaction and freeze for manual signing 
tokenUpdateTransaction, err := hedera.NewTokenUpdateTransaction().
	  SetTokenID(tokenId).
		SetTokenName("Your New Token Name").
		FreezeWith(client)

if err != nil {
	panic(err)
}

//Sign with the admin private key of the token, sign with the client operator private key and submit the transaction to a Hedera network
txResponse, err := tokenUpdateTransaction.Sign(adminKey).Execute(client)

if err != nil {
	panic(err)
}

//Request the receipt of the transaction
receipt, err := txResponse.GetReceipt(client)
if err != nil {
	panic(err)
}

//Get the transaction consensus status
status := receipt.Status

fmt.Printf("The transaction consensus status is %v\n", status)

//v2.1.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | Required  |
| `setName(<name>)` | String | Optional |
| `setSybmol(<symbol>)` | String | Optional |
| `setTreasury(<treasury>)` | AccountId | Optional |
| `setAdminKey(<key>)` | PublicKey | Optional |
| `setKycKey(<key>)` | PublicKey | Optional |
| `setFreezeKey(<key>)` | PublicKey | Optional |
| `setWipeKey(<key>)` | PublicKey | Optional |
| `setSupplyKey(<key>)` | PublicKey | Optional |
| `setFreezeDefault(<freeze>`\) | boolean | Optional |
| `setExpirationTime(<expirationTime>)` | Instant | Optional |
| `setAutoRenewAccount(<account>)` | AccountId | Optional |
| `setAutoRenewPeriod(<period>)` | Duration | Optional |

{% code title="Java" %}
```java
//Update the name of the token
TokenUpdateTransaction transaction = new TokenUpdateTransaction()
    .setTokenId(newTokenId)
    .setName("Your New Token Name");

//Build the unsigned transaction, sign with the admin private key of the token, submit the transaction to a Hedera network
TransactionId transactionId = transaction.build(client).sign(adminKey).execute(client);
    
//Request the receipt of the transaction
TransactionReceipt receipt = transactionId.getReceipt(client);
    
//Get the transaction consensus status
Status transactionStatus = receipt.status;

System.out.println("The transaction consensus status is " +transactionStatus);
//Version: 1.2.2
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Update the name of the token
const transaction = new TokenUpdateTransaction()
    .setTokenId(newTokenId)
    .setName("Your New Token Name");
    
//Build the unsigned transaction, sign with the token admin private key of the token, submit the transaction to a Hedera network
const transactionId = await transaction.build(client).sign(adminKey).execute(client);
    
//Request the receipt of the transaction
const receipt = await transactionId.getReceipt(client);
    
//Get the transaction consensus status
const transactionStatus = receipt.status;

console.log("The transaction consensus status is " +transactionStatus);
//Version: 1.4.2
```
{% endcode %}
{% endtab %}
{% endtabs %}



