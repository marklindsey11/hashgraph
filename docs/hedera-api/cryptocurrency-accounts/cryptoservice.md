# CryptoService

| RPC | Request | Response | Comments |
| :--- | :--- | :--- | :--- |
| createAccount | Transaction | TransactionResponse | Creates a new account by submitting the transaction. The grpc server returns the TransactionResponse |
| updateAccount | Transaction | TransactionResponse | Updates an account by submitting the transaction. The grpc server returns the TransactionResponse |
| cryptoTransfer | Transaction | TransactionResponse | Initiates a transfer by submitting the transaction. The grpc server returns the TransactionResponse |
| cryptoDelete | Transaction | TransactionResponse | Deletes and account by submitting the transaction. The grpc server returns the TransactionResponse |
| addLiveHash | Transaction | TransactionResponse | \(NOT CURRENTLY SUPPORTED\) Adds a livehash |
| deleteLiveHash | Transaction | TransactionResponse | \(NOT CURRENTLY SUPPORTED\) Deletes a livehash |
| getLiveHash | Query | Response | \(NOT CURRENTLY SUPPORTED\) Retrieves a livehash for an account |
| getAccountRecords | Query | Response | Retrieves the record\(fetch by AccountID ID\) for an account by submitting the query. |
| cryptoGetBalance | Query | Response | Retrieves the balance for an account by submitting the query. |
| getAccountInfo | Query | Response | Retrieves the account information for an account by submitting the query. |
| getTransactionReceipts | Query | Response | Retrieves the transaction receipts for an account by TxId which last for 180sec only for no fee. |
| getFastTransactionRecord | Query | Response | Retrieves the transaction record by TxID which last for 180sec only for no fee. |
| getTxRecordByTxID | Query | Response | Retrieves the transactions record\(fetch by Transaction ID\) for an account by submitting the query. |
| getStakersByAccountID | Query | Response | Retrieves the stakers for a node by account ID by submitting the query. |

