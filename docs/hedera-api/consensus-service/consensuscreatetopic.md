# ConsensusCreateTopic

## ConsensusCreateTopicTransactionBody

| Field | Type | Description |
| :--- | :--- | :--- |
| `memo` |  | Short publicly visible memo about the topic. No guarantee of uniqueness. |
| `adminKey` | [Key](../basic-types/key.md) | Access control for updateTopic/deleteTopic. Anyone can increase the topic's expirationTime via ConsensusService.updateTopic\(\), regardless of the adminKey. If no adminKey is specified, updateTopic may only be used to extend the topic's expirationTime, and deleteTopic is disallowed. |
| `submitKey` | [Key](../basic-types/key.md) | Access control for submitMessage. If unspecified, no access control is performed on ConsensusService.submitMessage \(all submissions are allowed\). |
| `autoRenewPeriod` | [Duration](../miscellaneous/duration.md) | The initial lifetime of the topic and the amount of time to attempt to extend the topic's lifetime by automatically at the topic's expirationTime, if the autoRenewAccount is configured \(once autoRenew functionality is supported by HAPI\). Limited to MIN\_AUTORENEW\_PERIOD and MAX\_AUTORENEW\_PERIOD value by server-side configuration. Required. |
| `autoRenewAccount` | [AccountID](../basic-types/accountid.md) | Optional account to be used at the topic's expirationTime to extend the life of the topic \(once autoRenew functionality is supported by HAPI\). The topic lifetime will be extended up to a maximum of the autoRenewPeriod or however long the topic can be extended using all funds on the account \(whichever is the smaller duration/amount and if any extension is possible with the account's funds\). If specified, there must be an adminKey and the autoRenewAccount must sign this transaction. |

