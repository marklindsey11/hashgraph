# TokenCreate

## TokenCreateTransactionBody

| Field | Type | Description |
| :--- | :--- | :--- |
| name |  | The publicly visible name of the token, specified as a string of only ASCII characters |
| symbol |  | The publicly visible token symbol. It is UTF-8 capitalized alphabetical string identifying the token |
| decimals |  | The number of decimal places a token is divisible by. This field can never be changed! |
| initialSupply |  | Specifies the initial supply of tokens to be put in circulation. The initial supply is sent to the Treasury Account. The supply is in the lowest denomination possible. |
| treasury | AccountID | The account which will act as a treasury for the token. This account will receive the specified initial supply |
| adminKey | Key | The key which can perform update/delete operations on the token. If empty, the token can be perceived as immutable \(not being able to be updated/deleted\) |
| kycKey | Key | The key which can grant or revoke KYC of an account for the token's transactions. If empty, KYC is not required, and KYC grant or revoke operations are not possible. |
| freezeKey | Key | The key which can sign to freeze or unfreeze an account for token transactions. If empty, freezing is not possible |
| wipeKey | Key | The key which can wipe the token balance of an account. If empty, wipe is not possible |
| supplyKey | Key | The key which can change the supply of a token. The key is used to sign Token Mint/Burn operations |
| freezeDefault |  | The default Freeze status \(frozen or unfrozen\) of Hedera accounts relative to this token. If true, an account must be unfrozen before it can receive the token |
| expiry |  | The epoch second at which the token should expire; if an auto-renew account and period are specified, this is coerced to the current epoch second plus the autoRenewPeriod |
| autoRenewAccount | AccountID | An account which will be automatically charged to renew the token's expiration, at autoRenewPeriod interval |
| autoRenewPeriod |  | The interval at which the auto-renew account will be charged to extend the token's expiry |

