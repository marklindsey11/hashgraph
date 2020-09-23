# Queries

Queries are requests that do not require network consensus. Queries are processed only by the single node the request is sent to. Below is a list of network queries by service.

| Cryptocurrency Accounts | Consensus | File Service | Smart Contracts |
| :--- | :--- | :--- | :--- |
| [AccountBalanceQuery](cryptocurrency/get-account-balance.md) | [ConsensusTopicInfoQuery](consensus/get-topic-info.md) | [FileContentsQuery](file-storage/get-file-contents.md) | [ContractCallQuery](smart-contracts/get-smart-contract-bytecode.md) |
| [AccountInfoQuery](cryptocurrency/get-account-info.md) |  | [FileInfoQuery](file-storage/get-file-info.md) | [ContractByteCodeQuery](../hedera-api/smart-contracts/smartcontractservice.md) |
| [AccountRecordQuery](cryptocurrency/get-account-record.md) |  |  | [ContractInfoQuery](smart-contracts/get-smart-contract-info.md) |
|  |  |  | [ContractRecordQuery](smart-contracts/get-smart-contract-record.md) |

The following methods can be called when building the above queries

| Method | Type | Description |
| :--- | :--- | :--- |
| `setQueryPayment(<paymentAmount>)` | Hbar/long | Explicitly specify that the operator account is paying for the query; when the query is executed a payment transaction will be constructed with a transfer of this amount from the operator account to the node which will handle the query. |
| `setMaxQueryPayment(<paymentAmount>)` | Hbar/long | The maximum payment amount to be paid for this query. The actual payment amount may be less, but will never be greater than this value. |
| `getCost(<client>)` | Client | Returns the cost of the query prior to submitting the request |
| `execute(<client>)` | Client | Submits the transaction to the Hedera network |

