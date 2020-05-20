# Submit a message

`ConsensusMessageSubmitTransaction()` submits a message to a topic. If you are trying to submit a message to a private topic, you will need the associated `submitKey` to successfully submit messages to it.

| Constructor | Description |
| :--- | :--- |
| `ConsensusMessageSubmitTransaction()` | Initializes a ConsensusMessageSubmitTransaction object |

```java
new ConsensusMessageSubmitTransaction()
```

## Basic

| Methods | Type | Description |
| :--- | :--- | :--- |
| `setTopicID(<topic>` | TopicID | The ID of the topic to submit a message to |
| `setMessage(<message>)` | byte\[ \] | The message to submit in byte format. Max size of the transaction \(including signatures\) is 6144 bytes. |
| `setMessage(<message>)` | String | The message to submit in string format |

### Example

{% tabs %}
{% tab title="Java" %}
```java
//Submits a message to a public topic 
new ConsensusMessageSubmitTransaction()
    .setTopicId(topicId)
    .setMessage("hello, HCS! " + i)
    .build(client)
    .execute(client)
    .getReceipt(client);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Submits a message to a public topic 
await new ConsensusSubmitMessageTransaction()
    .setTopicId(topicId)
    .setMessage("hello, HCS! " + i)
    .build(client)
    .execute(client)
    .getReceipt(client);
```
{% endtab %}
{% endtabs %}

## Advanced

### Submit a message to a private topic

To submit a message to a private topic, you will need access to the the `submitKey`. The `submitKey` is a property set at the time the topic is created and can be modified. If you do not have the appropriate `submitKey,` you will not be able to submit messages to that topic. 

{% tabs %}
{% tab title="Java" %}
```javascript
new ConsensusMessageSubmitTransaction()
     .setTopicId(topicId)
     .setMessage(message)
     .build(hapiClient)
     // The transaction is automatically signed by the payer.
     // Due to the topic having a submitKey requirement, additionally sign the transaction with that key.
    .sign(submitKey)
    .execute(hapiClient)
    .getReceipt(hapiClient);

```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await new ConsensusSubmitMessageTransaction()
     .setTopicId(topicId)
     .setMessage(message)
     .build(hapiClient)
     // The transaction is automatically signed by the payer.
     // Due to the topic having a submitKey requirement, additionally sign the transaction with that key.
    .sign(submitKey)
    .execute(hapiClient)
    .getReceipt(hapiClient);
```
{% endtab %}
{% endtabs %}

You can view the complete example [here](https://github.com/hashgraph/hedera-sdk-java/blob/master/examples/src/main/java/com/hedera/hashgraph/sdk/examples/ConsensusPubSubWithSubmitKey.java). 

