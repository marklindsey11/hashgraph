# TokenBurn

## TokenBurnTransactionBody

| Field | Type | Description |
| :--- | :--- | :--- |
| token | [TokenID](../basic-types/tokenid.md) | The token for which to burn tokens. If token does not exist, transaction results in INVALID\_TOKEN\_ID |
| amount |  | The amount to burn from the Treasury Account. Amount must be a positive non-zero number, not bigger than the token balance of the treasury account \(0; balance\], represented in the lowest denomination. |

