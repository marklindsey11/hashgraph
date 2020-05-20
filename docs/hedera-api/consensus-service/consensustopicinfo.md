# ConsensusTopicInfo

| Field | Type | Description |
| :--- | :--- | :--- |
| `memo` | ​Content | Short publicly visible memo about the topic. No guarantee of uniqueness. |
| `runningHash` | ​Content | When a topic is created, its running hash is initialized to 48 bytes of binary zeros. For each submitted message, the topic’s running hash is then updated to the output of a particular SHA-384 digest whose input data include the previous running hash.   See the TransactionReceipt.proto documentation for an exact description of the data included in the SHA-384 digest used for the update. |
| `sequenceNumber` | ​Content | Sequence number \(starting at 1 for the first submitMessage\) of messages on the topic. |
| `expirationTime` | ​[Timestamp](../miscellaneous/timestamp.md#timestamp)​ | Effective consensus timestamp at \(and after\) which submitMessage calls will no longer succeed on the topic and the topic will expire and after AUTORENEW\_GRACE\_PERIOD be automatically deleted. |
| `adminKey` | ​[Key](../basic-types/key.md)​ | Access control for update/delete of the topic. Null if there is no key. |
| `submitKey` | ​[Key](../basic-types/key.md)​ | Access control for ConsensusService.submitMessage. Null if there is no key. |
| `autoRenewPeriod` | ​[Duration](../miscellaneous/duration.md)​ | The duration in which to renew the topic |
| `autoRenewAccount` | ​[AccountID](../basic-types/accountid.md)​ | Null if there is no autoRenewAccount. |

