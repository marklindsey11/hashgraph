# TokenGetInfo

## TokenGetInfoQuery

Gets information about Token instance

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [QueryHeader](../miscellaneous/queryheader.md) | Standard info sent from client to node, including the signed payment, and what kind of response is requested \(cost, state proof, both, or neither\) |
| token | [TokenID](../basic-types/tokenid.md) | The token for which information is requested. If invalid token is provided, INVALID\_TOKEN\_ID response is returned. |

## TokenGetInfoResponse

Response when the client sends the node TokenGetInfoQuery

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [ResponseHeader](../miscellaneous/responseheader.md) | Standard response from node to client, including the requested fields: cost, or state proof, or both, or neither |
| tokenInfo | TokenInfo | The information requested about this token instance |

## TokenInfo

The metadata about a Token instance

| Field | Type | Description |
| :--- | :--- | :--- |
| tokenId | [TokenID](../basic-types/tokenid.md) | ID of the token instance |
| name | string | The name of the token. It is a string of ASCII only characters |
| symbol | string | The symbol of the token. It is a UTF-8 capitalized alphabetical string |
| decimals | uint32 | The number of decimal places a token is divisible by |
| totalSupply | uint64 | The total supply of tokens that are currently in circulation |
| treasury | [AccountID](../basic-types/accountid.md) | The ID of the account which is set as Treasury |
| adminKey | [Key](../basic-types/key.md) | The key which can perform update/delete operations on the token. If empty, the token can be perceived as immutable \(not being able to be updated/deleted\) |
| kycKey | [Key](../basic-types/key.md) | The key which can grant or revoke KYC of an account for the token's transactions. If empty, KYC is not required, and KYC grant or revoke operations are not possible. |
| freezeKey | [Key](../basic-types/key.md) | The key which can freeze or unfreeze an account for token transactions. If empty, freezing is not possible |
| wipeKey | [Key](../basic-types/key.md) | The key which can wipe token balance of an account. If empty, wipe is not possible |
| supplyKey | [Key](../basic-types/key.md) | The key which can change the supply of a token. The key is used to sign Token Mint/Burn operations |
| defaultFreezeStatus | [TokenFreezeStatus](../basic-types/tokenfreezestatus.md) | The default Freeze status \(not applicable, frozen or unfrozen\) of Hedera accounts relative to this token. FreezeNotApplicable is returned if Token Freeze Key is empty. Frozen is returned if Token Freeze Key is set and defaultFreeze is set to true. Unfrozen is returned if Token Freeze Key is set and defaultFreeze is set to false |
| defaultKycStatus | [TokenKycStatus](../basic-types/tokenkycstatus.md) | The default KYC status \(KycNotApplicable or Revoked\) of Hedera accounts relative to this token. KycNotApplicable is returned if KYC key is not set, otherwise Revoked |
| isDeleted | bool | Specifies whether the token was deleted or not |
| autoRenewAccount | [AccountID](../basic-types/accountid.md) | An account which will be automatically charged to renew the token's expiration, at autoRenewPeriod interval |
| autoRenewPeriod | uint64 | The interval at which the auto-renew account will be charged to extend the token's expiry |
| expiry | uint64 | The epoch second at which the token will expire; if an auto-renew account and period are specified, this is coerced to the current epoch second plus the autoRenewPeriod |



### 

