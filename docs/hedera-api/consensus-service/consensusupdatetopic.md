# ConsensusUpdateTopic

All fields left null will not be updated.

## ConsensusUpdateTopicTransactionBody

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| `topicID` | [TopicID](../basic-types/topicid.md) |  |  |
| `memo` | google.protobuf.StringValue | Short publicly visible memo about the topic. No guarantee of uniqueness. Null for "do not update". |  |
| `expirationTime` | [Timestamp](../miscellaneous/timestamp.md#timestamp) | Effective consensus timestamp at \(and after\) which all consensus transactions and queries will fail. The expirationTime may be no longer than MAX\_AUTORENEW\_PERIOD \(8000001 seconds\) from the consensus timestamp of this transaction. On topics with no adminKey, extending the expirationTime is the only updateTopic option allowed on the topic. If unspecified, no change. |  |
| `adminKey` | [Key](../basic-types/key.md) | Access control for update/delete of the topic. If unspecified, no change. If empty keyList - the adminKey is cleared. |  |
| `submitKey` | [Key](../basic-types/key.md) | Access control for ConsensusService.submitMessage. If unspecified, no change. If empty keyList - the submitKey is cleared. |  |
| `autoRenewPeriod` | [Duration](../miscellaneous/duration.md) | The amount of time to extend the topic's lifetime automatically at expirationTime if the autoRenewAccount is configured and has funds \(once autoRenew functionality is supported by HAPI\). Limited to between MIN\_AUTORENEW\_PERIOD \(6999999 seconds\) and MAX\_AUTORENEW\_PERIOD \(8000001 seconds\) by servers-side configuration \(which may change\). If unspecified, no change. |  |
| autoRenewAccount | [AccountID](../basic-types/accountid.md) | Optional account to be used at the topic's expirationTime to extend the life of the topic. Once autoRenew functionality is supported by HAPI, the topic lifetime will be extended up to a maximum of the autoRenewPeriod or however long the topic can be extended using all funds on the account \(whichever is the smaller duration/amount\). If specified as the default value \(0.0.0\), the autoRenewAccount will be removed. If unspecified, no change. |  |

