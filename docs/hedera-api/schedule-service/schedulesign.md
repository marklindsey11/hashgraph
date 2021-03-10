# ScheduleSign

Provides signatures for a given Scheduled Transaction. The Scheduled Transaction executes if all of the required signatures are witnessed.

INVALID\_SCHEDULE\_ID is returned if the specified ScheduleID does not exist; or has now expired, been deleted, or been executed.

UNRESOLVABLE\_REQUIRED\_SIGNERS is returned if any of the required keys were updated/deleted and cannot be resolved.

INVALID\_ACCOUNT\_ID is returned if the payerAccountID has been deleted or cannot be resolved.

NO\_NEW\_VALID\_SIGNATURES is returned if there are no new signatures provided in the sigMap to be witnessed.

SOME\_SIGNATURES\_WERE\_INVALID is returned if one of the signatures provided does not represent a valid signature for any required signer.

## ScheduleSignTransactionBody

| Field | Type | Description | Signature Required |
| :--- | :--- | :--- | :--- |
| `scheduleID` | [ScheduleID](../basic-types/scheduleid.md) | The ID of the Scheduled Entity | Required |
| `sigMap` | [SignatureMap](../basic-types/signaturemap.md) | The signature map containing the signature\(s\) to authorise the transaction | Required |

