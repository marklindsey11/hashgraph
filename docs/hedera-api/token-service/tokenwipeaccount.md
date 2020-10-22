# TokenWipeAccount

Wipes the provided amount of tokens from the specified Account. Must be signed by the Token's Wipe key.

If the provided account is not found, the transaction will resolve to INVALID\_ACCOUNT\_ID.

If the provided account has been deleted, the transaction will resolve to ACCOUNT\_DELETED.

If the provided token is not found, the transaction will resolve to INVALID\_TOKEN\_ID.

If the provided token has been deleted, the transaction will resolve to TOKEN\_WAS\_DELETED.

If an Association between the provided token and account is not found, the transaction will resolve to TOKEN\_NOT\_ASSOCIATED\_TO\_ACCOUNT.

If Wipe Key is not present in the Token, transaction results in TOKEN\_HAS\_NO\_WIPE\_KEY.

If the provided account is the Token's Treasury Account, transaction results in CANNOT\_WIPE\_TOKEN\_TREASURY\_ACCOUNT

On success, tokens are removed from the account and the total supply of the token is decreased by the wiped amount.

The amount provided is in the lowest denomination possible. Example:

Token A has 2 decimals. In order to wipe 100 tokens from account, one must provide amount of 10000. In order to wipe 100.55 tokens, one must provide amount of 10055.

## TokenWipeAccountTransactionBody

| Field | Type | Description |
| :--- | :--- | :--- |
| token | [TokenID](../basic-types/tokenid.md) | The token for which the account will be wiped. If token does not exist, transaction results in INVALID\_TOKEN\_ID  |
| account | [AccountID](../basic-types/accountid.md) | The account to be wiped  |
| amount | uint64 | The amount of tokens to wipe from the specified account. Amount must be a positive non-zero number in the lowest denomination possible, not bigger than the token balance of the account \(0; balance\] |

