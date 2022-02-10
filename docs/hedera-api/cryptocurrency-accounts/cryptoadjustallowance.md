# CryptoAdjustAllowance

## CryptoAdjustAllowanceTransactionBody

Modifies or creates an hbar/token allowance for a spender **relative to the payer account** of **this transaction.** (So if account 0.0.X pays for this transaction, then at consensus the spender account will have new allowances to spend hbar or tokens from 0.0.X).

If the allowance already exists, the hbar/token amount will be used to adjust the current allowance balance. If this value is negative the approved allowance will be decreased. The adjusted allowance balance cannot exceed the total supply of the token nor can it be negative.

If the allowance does not exist, it will be created with the hbar/token amount being used as the allowance balance.

**IMPORTANT**: If an allowance for the spender does not currently exist, this transaction behaves like an allowance approval.



| Field             | Type                                                          | Description                                                         |
| ----------------- | ------------------------------------------------------------- | ------------------------------------------------------------------- |
| `cryptoAllowance` | repeated [CryptoAllowance](../basic-types/cyrptoallowance.md) | List of hbar allowances approved by the account owner               |
| `nftAllowance`    | repeated [NftAllowance](../basic-types/nftallowance.md)       | List of non-fungible token allowances approved by the account owner |
| `tokenAllowance`  | repeated [TokenAllowance](../basic-types/tokenallowance.md)   | List of fungible token allowances approved by the account owner.    |
