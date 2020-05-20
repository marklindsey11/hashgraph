# TransactionGetRecord

## TransactionGetRecordQuery

Get the record for a transaction. If the transaction requested a record, then the record lasts for one hour, and a state proof is available for it. If the transaction created an account, file, or smart contract instance, then the record will contain the ID for what it created. If the transaction called a smart contract function, then the record contains the result of that call. If the transaction was a cryptocurrency transfer, then the record includes the TransferList which gives the details of that transfer. If the transaction didn't return anything that should be in the record, then the results field will be set to nothing.

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| header | [QueryHeader](queryheader.md) | Standard info sent from client to node, including the signed payment, and what kind of response is requested \(cost, state proof, both, or neither\). |  |
| transactionID | [TransactionID](../basic-types/transactionid.md) | The ID of the transaction for which the record is requested. |  |

## TransactionGetRecordResponse

Response when the client sends the node TransactionGetRecordQuery

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| header | [ResponseHeader](responseheader.md#responseheader) | Standard response from node to client, including the requested fields: cost, or state proof, or both, or neither. |  |
| transactionRecord | [TransactionRecord](transactionrecord.md) | The requested record |  |



