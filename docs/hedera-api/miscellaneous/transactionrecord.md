# TransactionRecord

## TransactionRecord

Response when the client sends the node TransactionGetRecordResponse

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| receipt | [TransactionReceipt](transactionreceipt.md#transactionreceipt) | The status \(reach consensus, or failed, or is unknown\) and the ID of any new account/file/instance created. |  |
| transactionHash |  | The hash of the Transaction that executed \(not the hash of any Transaction that failed for having a duplicate TransactionID\) |  |
| consensusTimestamp | [Timestamp](timestamp.md#timestamp) | The consensus timestamp \(or null if didn't reach consensus yet\) |  |
| transactionID | [TransactionID](../basic-types/transactionid.md) | The ID of the transaction this record represents |  |
| memo |  | The memo that was submitted as part of the transaction \(max 100 bytes\) |  |
| transactionFee |  | The actual transaction fee charged, not the original transactionFee value from TransactionBody |  |
| body | oneof |  |  |
|  | contractCallResult | ContractFunctionResult | Record of the value returned by the smart contract function \(if it completed and didn't fail\) from ContractCallTransaction |
|  | contractCreateResult | ContractFunctionResult | Record of the value returned by the smart contract constructor \(if it completed and didn't fail\) from ContractCreateTransaction |
| transferList | [TransferList](../cryptocurrency-accounts/cryptotransfer.md#transferlist) | All hbar transfers as a result of this transaction, such as fees, or transfers performed by the transaction, or by a smart contract it calls, or by the creation of threshold records that it triggers. |  |

