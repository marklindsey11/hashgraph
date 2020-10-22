# TokenCreate

Create a new token. After the token is created, the Token ID for it is in the receipt.

The specified Treasury Account is receiving the initial supply of tokens as-well as the tokens from the Token Mint operation once executed. The balance of the treasury account is decreased when the Token Burn operation is executed.

The supply that is going to be put in circulation is going to be the initial supply provided. The maximum supply a token can have is 2^63-1.

Example:

Token A has initial supply set to 10\_000 and decimals set to 2. The tokens that will be put into circulation are going be 100.

Token B has initial supply set to 10\_012\_345\_678 and decimals set to 8. The number of tokens that will be put into circulation are going to be 100.12345678

Creating immutable token: Token can be created as immutable if the adminKey is omitted. In this case, the name, symbol, treasury, management keys, expiry and renew properties cannot be updated. If a token is created as immutable, anyone is able to extend the expiry time by paying the fee.

## TokenCreateTransactionBody

| Field | Type | Description |
| :--- | :--- | :--- |
| name | string | The publicly visible name of the token, specified as a string of only ASCII characters |
| symbol | string | The publicly visible token symbol. It is UTF-8 capitalized alphabetical string identifying the token |
| decimals | uint32 | The number of decimal places a token is divisible by. This field can never be changed! |
| initialSupply | uint64 | Specifies the initial supply of tokens to be put in circulation. The initial supply is sent to the Treasury Account. The supply is in the lowest denomination possible. |
| treasury | [AccountID](../basic-types/accountid.md) | The account which will act as a treasury for the token. This account will receive the specified initial supply |
| adminKey | [Key](../basic-types/key.md) | The key which can perform update/delete operations on the token. If empty, the token can be perceived as immutable \(not being able to be updated/deleted\) |
| kycKey | [Key](../basic-types/key.md) | The key which can grant or revoke KYC of an account for the token's transactions. If empty, KYC is not required, and KYC grant or revoke operations are not possible. |
| freezeKey | [Key](../basic-types/key.md) | The key which can sign to freeze or unfreeze an account for token transactions. If empty, freezing is not possible |
| wipeKey | [Key](../basic-types/key.md) | The key which can wipe the token balance of an account. If empty, wipe is not possible |
| supplyKey | [Key](../basic-types/key.md) | The key which can change the supply of a token. The key is used to sign Token Mint/Burn operations |
| freezeDefault | bool | The default Freeze status \(frozen or unfrozen\) of Hedera accounts relative to this token. If true, an account must be unfrozen before it can receive the token |
| expiry | uint64 | The epoch second at which the token should expire; if an auto-renew account and period are specified, this is coerced to the current epoch second plus the autoRenewPeriod |
| autoRenewAccount | [AccountID](../basic-types/accountid.md) | An account which will be automatically charged to renew the token's expiration, at autoRenewPeriod interval |
| autoRenewPeriod | uint64 | The interval at which the auto-renew account will be charged to extend the token's expiry |

