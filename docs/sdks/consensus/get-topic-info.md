# Get topic info

The `ConsensusTopicInfoQuery()` returns the following information about a topic:

| Info Item | Description |
| :--- | :--- |
| **topicId** | The ID of the topic |
| **adminKey** | Access control for update/delete of the topic. Null if there is no key. |
| **submitKey** | Access control for ConsensusService.submitMessage. Null if there is no key. |
| **sequenceNumber** | Current sequence number \(starting at 1 for the first submitMessage\) of messages on the topic. |
| **runningHash** | SHA-384 running hash  |
| **expirationTime** | Effective consensus timestamp at \(and after\) which submitMessage calls will no longer succeed on the topic and the topic will expire and be marked as deleted. |
| **topicMemo** | Short publicly visible memo about the topic. No guarantee of uniqueness. |
| **autoRenewPeriod** | The lifetime of the topic and the amount of time to extend the topic's lifetime by |
| **autoRenewAccoun**t | Null if there is no autoRenewAccount.  |

| Constructor | Description |
| :--- | :--- |
| `ConsensusTopicInfoQuery()` | Initializes the ConsensusTopicInfoQuery object |

```java
new ConsensusTopicInfoQuery()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setTopicId(<topicId>)` | TopicId | The ID of the topic to return information for |

### Example

{% tabs %}
{% tab title="Java" %}
```java
// Returns the current sequence numnber for the specified topic
ConsensusTopicInfo topicInfo = new ConsensusTopicInfoQuery()
    .setTopicId(topicId)
    .execute(client);
        
System.out.println(topicInfo.sequenceNumber);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const topicInfo = await new ConsensusTopicInfoQuery()
     .setTopicId(topicId)
     .execute(client);
     
console.log(`${topicInfo.sequenceNumber}`)
```
{% endtab %}
{% endtabs %}

