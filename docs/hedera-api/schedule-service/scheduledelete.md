# ScheduleDelete

Deletes a Scheduled Transaction from the ledger.

The operation must be signed by the specified Admin Key of the Scheduled Transaction. If admin key is not set, Transaction will result in SCHEDULE\_IS\_IMMUTABLE.

Once deleted, sign and delete transactions will resolve to INVALID\_SCHEDULE\_ID.

## ScheduleDeleteTransactionBody

| Field | Type | Description | Signature Required |
| :--- | :--- | :--- | :--- |
| `scheduleID` | [ScheduleID](../basic-types/scheduleid.md) | The ID of the Scheduled Entity | Required |



