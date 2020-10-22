# TokenService



#### TokenService <a id="proto.TokenService"></a>

Transactions and queries for the Token Service

| Method Name | Request Type | Response Type | Description |
| :--- | :--- | :--- | :--- |
| createToken | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Creates a new Token by submitting the transaction |
| updateToken | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Updates the account by submitting the transaction |
| mintToken | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Mints an amount of the token to the defined treasury account |
| burnToken | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Burns an amount of the token from the defined treasury account |
| deleteToken | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | \(NOT CURRENTLY SUPPORTED\) Deletes a Token |
| wipeTokenAccount | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Wipes the provided amount of tokens from the specified Account ID |
| freezeTokenAccount | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Freezes the transfer of tokens to or from the specified Account ID |
| unfreezeTokenAccount | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Unfreezes the transfer of tokens to or from the specified Account ID |
| grantKycToTokenAccount | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Flags the provided Account ID as having gone through KYC |
| revokeKycFromTokenAccount | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Removes the KYC flag of the provided Account ID |
| transferTokens | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Initiates a Token transfer by submitting the transaction |
| associateTokens | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Associates tokens to an account |
| dissociateTokens | [Transaction](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Transaction) | [TransactionResponse](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.TransactionResponse) | Dissociates tokens from an account |
| getTokenInfo | [Query](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Query) | [Response](file:///Users/simihunjan/Downloads/hedera-services-master/hapi-proto/HAPI.html#proto.Response) | Retrieves the metadata of a token |

