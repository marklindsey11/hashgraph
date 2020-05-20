# TransactionResponse

When the client sends the node a transaction of any kind, the node replies with this, which simply says that the transaction passed the precheck \(so the node will submit it to the network\) or it failed \(so it won't\). To learn the consensus result, the client should later obtain a receipt \(free\), or can buy a more detailed record \(not free\).

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| nodeTransactionPrecheckCode | [ResponseCodeEnum](responsecode.md#responsecodeenum) | The response code that indicates the current status of the transaction. |  |



