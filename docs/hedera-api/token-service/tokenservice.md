# TokenService

Transactions and queries for the Token Service.

## TokenService

| Method Name | Request Type | Response Type | Description |
| :--- | :--- | :--- | :--- |
| `createToken` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Creates a new Token by submitting the transaction |
| `updateToken` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Updates the account by submitting the transaction |
| `mintToken` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Mints an amount of the token to the defined treasury account |
| `burnToken` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Burns an amount of the token from the defined treasury account |
| `deleteToken` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | \(NOT CURRENTLY SUPPORTED\) Deletes a Token |
| `wipeTokenAccount` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Wipes the provided amount of tokens from the specified Account ID |
| `freezeTokenAccount` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Freezes the transfer of tokens to or from the specified Account ID |
| `unfreezeTokenAccount` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Unfreezes the transfer of tokens to or from the specified Account ID |
| `grantKycToTokenAccount` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Flags the provided Account ID as having gone through KYC |
| `revokeKycFromTokenAccount` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Removes the KYC flag of the provided Account ID |
| `transferTokens` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Initiates a Token transfer by submitting the transaction |
| `associateTokens` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Associates tokens to an account |
| `dissociateTokens` | [Transaction](../miscellaneous/transaction.md) | [TransactionResponse](../miscellaneous/transactionresponse.md) | Dissociates tokens from an account |
| `getTokenInfo` | [Query](../miscellaneous/query.md) | [Response](../miscellaneous/response.md) | Retrieves the metadata of a token |
| `getAccountNftInfo` | [Query](../miscellaneous/query.md) | [Response](../miscellaneous/response.md) | Gets info on NFTs N through M on the list of NFTs associated with a given account |
| `getTokenNftInfo` | [Query](../miscellaneous/query.md) | [Response](../miscellaneous/response.md) | Retrieves the metadata of an NFT by TokenID and serial number |
| `getTokenNftInfo` | [Query](../miscellaneous/query.md) | [Response](../miscellaneous/response.md) | Gets info on NFTs N through M on the list of NFTs associated with a given Token of type `NON_FUNGIBLE` |



