# TokenFreezeAccount

Freezes transfers of the specified token for the account. Must be signed by the Token's freezeKey.

#### TokenFreezeAccountTransactionBody

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| token | TokenID | The token for which this account will be frozen. If token does not exist, transaction results in INVALID\_TOKEN\_ID |  |
| account | AccountID | The account to be frozen |  |

