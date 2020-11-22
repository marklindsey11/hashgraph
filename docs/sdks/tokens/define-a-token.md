# Define a token

Create a new token on the Hedera network. After you submit the transaction to the Hedera network, you can obtain the new token ID by requesting the receipt. Smart contracts cannot access or transfer HTS tokens at this time.

* The specified Treasury Account is receiving the initial supply of tokens as-well as the tokens from the Token Mint operation once executed. 
* The balance of the treasury account is decreased when the Token Burn operation is executed. You must the Supply Key if you wish to burn tokens in the future. If you do not set the Supply Key upon creation of the token, you may update the token properties using the TokenUpdateTransaction.
* The supply that is going to be put in circulation is going to be the initial supply provided
* The maximum supply a token can have is 2^63-1
* Example: Token A has initial supply set to 10\_000 and decimals set to 2. The tokens that will be put into circulation are going be 100. Token B has initial supply set to 10\_012\_345\_678 and decimals set to 8. The number of tokens that will be put into circulation are going to be 100.12345678
* The transaction has to be signed by the Admin Key of the new token
* Creating immutable token: Token can be created as immutable if the adminKey is omitted. In this case, the name, symbol, treasury, management keys, expiry and renew properties 

You can set the following properties when creating a token:

| Property | Description |
| :--- | :--- |
| **Name** | Set the publicly visible name of the token, specified as a string of only ASCII characters. Maximum of 100 characters. |
| **Symbol** | The publicly visible token symbol. It is UTF-8 capitalized alphabetical string identifying the token. |
| **Decimal** | The number of decimal places a token is divisible by. This field can never be changed! |
| **Initial Supply** | Specifies the initial supply of tokens to be put in circulation.The initial supply is sent to the Treasury Account. The supply is in the lowest denomination possible. Max supply: 2^63-1 tokens. |
| **Treasury Account** | The account which will act as a treasury for the token. This account will receive the specified initial supply. The Token Treasury Account is required to sign the TokenCreateTransaction. |
| **Admin Key** | The key which can perform update/delete operations on the token.The Admin Key has the authority to change the Freeze Key, Wipe Key, and KYC Key. It can also update the treasury account.  If empty, the token can be perceived as immutable \(not being able to be updated/deleted\). This key is required to sign transaction if present. |
| **KYC Key** | The key which can grant or revoke KYC of an account for the token's transactions. If empty, KYC is not required, and KYC grant or revoke operations are not possible.  |
| **Freeze Key** | The key which can sign to freeze or unfreeze an account for token transactions. If empty, freezing is not possible.  |
| **Wipe Key** | The key which can wipe the token balance of an account. If empty, wipe is not possible.  |
| **Supply Key** | The key which can change the total supply of a token. This key is used to sign Token Mint/Burn operations. If this is left empty minting/burning tokens is not possible.  |
| **Freeze Default** | The default Freeze status \(frozen or unfrozen\) of Hedera accounts relative to this token. If true, an account must be unfrozen before it can receive the token |
| **Expiration Time** | The epoch second at which the token should expire; if an auto-renew account and period are specified, this is coerced to the current epoch second plus the autoRenewPeriod. The default expiration time is 90 days. |
| **Auto Renew Account** | An account which will be automatically charged to renew the token's expiration, at autoRenewPeriod interval. This key is required to sign transaction if present. |
| **Set Auto Renew Period** | The interval at which the auto-renew account will be charged to extend the token's expiry. The default auto renew period is 131,500 minutes. |

| Constructor | Description |
| :--- | :--- |
| `new TokenCreateTransaction()` | Initializes the TokenCreateTransaction object |

```java
new TokenCreateTransaction()
```

### Methods

<table>
  <thead>
    <tr>
      <th style="text-align:left">Method</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Requirement</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>setName(&lt;name&gt;)</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Required</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setSybmol(&lt;symbol&gt;)</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Required</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setDecimals(&lt;decimal&gt;)</code>
      </td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">Optional</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setInitialSupply(&lt;initialSupply&gt;) </code>
      </td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">Optional</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setTreasury(&lt;treasury&gt;)</code>
      </td>
      <td style="text-align:left"><a href="../specialized-types.md#accountid">AccountId</a>
      </td>
      <td style="text-align:left">Required</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setAdminKey(&lt;key&gt;)</code>
      </td>
      <td style="text-align:left"><a href="../keys/">PublicKey</a>
      </td>
      <td style="text-align:left">Optional</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setKycKey(&lt;key&gt;)</code>
      </td>
      <td style="text-align:left"><a href="../keys/">PublicKey</a>
      </td>
      <td style="text-align:left">Optional</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setFreezeKey(&lt;key&gt;)</code>
      </td>
      <td style="text-align:left"><a href="../keys/">PublicKey</a>
      </td>
      <td style="text-align:left">Optional</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setWipeKey(&lt;key&gt;)</code>
      </td>
      <td style="text-align:left"><a href="../keys/">PublicKey</a>
      </td>
      <td style="text-align:left">Optional</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setSupplyKey(&lt;key&gt;)</code>
      </td>
      <td style="text-align:left"><a href="../keys/">PublicKey</a>
      </td>
      <td style="text-align:left">Optional</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setFreezeDefault(&lt;freeze&gt;</code>)</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">Optional</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setExpirationTime(&lt;expirationTime&gt;)</code>
      </td>
      <td style="text-align:left">Instant</td>
      <td style="text-align:left">
        <p>Optional</p>
        <p>(default: 90 days)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setAutoRenewAccount(&lt;account&gt;)</code>
      </td>
      <td style="text-align:left"><a href="../specialized-types.md#accountid">AccountId</a>
      </td>
      <td style="text-align:left">Optional</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setAutoRenewPeriod(&lt;period&gt;)</code>
      </td>
      <td style="text-align:left">Duration</td>
      <td style="text-align:left">
        <p>Optional</p>
        <p>(default: 131,500 minutes)</p>
      </td>
    </tr>
  </tbody>
</table>

{% tabs %}
{% tab title="Java" %}
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

//Obtain the token ID
TokenId tokenId = getReceipt.getTokenId();

System.out.println("The new token ID is " +newTokenId);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
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

//Obtain the token ID
const tokenId = getReceipt.getTokenId();

console.log("The new token ID is " +newTokenId);
//Version: 1.4.2
```
{% endtab %}
{% endtabs %}





