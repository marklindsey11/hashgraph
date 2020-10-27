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
      <td style="text-align:left">TokenId</td>
      <td style="text-align:left">ID of the token instance</td>
    </tr>
    <tr>
      <td style="text-align:left">Name</td>
      <td style="text-align:left">The name of the token. It is a string of ASCII only characters</td>
    </tr>
    <tr>
      <td style="text-align:left">Symbol</td>
      <td style="text-align:left">The symbol of the token. It is a UTF-8 capitalized alphabetical string</td>
    </tr>
    <tr>
      <td style="text-align:left">Decimals</td>
      <td style="text-align:left">The number of decimal places a token is divisible by</td>
    </tr>
    <tr>
      <td style="text-align:left">Total Supply</td>
      <td style="text-align:left">The total supply of tokens that are currently in circulation</td>
    </tr>
    <tr>
      <td style="text-align:left">Treasury</td>
      <td style="text-align:left">The ID of the account which is set as Treasury</td>
    </tr>
    <tr>
      <td style="text-align:left">Admin Key</td>
      <td style="text-align:left">The key which can perform update/delete operations on the token. If empty,
        the token can be perceived as immutable (not being able to be updated/deleted)</td>
    </tr>
    <tr>
      <td style="text-align:left">KYC Key</td>
      <td style="text-align:left">The key which can grant or revoke KYC of an account for the token&apos;s
        transactions. If empty, KYC is not required, and KYC grant or revoke operations
        are not possible.</td>
    </tr>
    <tr>
      <td style="text-align:left">Freeze Key</td>
      <td style="text-align:left">The key which can freeze or unfreeze an account for token transactions.
        If empty, freezing is not possible</td>
    </tr>
    <tr>
      <td style="text-align:left">Wipe Key</td>
      <td style="text-align:left">The key which can wipe token balance of an account. If empty, wipe is
        not possible</td>
    </tr>
    <tr>
      <td style="text-align:left">Supply Key</td>
      <td style="text-align:left">The key which can change the supply of a token. The key is used to sign
        Token Mint/Burn operations</td>
    </tr>
    <tr>
      <td style="text-align:left">Default Freeze Status</td>
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
      <td style="text-align:left">Default KYC Status</td>
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
      <td style="text-align:left">Auto Renew Account</td>
      <td style="text-align:left">An account which will be automatically charged to renew the token&apos;s
        expiration, at autoRenewPeriod interval</td>
    </tr>
    <tr>
      <td style="text-align:left">Auto Renew Period</td>
      <td style="text-align:left">The interval at which the auto-renew account will be charged to extend
        the token&apos;s expiry</td>
    </tr>
    <tr>
      <td style="text-align:left">Expiry</td>
      <td style="text-align:left">The epoch second at which the token will expire; if an auto-renew account
        and period are specified, this is coerced to the current epoch second plus
        the autoRenewPeriod</td>
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

| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | [TokenId](token-id.md) | Required |
| `<TokenInfoQuery>.tokenId` | [TokenId](token-id.md) | Optional |
| `<TokenInfoQuery>.name` | String | Optional |
| `<TokenInfoQuery>.symbol` | String | Optional |
| `<TokenInfoQuery>.decimals` | int | Optional |
| `<TokenInfoQuery>.totalSupply` | long | Optional |
| `<TokenInfoQuery>.treasury` | [AccountId](../specialized-types.md#accountid) | Optional |
| `<TokenInfoQuery>.adminKey` | [PublicKey](../keys.md) | Optional |
| `<TokenInfoQuery>.kycKey` | [PublicKey](../keys.md) | Optional |
| `<TokenInfoQuery>.freezeKey` | [PublicKey](../keys.md) | Optional |
| `<TokenInfoQuery>.wipeKey` | [PublicKey](../keys.md) | Optional |
| `<TokenInfoQuery>.supplyKey` | [PublicKey](../keys.md) | Optional |
| `<TokenInfoQuery>.defaultFreezeStatus` | Boolean | Optional |
| `<TokenInfoQuery>.defaultKycStatus` | Boolean | Optional |
| `<TokenInfoQuery>.isDeleted` | Boolean | Optional |
| `<TokenInfoQuery>.autoRenewAccount` | [AccountId](../specialized-types.md#accountid) | Optional |
| `<TokenInfoQuery>.autoRenewPeriod` | Duration | Optional |
| `<TokenInfoQuery>.expiry` | Instant | Optional |

{% tabs %}
{% tab title="Java" %}
```java
TokenInfoQuery tokenInfo = new TokenInfoQuery()
    .setTokenId(newTokenId);

//Submit the query to the network and obtain the token supply
long totalSupply = tokenInfo.execute(client).totalSupply;
System.out.println("The total supply of this token is " +totalSupply)
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const tokenInfo = await new TokenInfoQuery()
    .setTokenId(newTokenId);

const totalSupply = await tokenInfo.execute(client).totalSupply;
console.log("The total supply of this token is " +totalSupply)
//Version 1.4.3
```
{% endtab %}
{% endtabs %}





