# Errors

| Error | Description |
| :--- | :--- |
| `INVALID_TOPIC_ID` | The Topic ID specified is not in the system. |
| `TOPIC_DELETED` | The Topic has been deleted |
| `INVALID_TOPIC_EXPIRATION_TIME` | ​The expiration time set for the topic is not valid |
| `INVALID_TOPIC_ADMIN_KEY` | ​The `adminKey` associated with the topic is not correct |
| `INVALID_TOPIC_SUBMIT_KEY` | ​The `submitKey` associated with the topic is not correct |
| `UNAUTHORIZED` | An attempted operation was not authorized \(ie - a deleteTopic for a topic with no `adminKey`\) |
| `INVALID_TOPIC_MESSAGE` | A `ConsensusService` message is empty |
| `INVALID_AUTORENEW_ACCOUNT` | The `autoRenewAccount` specified is not a valid, active account. |
| `AUTORENEW_ACCOUNT_NOT_ALLOWED` | An admin key was not specified on the topic, so there must not be an autorenew account. |
| `AUTORENEW_ACCOUNT_SIGNATURE_MISSING` | The `autoRenewAccount` didn't sign the transaction. |

