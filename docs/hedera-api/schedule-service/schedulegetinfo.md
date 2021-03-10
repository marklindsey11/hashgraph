# ScheduleGetInfo

Gets information about Scheduled Transaction instance. Answered with status INVALID\_SCHEDULE\_ID if the Scheduled Transaction is deleted, expires or is executed.

## ScheduleGetInfoQuery

| Field | Type | Description |
| :--- | :--- | :--- |
| `header` | ​[QueryHeader](../miscellaneous/queryheader.md)​ | Standard info sent from client to node, including the signed payment, and what kind of response is requested \(cost, state proof, both, or neither\). |
| `scheduleID` | ​[ScheduleID](../basic-types/scheduleid.md) | The ID of the Scheduled Entity |

## ScheduleInfo

Metadata about a Scheduled Transaction instance.

| Field | Type | Description |
| :--- | :--- | :--- |
| `scheduleID` | [ScheduleID](../basic-types/scheduleid.md) | The ID of the Scheduled Entity |
| `creatorAccountID` | [AccountID](../basic-types/accountid.md) | The Account ID which created the scheduled transaction |
| `payerAccountIDAccountID` | [AccountID](../basic-types/accountid.md) | The account which is going to pay for the execution of the scheduled transaction |
| `transactionBody` | bytes | The transaction serialized into bytes that must be signed |
| `signatories` | [KeyList](../basic-types/keylist.md) | The signatories that have provided signatures so far for the scheduled transaction |
| `adminKey` | [Key](../basic-types/key.md) | The Key which is able to delete the Scheduled Transaction if set |
| `memo` | string | Publicly visible information about the Scheduled entity, up to 100 bytes. No guarantee of uniqueness. |
| `expirationTime` | [TimeStamp](../miscellaneous/timestamp.md#timestamp) | The epoch second at which the schedule will expire |

‌

## ScheduleGetInfoResponse <a id="consensusgettopicinforesponse"></a>

Response that gets returned, when the client sends the node a ScheduleGetInfoQuery

| Field | Type | Description |
| :--- | :--- | :--- |
| `header` | ​[ResponseHeader](../miscellaneous/responseheader.md#responseheader)​ | Standard response from node to client, including the requested fields: cost, or state proof, or both, or neither. |
| `scheduleInfo` | [ScheduleInfo](schedulegetinfo.md#scheduleinfo) | Current state of the topic |

