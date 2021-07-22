# AssessedCustomFee

A custom transfer fee that was assessed during the handling of a CryptoTransfer.

| Field | Type | Description |
| :--- | :--- | :--- |
| amount | int64 | The number of units assessed for the fee |
| token\_id | [TokenID](../../basic-types/tokenid.md) | The denomination of the fee; taken as hbar if left unset |
| fee\_collector\_account\_id | [AccountID](../../basic-types/accountid.md) | The account to receive the assessed fee |



