# Response

A single response, which is returned from the node to the client, after the client sent the node a query. This includes all responses.

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| response | oneof |  |  |
|  | getByKey | [GetByKeyResponse](getbykey.md#getbykeyresponse) | Get all entities associated with a given key |
|  | getBySolidityID | [GetBySolidityIDResponse](getbysolidityid.md#getbysolidityidresponse) | Get the IDs in the format used in transactions, given the format used in Solidity |
|  | contractCallLocal | [ContractCallLocalResponse](../smart-contracts/contractcalllocal.md#contractcalllocalresponse) | Response to call a function of a smart contract instance |
|  | contractGetBytecodeResponse | [ContractGetBytecodeResponse](../smart-contracts/contractgetbytecode.md#contractgetbytecoderesponse) | Get the bytecode for a smart contract instance |
|  | contractGetInfo | [ContractGetInfoResponse](../smart-contracts/contractgetinfo.md#contractgetinforesponse) | Get information about a smart contract instance |
|  | contractGetRecordsResponse | [ContractGetRecordsResponse](../smart-contracts/contractgetrecords.md#contractgetrecordsresponse) | Get all existing records for a smart contract instance |
|  | cryptogetAccountBalance | [CryptoGetAccountBalanceResponse](../cryptocurrency-accounts/cryptogetaccountbalance.md#cryptogetaccountbalanceresponse) | Get the current balance in a cryptocurrency account |
|  | cryptoGetAccountRecords | [CryptoGetAccountRecordsResponse](../cryptocurrency-accounts/cryptogetaccountrecords.md#cryptogetaccountrecordsresponse) | Get all the records that currently exist for transactions involving an account |
|  | cryptoGetInfo | [CryptoGetInfoResponse](../cryptocurrency-accounts/cryptogetinfo.md#cryptogetinforesponse) | Get all information about an account |
|  | cryptoGetLiveHash | CryptoGetLiveHash | Get a single claim from a single account \(or null if it doesn't exist\) |
|  | cryptoGetProxyStakers | [CryptoGetStakersResponse](../cryptocurrency-accounts/cryptogetstakers.md#cryptogetstakersresponse) | Get all the accounts that proxy stake to a given account, and how much they proxy stake |
|  | fileGetContents | [FileGetContentsResponse](../file-service/filegetcontents.md#filegetcontentsresponse) | Get the contents of a file \(the bytes stored in it\) |
|  | fileGetInfo | [FileGetInfoResponse](../file-service/filegetinfo.md#filegetinforesponse) | Get information about a file, such as its expiration date |
|  | transactionGetReceipt | [TransactionGetReceiptResponse](transactiongetreceipt.md#transactiongetreceiptresponse) | Get a receipt for a transaction \(lasts 180 seconds\) |
|  | transactionGetRecord | [TransactionGetRecordResponse](transactiongetrecord.md#transactiongetrecordresponse) | Get a record for a transaction \(lasts 1 hour\) |
|  | transactionGetFastRecord | [TransactionGetFastRecordResponse](transactiongetfastrecord.md#transactiongetfastrecordresponse) | Get a record for a transaction \(lasts 180 seconds\) |
|  | consensusGetTopicInfo | [ConsensusGetTopicInfoResponse](../consensus-service/consensusgettopicinfo.md#consensusgettopicinforesponse) | Parameters of and state of a consensus topic. |

