# CryptoTransfer

## AccountAmount

An account, and the amount that it sends or receives during a cryptocurrency transfer.

| Field | Type | Description |
| :--- | :--- | :--- |
| accountID | [AccountID](../basic-types/accountid.md) | The Account ID that sends or receives cryptocurrency |
| amount | int64 | The amount of tinybars that the account sends\(negative\) or receives\(positive\) |

## CryptoTransferTransactionBody

Transfer cryptocurrency from some accounts to other accounts. The accounts list can contain up to 10 accounts. The amounts list must be the same length as the accounts list. Each negative amount is withdrawn from the corresponding account \(a sender\), and each positive one is added to the corresponding account \(a receiver\). The amounts list must sum to zero. Each amount is a number of tinyBars \(there are 100,000,000 tinyBars in one Hbar\). If any sender account fails to have sufficient hbars to do the withdrawal, then the entire transaction fails, and none of those transfers occur, though the transaction fee is still charged. This transaction must be signed by the keys for all the sending accounts, and for any receiving accounts that have receiverSigRequired == true. The signatures are in the same order as the accounts, skipping those accounts that don't need a signature.

| Field | Type | Description |
| :--- | :--- | :--- |
| transfers | [TransferList](cryptotransfer.md#transferlist) | Accounts and amounts to transfer |

## TransferList

A list of accounts and amounts to transfer out of each account \(negative\) or into it \(positive\).

| Field | Type | Description |
| :--- | :--- | :--- |
| accountAmounts | AccountAmount | Multiple list of AccountAmount pairs, each of which has an account and an amount to transfer into it \(positive\) or out of it \(negativ |

