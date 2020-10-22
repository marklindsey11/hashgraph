# TokenAssociate

Associates the provided account with the provided tokens. Must be signed by the provided Account's key.

If the provided account is not found, the transaction will resolve to INVALID\_ACCOUNT\_ID.

If the provided account has been deleted, the transaction will resolve to ACCOUNT\_DELETED.

If any of the provided tokens is not found, the transaction will resolve to INVALID\_TOKEN\_REF.

If any of the provided tokens has been deleted, the transaction will resolve to TOKEN\_WAS\_DELETED.

If an association between the provided account and any of the tokens already exists, the transaction will resolve to TOKEN\_ALREADY\_ASSOCIATED\_TO\_ACCOUNT.

If the provided account's associations count exceed the constraint of maximum token associations per account, the transaction will resolve to TOKENS\_PER\_ACCOUNT\_LIMIT\_EXCEEDED.

On success, associations between the provided account and tokens are made and the account is ready to interact with the tokens.

## TokenAssociateTransactionBody

| Field | Type | Description |
| :--- | :--- | :--- |
| account | [AccountID](../basic-types/accountid.md) | The account to be associated with the provided tokens |
| tokens | [TokenID](../basic-types/tokenid.md) | The tokens to be associated with the provided account |



