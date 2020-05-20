# Query

## Query

A single query, which is sent from the client to the node. This includes all possible queries. Each Query should not have more than 50 levels.

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| query | oneof |  |  |
|  | getByKey | [GetByKeyQuery](getbykey.md#getbykeyquery) | Get all entities associated with a given key |
|  | getBySolidityID | [GetBySolidityIDQuery](getbysolidityid.md#getbysolidityidquery) | Get the IDs in the format used in transactions, given the format used in Solidity |
|  | contractCallLocal | [ContractCallLocalQuery](../smart-contracts/contractcalllocal.md#contractcalllocalquery) | Call a function of a smart contract instance |
|  | contractGetInfo | [ContractGetInfoQuery](../smart-contracts/contractgetinfo.md#contractgetinfoquery) | Get information about a smart contract instance |
|  | contractGetBytecode | [ContractGetBytecodeQuery](../smart-contracts/contractgetbytecode.md#contractgetbytecodequery) | Get bytecode used by a smart contract instance |
|  | ContractGetRecords | [ContractGetRecordsQuery](../smart-contracts/contractgetrecords.md#contractgetrecordsquery) | Get Records of the contract instance |
|  | cryptogetAccountBalance | [CryptoGetAccountBalanceQuery](../cryptocurrency-accounts/cryptogetaccountbalance.md#cryptogetaccountbalancequery) | Get the current balance in a cryptocurrency account |
|  | cryptoGetAccountRecords | [CryptoGetAccountRecordsQuery](../cryptocurrency-accounts/cryptogetaccountrecords.md#cryptogetaccountrecordsquery) | Get all the records that currently exist for transactions involving an account |
|  | cryptoGetInfo | [CryptoGetInfoQuery](../cryptocurrency-accounts/cryptogetinfo.md#cryptogetinfoquery) | Get all information about an account |
|  | cryptoGetLiveHash | CryptoGetLiveHash | Get a single livehash from a single account \(or null if it doesn't exist\) |
|  | cryptoGetProxyStakers | [CryptoGetStakersQuery](../cryptocurrency-accounts/cryptogetstakers.md#cryptogetstakersquery) | Get all the accounts that proxy stake to a given account, and how much they proxy stake \(not yet implemented in the current API\) |
|  | fileGetContents | [FileGetContentsQuery](../file-service/filegetcontents.md#filegetcontentsquery) | Get the contents of a file \(the bytes stored in it\) |
|  | fileGetInfo | [FileGetInfoQuery](../file-service/filegetinfo.md#filegetinfoquery) | Get information about a file, such as its expiration date |
|  | transactionGetReceipt | [TransactionGetReceiptQuery](transactiongetreceipt.md#transactiongetreceiptquery) | Get a receipt for a transaction \(lasts 180 seconds\) |
|  | transactionGetRecord | [TransactionGetRecordQuery](transactiongetrecord.md#transactiongetrecordquery) | Get a record for a transaction \(lasts 1 hour\) |
|  | transactionGetFastRecord | [TransactionGetFastRecordQuery](transactiongetfastrecord.md#transactiongetfastrecordquery) | Get a record for a transaction \(lasts 180 seconds\) |
|  | consensusGetTopicInfo | [ConsensusGetTopicInfoQuery](../consensus-service/consensusgettopicinfo.md#consensusgettopicinfoquery) | Get the parameters of and state of a consensus topic. |
|  | networkGetVersionInfo | NetworkGetVersionInfoQuery | Get the version of the network |



