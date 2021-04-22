# Network Response Messages

| Network Response | Description |
| :--- | :--- |
| `INVALID_SCHEDULE_ID` | The Scheduled entity does not exist; or has now expired, been deleted, or been executed |
| `SCHEDULE_IS_IMMUTABLE` | The Scheduled entity cannot be modified. Admin key was not set during the creation of the Scheduled entity.  |
| `INVALID_SCHEDULE_PAYER_ID` | The provided Scheduled Payer does not exist |
| `INVALID_SCHEDULE_ACCOUNT_ID` | The Schedule Create Transaction TransactionID account does not exist |
| `NO_NEW_VALID_SIGNATURES` | The provided sig map did not contain any new valid signatures from required signers of the scheduled transaction |
| `UNRESOLVABLE_REQUIRED_SIGNERS` | The required signers for a scheduled transaction cannot be resolved, for example because they do not exist or have been deleted |
| `UNPARSEABLE_SCHEDULED_TRANSACTION` | The bytes allegedly representing a transaction to be scheduled could not be parsed |
| `UNSCHEDULABLE_TRANSACTION` | ScheduleCreate and ScheduleSign transactions cannot be scheduled |
| `SOME_SIGNATURES_WERE_INVALID` | At least one of the signatures in the provided sig map did not represent a valid signature for any required signer |
| `TRANSACTION_ID_FIELD_NOT_ALLOWED` | The scheduled and nonce fields in the TransactionID may not be set in a top-level transaction |
| `IDENTICAL_SCHEDULE_ALREADY_CREATED` | A schedule already exists with the same identifying fields of an attempted ScheduleCreate \(that is, all fields other than scheduledPayerAccountID\) |
| `SCHEDULE_ALREADY_DELETED` | A schedule being signed or deleted has already been deleted |

