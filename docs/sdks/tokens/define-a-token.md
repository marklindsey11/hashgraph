# Define a token

Create a new token on the Hedera network. After you submit the transaction to the Hedera network, you can obtain the new token ID by requesting the receipt. Smart contracts cannot access or transfer HTS tokens at this time.

* The specified Treasury Account is receiving the initial supply of tokens as-well as the tokens from the Token Mint operation once executed. 
* The balance of the treasury account is decreased when the Token Burn operation is executed. You must the Supply Key if you wish to burn tokens in the future. If you do not set the Supply Key upon creation of the token, you may update the token properties using the TokenUpdateTransaction.
* The supply that is going to be put in circulation is going to be the initial supply provided
* The maximum supply a token can have is 9,223,372,036,854,775,807 \(`2^63-1`\) tokens
* The supply is in the lowest denomination possible
* Example: Token A has initial supply set to 10\_000 and decimals set to 2. The tokens that will be put into circulation are going be 100. Token B has initial supply set to 10\_012\_345\_678 and decimals set to 8. The number of tokens that will be put into circulation are going to be 100.12345678
* The transaction has to be signed by the Admin Key of the new token
* Creating immutable token: Token can be created as immutable if the adminKey is omitted. In this case, the name, symbol, treasury, management keys, expiry and renew properties 

You can set the following properties when creating a token:

| Property | Description |
| :--- | :--- |
| **Name** | Set the publicly visible name of the token, specified as a string of UTF-8 characters. Maximum of 100 characters. The token name is not unique. |
| **Symbol** | The publicly visible token symbol. It is UTF-8 capitalized alphabetical string identifying the token. The token symbol is not unique. Maximum of 100 characters. |
| **Decimal** | The number of decimal places a token is divisible by. This field can never be changed! |
| **Initial Supply** | Specifies the initial supply of tokens to be put in circulation.The initial supply is sent to the Treasury Account. The maximum supply of tokens is `9,223,372,036,854,775,807` tokens and  is in the lowest denomination possible. If the total supply is `S` tokens, and `S` is an `N` digit number, and the token is using `D` decimals, then `S * 10^D` must be equal to or less than `2^63-1`, which is  `9,223,372,036,854,775,807.`This means it is always ok if `N+D` is 18 or less.It is also ok if `N+D` is 19, and the first digit of `S` is 8 or less.If decimals is 8 or 11, then the total supply can be a few billions or millions, respectively. For example, it could match Bitcoin \(21 million tokens with 8 decimals\) or hbars \(50 billion tokens with 8 decimals\). It could even match Bitcoin with milli-satoshis \(21 million tokens with 11 decimals\).  |
| **Treasury Account** | The account which will act as a treasury for the token. This account will receive the specified initial supply. The Token Treasury Account is required to sign the TokenCreateTransaction. |
| **Admin Key** | The key which can perform update/delete operations on the token.The Admin Key has the authority to change the Freeze Key, Wipe Key, and KYC Key. It can also update the treasury account.  If empty, the token can be perceived as immutable \(not being able to be updated/deleted\). This key is required to sign transaction if present. |
| **KYC Key** | The key which can grant or revoke KYC of an account for the token's transactions. If empty, KYC is not required, and KYC grant or revoke operations are not possible.  |
| **Freeze Key** | The key which can sign to freeze or unfreeze an account for token transactions. If empty, freezing is not possible.  |
| **Wipe Key** | The key which can wipe the token balance of an account. If empty, wipe is not possible.  |
| **Supply Key** | The key which can change the total supply of a token. This key is used to sign Token Mint/Burn operations. If this is left empty minting/burning tokens is not possible.  |
| **Freeze Default** | The default Freeze status \(frozen or unfrozen\) of Hedera accounts relative to this token. If true, an account must be unfrozen before it can receive the token |
| **Expiration Time** | The epoch second at which the token should expire; if an auto-renew account and period are specified, this is coerced to the current epoch second plus the autoRenewPeriod. The default expiration time is 90 days. |
| **Auto Renew Account** | An account which will be automatically charged to renew the token's expiration, at autoRenewPeriod interval. This key is required to sign transaction if present. |
| **Auto Renew Period** | The interval at which the auto-renew account will be charged to extend the token's expiry. The default auto renew period is 131,500 minutes. |

| Constructor | Description |
| :--- | :--- |
| `new TokenCreateTransaction()` | Initializes the TokenCreateTransaction object |

```java
new TokenCreateTransaction()
```

### Methods

{% tabs %}
{% tab title="V2" %}


| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setTokenName(<name>)` | String | Required |
| `setTokenSybmol(<symbol>)` | String | Required |
| `setDecimals(<decimal>)` | int | Optional |
| `setInitialSupply(<initialSupply>)`   | int | Optional |
| `setTreasuryAccountId(<treasury>)` | [AccountId](../specialized-types.md#accountid) | Required |
| `setAdminKey(<key>)` | Key | Optional |
| `setKycKey(<key>)` | Key | Optional |
| `setFreezeKey(<key>)` | Key | Optional |
| `setWipeKey(<key>)` | Key | Optional |
| `setSupplyKey(<key>)` | Key | Optional |
| `setFreezeDefault(<freeze>`\) | boolean | Optional |
| `setExpirationTime(<expirationTime>)` | Instant | Required |
| `setAutoRenewAccountId(<account>)` | [AccountId](../specialized-types.md#accountid) | Disabled |
| `setAutoRenewPeriod(<period>)` | Duration | Disabled |

{% code title="Java" %}
```java
//Create the transaction
TokenCreateTransaction transaction = new TokenCreateTransaction()
        .setTokenName("Your Token Name")
        .setTokenSymbol("F")
        .setTreasuryAccountId(treasuryAccountId)
        .setInitialSupply(5000)
        .setAdminKey(adminKey.getPublicKey())
        .setMaxTransactionFee(new Hbar(30)); //Change the default max transaction fee

//Build the unsigned transaction, sign with admin private key of the token, sign with the token treasury private key, submit the transaction to a Hedera network
TransactionResponse txResponse = transaction.freezeWith(client).sign(adminKey).sign(treasuryKey).execute(client);

//Request the receipt of the transaction
TransactionReceipt receipt = txResponse.getReceipt(client);

//Get the token ID from the receipt
TokenId tokenId = receipt.tokenId;

System.out.println("The new token ID is " + tokenId);

//v2.0.1
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create the transaction and freeze for manual signing
const transaction = await new TokenCreateTransaction().
     .setTokenName("Your Token Name")
     .setTokenSymbol("F")
     .setTreasuryAccountId(treasuryAccountId)
     .setInitialSupply(5000)
     .setAdminKey(adminPublicKey)
     .setMaxTransactionFee(new Hbar(30)) //Change the default max transaction fee
     .freezeWith(client);

//Sign the transaction with the token adminKey and the token treasury account private key
const signTx =  await (await transaction.sign(adminKey)).sign(treasuryKey);

//Sign the transaction with the client operator private key and submit to a Hedera network
const txResponse = await signTx.execute(client);
    
//Get the receipt of the transaction
const receipt = await txResponse.getReceipt(client);

//Get the token ID from the receipt
const tokenId = receipt.tokenId;

console.log("The new token ID is " + tokenId);

//v2.0.5
```
{% endcode %}

{% code title="Go" %}
```go
//Create the transaction and freeze the unsigned transaction
tokenCreateTransaction, err := hedera.NewTokenCreateTransaction().
	  SetTokenName("Your Token Name").
		SetTokenSymbol("F").
		SetTreasuryAccountID(treasuryAccountId).
		SetInitialSupply(1000).
		SetAdminKey(adminKey).
		SetMaxTransactionFee(hedera.NewHbar(30)). //Change the default max transaction fee
		FreezeWith(client)

if err != nil {
	panic(err)
}

//Sign with the admin private key of the token, sign with the token treasury private key, sign with the client operator private key and submit the transaction to a Hedera networ
txResponse, err := tokenCreateTransaction.Sign(adminKey).Sign(treasuryKey).Execute(client)

if err != nil {
	panic(err)
}

//Request the receipt of the transaction
receipt, err := txResponse.GetReceipt(client)
if err != nil {
	panic(err)
}

//Get the token ID from the receipt
tokenId := *receipt.TokenID

fmt.Printf("The new token ID is %v\n", tokenId)

//v2.1.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setName(<name>)` | String | Required |
| `setSybmol(<symbol>)` | String | Required |
| `setDecimals(<decimal>)` | int | Optional |
| `setInitialSupply(<initialSupply>)`   | int | Optional |
| `setTreasury(<treasury>)` | [AccountId](../specialized-types.md#accountid) | Required |
| `setAdminKey(<key>)` | [PublicKey](../keys/generate-a-new-key-pair.md) | Required |
| `setKycKey(<key>)` | [PublicKey](../keys/generate-a-new-key-pair.md) | Optional |
| `setFreezeKey(<key>)` | [PublicKey](../keys/generate-a-new-key-pair.md) | Optional |
| `setWipeKey(<key>)` | [PublicKey](../keys/generate-a-new-key-pair.md) | Optional |
| `setSupplyKey(<key>)` | [PublicKey](../keys/generate-a-new-key-pair.md) | Optional |
| `setFreezeDefault(<freeze>`\) | boolean | Optional |
| `setExpirationTime(<expirationTime>)` | Instant | Required |
| `setAutoRenewAccount(<account>)` | [AccountId](../specialized-types.md#accountid) | Optional |
| `setAutoRenewPeriod(<period>)` | Duration | Optional |

{% code title="Java" %}
```java
//Create a token
TokenCreateTransaction transaction = new TokenCreateTransaction()
    .setName("Your Token Name")
    .setSymbol("F")
    .setTreasury(treasuryAccountId)
    .setInitialSupply(5000)
    .setAdminKey(adminKey.publicKey);

//Build the unsigned transaction, sign with admin private key of the token, sign with the token treasury private key, submit the transaction to a Hedera network
TransactionId transactionId = transaction.build(client).sign(adminKey).sign(treasuryKey).execute(client);

//Request the receipt of the transaction
TransactionReceipt getReceipt = transactionId.getReceipt(client);

//Get the token ID from the receipt
TokenId tokenId = getReceipt.getTokenId();

System.out.println("The new token ID is " +tokenId);

//Version: 1.2.2
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create a token
const transaction = new TokenCreateTransaction()
    .setName("Your Token Name")
    .setSymbol("F")
    .setTreasury(treasuryAccountId)
    .setInitialSupply(5000)
    .setAdminKey(adminKey.publicKey);

//Build the unsigned transaction, sign with the admin private key of the token, sign with the token treasury private key, submit the transaction to a Hedera network
const transactionId = await transaction.build(client).sign(adminKey).sign(treasuryKey).execute(client);

//Request the receipt of the transaction
const getReceipt = await transactionId.getReceipt(client);

//Get the token ID from the receipt
const tokenId = getReceipt.getTokenId();

console.log("The new token ID is " +tokenId);

//Version: 1.4.2
```
{% endcode %}
{% endtab %}
{% endtabs %}



