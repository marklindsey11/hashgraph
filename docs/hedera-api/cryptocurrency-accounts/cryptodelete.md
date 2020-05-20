# CryptoDelete

## CryptoDeleteTransactionBody

Mark an account as deleted, moving all its current hbars to another account. It will remain in the ledger, marked as deleted, until it expires. Transfers into it a deleted account fail. But a deleted account can still have its expiration extended in the normal way.

| Field | Type | Description |
| :--- | :--- | :--- |
| transferAccountID | [AccountID](../basic-types/accountid.md) | The account ID which will receive all remaining hbars |
| deleteAccountID | [AccountID](../basic-types/accountid.md) | The account ID which should be deleted |

## CryptoDeleteClaim.proto

#### CryptoDeleteClaimTransactionBody

Delete a claim hash that was attached to the given account. This transaction is valid if signed by all the keys used for transfers out of the account. It is also valid if signed by any single ThresholdKeys in the deleteKeys list for this hash. See CryptoAddClaimTransaction for more information about claim hashes.

| Field | Type | Description |
| :--- | :--- | :--- |
| accountIDToDeleteFrom | [AccountID](../basic-types/accountid.md) | The account ID that should have a claim deleted |
| hashToDelete |  | The hash in the claim to delete \(a SHA-384 hash, 48 bytes\) |

