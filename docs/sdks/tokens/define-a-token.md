# Create a token

{% hint style="info" %}
Check out "Getting Started with the Hedera Token Service" video tutorial in JavaScript [here](https://youtu.be/JZDAMScxbpU).
{% endhint %}

Create a new fungible or non-fungible token \(NFT\) on the Hedera network. After you submit the transaction to the Hedera network, you can obtain the new token ID by requesting the receipt. Smart contracts cannot access or transfer HTS tokens at this time.

**NFTs**

For non-fungible tokens, the token ID represents a NFT class. Once the token is created, you will have to mint each NFT using the [token mint](mint-a-token.md) operation.

**Token Properties**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Property</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Name</b>
      </td>
      <td style="text-align:left">Set the publicly visible name of the token. The token name is specified
        as a string of UTF-8 characters. The token name is not unique. Maximum
        of 100 characters.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Token Type</b>
      </td>
      <td style="text-align:left">The type of token to create. Either fungible or non-fungible.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Symbol</b>
      </td>
      <td style="text-align:left">The publicly visible token symbol. It is UTF-8 capitalized alphabetical
        string identifying the token. The token symbol is not unique. Maximum of
        100 characters.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Decimal</b>
      </td>
      <td style="text-align:left">The number of decimal places a token is divisible by. This field can never
        be changed.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Initial Supply</b>
      </td>
      <td style="text-align:left">Specifies the initial supply of fungible tokens to be put in circulation.
        The initial supply is sent to the Treasury Account. The maximum supply
        of tokens is <code>9,223,372,036,854,775,807</code>(<code>2^63-1</code>)
        tokens and is in the lowest denomination possible. For creating an NFT,
        you must set the initial supply to 0.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Treasury Account</b>
      </td>
      <td style="text-align:left">The account which will act as a treasury for the token. This account will
        receive the specified initial supply and any additional tokens that are
        minted. If tokens are burned, the supply will decreased from the treasury
        account.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Admin Key</b>
      </td>
      <td style="text-align:left">The key which can perform token update and token delete operations on
        the token.The admin key has the authority to change the freeze key, wipe
        key, and KYC key. It can also update the treasury account of the token.
        If empty, the token can be perceived as immutable (not being able to be
        updated/deleted).</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>KYC Key</b>
      </td>
      <td style="text-align:left">The key which can grant or revoke KYC of an account for the token&apos;s
        transactions. If empty, KYC is not required, and KYC grant or revoke operations
        are not possible.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Freeze Key</b>
      </td>
      <td style="text-align:left">The key which can sign to freeze or unfreeze an account for token transactions.
        If empty, freezing is not possible.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Wipe Key</b>
      </td>
      <td style="text-align:left">The key which can wipe the token balance of an account. If empty, wipe
        is not possible.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Supply Key</b>
      </td>
      <td style="text-align:left">The key which can change the total supply of a token. This key is used
        to authorize token mint and burn transactions. If this is left empty, minting/burning
        tokens is not possible.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Fee Schedule Key</b>
      </td>
      <td style="text-align:left">The key that can change the token&apos;s <a href="custom-token-fees.md">custom fee</a> schedule.
        A custom fee schedule token without a fee schedule key is immutable.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Fee Schedule Key</b>
      </td>
      <td style="text-align:left">The key which can change the token&apos;s custom fee schedule; must sign
        a TokenFeeScheduleUpdate transaction.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Custom Fees</b>
      </td>
      <td style="text-align:left">
        <p><a href="custom-token-fees.md">Custom fees</a> to charge during a token
          transfer transaction that transfers units of this token. Custom fees can
          either be <a href="custom-token-fees.md#fixed-fee">fixed</a>, <a href="custom-token-fees.md#fractional-fee">fractional</a>,
          or <a href="custom-token-fees.md#royalty-fee">royalty</a> fees. You can set
          up to a maximum of 10 custom fees.
          <br />
        </p>
        <p>&#x26A0; Note: The 0.17 Hedera Services release allows for 1 royalty fee
          to be charged for a non-funigble token. This limitation will be removed
          in the 0.18 release.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Max Supply</b>
      </td>
      <td style="text-align:left">For tokens of type <code>FUNGIBLE_COMMON</code> - the maximum number of
        tokens that can be in circulation.
        <br />For tokens of type <code>NON_FUNGIBLE_UNIQUE</code> - the maximum number
        of NFTs (serial numbers) that can be minted. This field can never be changed.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Supply Type</b>
      </td>
      <td style="text-align:left">Specifies the token supply type. Defaults to INFINITE.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Freeze Default</b>
      </td>
      <td style="text-align:left">The default Freeze status (frozen or unfrozen) of Hedera accounts relative
        to this token. If true, an account must be unfrozen before it can receive
        the token.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Expiration Time</b>
      </td>
      <td style="text-align:left">The epoch second at which the token should expire; if an auto-renew account
        and period are specified, this is coerced to the current epoch second plus
        the autoRenewPeriod. The default expiration time is 90 days.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Auto Renew Account</b>
      </td>
      <td style="text-align:left">An account which will be automatically charged to renew the token&apos;s
        expiration, at autoRenewPeriod interval. This key is required to sign the
        transaction if present. This is not currently enabled.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Auto Renew Period</b>
      </td>
      <td style="text-align:left">The interval at which the auto-renew account will be charged to extend
        the token&apos;s expiry. The default auto-renew period is 131,500 minutes.
        This is not currently enabled.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Memo</b>
      </td>
      <td style="text-align:left">A short publicly visible memo about the token.</td>
    </tr>
  </tbody>
</table>

**Transaction Signing Requirements:**

* Treasury key is required to sign
* Admin key, if specified 
* Freeze key, if specified 
* Wipe key, if specified
* Supply key, if specified 
* Fee schedule key, if specified
* Transaction fee payer key

| Constructor | Description |
| :--- | :--- |
| `new TokenCreateTransaction()` | Initializes the TokenCreateTransaction object |

```java
new TokenCreateTransaction()
```

## Methods

{% tabs %}
{% tab title="V2" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setTokenName(<name>)` | String | Required |
| `setTokenType(<tokenType>)` | [TokenType](token-types.md) | Optional |
| `setTokenSymbol(<symbol>)` | String | Required |
| `setDecimals(<decimal>)` | int | Optional |
| `setInitialSupply(<initialSupply>)` | int | Optional |
| `setTreasuryAccountId(<treasury>)` | [AccountId](../specialized-types.md#accountid) | Required |
| `setAdminKey(<key>)` | Key | Optional |
| `setKycKey(<key>)` | Key | Optional |
| `setFreezeKey(<key>)` | Key | Optional |
| `setWipeKey(<key>)` | Key | Optional |
| `setSupplyKey(<key>)` | Key | Optional |
| `setFreezeDefault(<freeze>`\) | boolean | Optional |
| `setExpirationTime(<expirationTime>)` | Instant | Optional |
| `setFeeScheduleKey(<key>)` | Key | Optional |
| `setCustomFees(<customFees>)` | List&lt;[CustomFee](custom-token-fees.md#custom-fee)&gt; | Optional |
| `setSupplyType(<supplyType>)` | TokenSupplyType | Optional |
| `setMaxSupply(<maxSupply>)` | long | Optional |
| `setTokenMemo(<memo>)` | String | Optional |
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
const transaction = await new TokenCreateTransaction()
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

//Sign with the admin private key of the token, sign with the token treasury private key, sign with the client operator private key and submit the transaction to a Hedera network
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
| `setTokenType(<tokenType>)` | [TokenType](token-types.md) | Optional |
| `setSymbol(<symbol>)` | String | Required |
| `setDecimals(<decimal>)` | int | Optional |
| `setInitialSupply(<initialSupply>)` | int | Optional |
| `setTreasury(<treasury>)` | [AccountId](../specialized-types.md#accountid) | Required |
| `setAdminKey(<key>)` | [PublicKey](../keys/generate-a-new-key-pair.md) | Required |
| `setKycKey(<key>)` | [PublicKey](../keys/generate-a-new-key-pair.md) | Optional |
| `setFreezeKey(<key>)` | [PublicKey](../keys/generate-a-new-key-pair.md) | Optional |
| `setWipeKey(<key>)` | [PublicKey](../keys/generate-a-new-key-pair.md) | Optional |
| `setSupplyKey(<key>)` | [PublicKey](../keys/generate-a-new-key-pair.md) | Optional |
| `setCustomFees(<customFee>)` | List&lt;[CustomFee](../../hedera-api/token-service/customfees/customfee.md)&gt; | Optional |
| `setFeeScheduleKey(<key>)` | PublicKey | Optional |
| `setMaxSupply(<maxSupply>)` | long | Optional |
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



