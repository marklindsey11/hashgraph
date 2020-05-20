# Freeze

## FreezeTransactionBody

Set the freezing period in which the platform will stop creating events and accepting transactions. This is used before safely shut down the platform for maintenance.

| Field | Description |
| :--- | :--- |
| startHour | The start hour \(in UTC time\), a value between 0 and 23 |
| startMin | The start minute \(in UTC time\), a value between 0 and 59 |
| endHour | The end hour \(in UTC time\), a value between 0 and 23 |
| endMin | The end minute \(in UTC time\), a value between 0 and 59 |

## FreezeService.proto

#### FreezeService

| RPC | Request | Response | Comments |
| :--- | :--- | :--- | :--- |
| freeze | Transaction | TransactionResponse | Freezes the nodes by submitting the transaction. The grpc server returns the TransactionResponse |

