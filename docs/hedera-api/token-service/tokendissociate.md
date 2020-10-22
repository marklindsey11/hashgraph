# TokenDissociate

Dissociates the provided account with the provided tokens. Must be signed by the provided Account's key.

If the provided account is not found, the transaction will resolve to INVALID\_ACCOUNT\_ID.

If the provided account has been deleted, the transaction will resolve to ACCOUNT\_DELETED.

If any of the provided tokens is not found, the transaction will resolve to INVALID\_TOKEN\_REF.

If any of the provided tokens has been deleted, the transaction will resolve to TOKEN\_WAS\_DELETED.

If an association between the provided account and any of the tokens does not exist, the transaction will resolve to TOKEN\_NOT\_ASSOCIATED\_TO\_ACCOUNT.

If the provided account has a nonzero balance with any of the provided tokens, the transaction will resolve to TRANSACTION\_REQUIRES\_ZERO\_TOKEN\_BALANCES.

## TokenDeleteTransactionBody

| Field | Type | Description |
| :--- | :--- | :--- |
| token | [TokenID](../basic-types/tokenid.md) | The token to be deleted. If invalid token is specified, transaction will result in INVALID\_TOKEN\_ID |

