# TokenMint

Mints tokens to the Token's treasury Account. If no Supply Key is defined, the transaction will resolve to TOKEN\_HAS\_NO\_SUPPLY\_KEY.

The operation increases the Total Supply of the Token. The maximum total supply a token can have is 2^63-1.

The amount provided must be in the lowest denomination possible. Example:

Token A has 2 decimals. In order to mint 100 tokens, one must provide amount of 10000. In order to mint 100.55 tokens, one must provide amount of 10055.

## TokenMintTransactionBody

| Field | Type | Description |
| :--- | :--- | :--- |
| token | [TokenID](../basic-types/tokenid.md) | The token for which to mint tokens. If token does not exist, transaction results in INVALID\_TOKEN\_ID  |
| amount | uint64 | The amount to mint to the Treasury Account. Amount must be a positive non-zero number represented in the lowest denomination of the token. The new supply must be lower than 2^63.  |

