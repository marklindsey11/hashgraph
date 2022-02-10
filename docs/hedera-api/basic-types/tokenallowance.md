# TokenAllowance

An approved allowance of token transfers for a spender.

| Field            | Type      | Description                                                                                                          |
| ---------------- | --------- | -------------------------------------------------------------------------------------------------------------------- |
| `TokenId`        |           |                                                                                                                      |
| `owner`          | AccountID | The account ID of the hbar owner (ie. the grantor of the allowance)                                                  |
| `spender`        | AccountID | The account ID of the spender of the hbar allowance                                                                  |
| `amount`         | int64     | The amount of the spender's token allowance                                                                          |
| `decimals`       | int32     | The number of decimal places the token allowance value is divisible by                                               |
| `approvedForAll` | boolean   | If true, the spender has access to all of the account owner's NFT instances (currently owned and any in the future). |

####
