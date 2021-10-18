# TokenPause

Pauses the Token from being involved in any kind of Transaction until it is unpaused.

* Must be signed with the Token's pause key.
* If the provided token is not found, the transaction will resolve to INVALID_TOKEN_ID.
* If the provided token has been deleted, the transaction will resolve to TOKEN_WAS_DELETED.
* If no Pause Key is defined, the transaction will resolve to TOKEN_HAS_NO_PAUSE_KEY.
* Once executed the Token is marked as paused and will be not able to be a part of any transaction.

## TokenPauseTransactionBody

| Field   | Type                                 | Description            |
| ------- | ------------------------------------ | ---------------------- |
| `token` | [TokenID](../basic-types/tokenid.md) | The token to be paused |

