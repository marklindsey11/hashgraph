# Get token info

Gets information about a token instance. The token info query returns the following information:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>TokenId</b>
      </td>
      <td style="text-align:left">ID of the token instance</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Name</b>
      </td>
      <td style="text-align:left">The name of the token. It is a string of ASCII only characters</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Symbol</b>
      </td>
      <td style="text-align:left">The symbol of the token. It is a UTF-8 capitalized alphabetical string</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Decimals</b>
      </td>
      <td style="text-align:left">The number of decimal places a token is divisible by</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Total Supply</b>
      </td>
      <td style="text-align:left">The total supply of tokens that are currently in circulation</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Treasury</b>
      </td>
      <td style="text-align:left">The ID of the account which is set as Treasury</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Admin Key</b>
      </td>
      <td style="text-align:left">The key which can perform update/delete operations on the token. If empty,
        the token can be perceived as immutable (not being able to be updated/deleted)</td>
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
      <td style="text-align:left">The key which can freeze or unfreeze an account for token transactions.
        If empty, freezing is not possible</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Wipe Key</b>
      </td>
      <td style="text-align:left">The key which can wipe token balance of an account. If empty, wipe is
        not possible</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Supply Key</b>
      </td>
      <td style="text-align:left">The key which can change the supply of a token. The key is used to sign
        Token Mint/Burn operations</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Default Freeze Status</b>
      </td>
      <td style="text-align:left">
        <p>The default Freeze status (not applicable = null, frozen = false, or unfrozen
          = true) of Hedera accounts relative to this token.<b> </b>FreezeNotApplicable
          is returned if Token Freeze Key is empty. Frozen is returned if Token Freeze
          Key is set and defaultFreeze is set to true. Unfrozen is returned if Token
          Freeze Key is set and defaultFreeze is set to false.</p>
        <p>FreezeNotApplicable = null;</p>
        <p>Frozen = false;</p>
        <p>Unfrozen = true;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Default KYC Status</b>
      </td>
      <td style="text-align:left">
        <p>The default KYC status (KycNotApplicable or Revoked) of Hedera accounts
          relative to this token. KycNotApplicable is returned if KYC key is not
          set, otherwise Revoked.</p>
        <p>KycNotApplicable = null;</p>
        <p>Granted = false;</p>
        <p>Revoked = true;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Auto Renew Account</b>
      </td>
      <td style="text-align:left">An account which will be automatically charged to renew the token&apos;s
        expiration, at autoRenewPeriod interval</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Auto Renew Period</b>
      </td>
      <td style="text-align:left">The interval at which the auto-renew account will be charged to extend
        the token&apos;s expiry</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Expiry</b>
      </td>
      <td style="text-align:left">The epoch second at which the token will expire; if an auto-renew account
        and period are specified, this is coerced to the current epoch second plus
        the autoRenewPeriod</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Memo</b>
      </td>
      <td style="text-align:left">Short publicly visible memo about the token, if any</td>
    </tr>
  </tbody>
</table>

| Constructor | Description |
| :--- | :--- |
| `new TokenInfoQuery()` | Initializes the TokenInfoQuery object |

```java
new TokenInfoQuery()
```

### Methods

{% tabs %}
{% tab title="V2" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | Required |
| `<TokenInfoQuery>.tokenId` | TokenId | Optional |
| `<TokenInfoQuery>.name` | String | Optional |
| `<TokenInfoQuery>.symbol` | String | Optional |
| `<TokenInfoQuery>.decimals` | int | Optional |
| `<TokenInfoQuery>.totalSupply` | long | Optional |
| `<TokenInfoQuery>.treasury` | AccountId | Optional |
| `<TokenInfoQuery>.adminKey` | PublicKey | Optional |
| `<TokenInfoQuery>.kycKey` | PublicKey | Optional |
| `<TokenInfoQuery>.freezeKey` | PublicKey | Optional |
| `<TokenInfoQuery>.wipeKey` | PublicKey | Optional |
| `<TokenInfoQuery>.supplyKey` | PublicKey | Optional |
| `<TokenInfoQuery>.defaultFreezeStatus` | Boolean | Optional |
| `<TokenInfoQuery>.defaultKycStatus` | Boolean | Optional |
| `<TokenInfoQuery>.isDeleted` | Boolean | Optional |
| `<TokenInfoQuery>.autoRenewAccount` | AccountId | Optional |
| `<TokenInfoQuery>.autoRenewPeriod` | Duration | Optional |
| `<TokenInfoQuery>.expiry` | Instant | Optional |

{% code title="Java" %}
```java
//Create the query
TokenInfoQuery query = new TokenInfoQuery()
    .setTokenId(newTokenId);

//Sign with the client operator private key, submit the query to the network and get the token supply
long tokenSupply = query.execute(client).totalSupply;

System.out.println("The token info is " +tokenSupply);

```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create the query
const query = new TokenInfoQuery()
    .setTokenId(newTokenId);

//Sign with the client operator private key, submit the query to the network and get the token supply
const tokenSupply = await query.execute(client).totalSupply;

console.log("The total supply of this token is " +tokenSupply);

//v2.0.7
```
{% endcode %}

{% code title="Go" %}
```go
//Create the query (issue logged)
query := hedera.NewTokenInfoQuery().
		SetTokenID(tokenId)

//Sign with the client operator private key and submit to a Hedera network
tokenInfo, err := query.Execute(client)

if err != nil {
		panic(err)
}

fmt.Printf("The token info is %v\n", tokenIinfo)

//v2.1.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | Required |
| `<TokenInfoQuery>.tokenId` | TokenId | Optional |
| `<TokenInfoQuery>.name` | String | Optional |
| `<TokenInfoQuery>.symbol` | String | Optional |
| `<TokenInfoQuery>.decimals` | int | Optional |
| `<TokenInfoQuery>.totalSupply` | long | Optional |
| `<TokenInfoQuery>.treasury` | AccountId | Optional |
| `<TokenInfoQuery>.adminKey` | PublicKey | Optional |
| `<TokenInfoQuery>.kycKey` | PublicKey | Optional |
| `<TokenInfoQuery>.freezeKey` | PublicKey | Optional |
| `<TokenInfoQuery>.wipeKey` | PublicKey | Optional |
| `<TokenInfoQuery>.supplyKey` | PublicKey | Optional |
| `<TokenInfoQuery>.defaultFreezeStatus` | Boolean | Optional |
| `<TokenInfoQuery>.defaultKycStatus` | Boolean | Optional |
| `<TokenInfoQuery>.isDeleted` | Boolean | Optional |
| `<TokenInfoQuery>.autoRenewAccount` | AccountId | Optional |
| `<TokenInfoQuery>.autoRenewPeriod` | Duration | Optional |
| `<TokenInfoQuery>.expiry` | Instant | Optional |

{% code title="Java" %}
```java
//Create the query
TokenInfoQuery tokenInfo = new TokenInfoQuery()
    .setTokenId(newTokenId);

//Submit the query to the network and obtain the token supply
long totalSupply = tokenInfo.execute(client).totalSupply;
System.out.println("The total supply of this token is " +totalSupply)
//Version: 1.2.2
```
{% endcode %}

{% code title="JavaScript \(Not working\)" %}
```javascript
//Create the query
const tokenInfo = new TokenInfoQuery()
    .setTokenId(newTokenId);

//Submit the query to the network and obtain the token supply
const totalSupply = await tokenInfo.execute(client).totalSupply;

console.log("The total supply of this token is " +totalSupply)

//Version 1.4.3
```
{% endcode %}
{% endtab %}
{% endtabs %}

