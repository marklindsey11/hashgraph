# Delete a topic

`ConsensusTopicDeleteTransaction()` deletes a topic. Once a topic is deleted, the topic cannot be recovered to receive messages and all submitMessage calls will fail. Older messages can still be accessed, even after the topic is deleted, via the mirror node. If the `adminKey` was set upon the creation of the topic, the `adminKey` is required to sign to successfully delete the topic.

| Constructor | Description |
| :--- | :--- |
| `ConsensusTopicDeleteTransaction()` | Initializes the ConsensusTopicDeleteTransaction object |

```java
new ConsensusTopicDeleteTransaction()
```

## Basic

| Methods | Type | Description |
| :--- | :--- | :--- |
| `setTopicId(<topicId>)` | TopicID | The ID of the topic to be deleted |

### Example

{% tabs %}
{% tab title="Java" %}
```java
// Delete a topic that does not require an adminKey
TransactionId transactionId = new ConsensusTopicDeleteTransaction()
     .setTopicId(topicId)
     .execute(client);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
// Delete a topic that does not require an adminKey
const transactionId = await new ConsensusTopicDeleteTransaction()
     .setTopicId(topicId)
     .execute(client);
```
{% endtab %}
{% endtabs %}

