# Get topic messages

Subscribe to a topic ID's messages from a mirror node. You will recieve all messages for the specified topic or within the defined start and end time.

{% tabs %}
{% tab title="V2" %}
| Constructor | Description |
| :--- | :--- |
| `new TopicMessageQuery()` | Initializes the TopicMessageQuery object |

```java
new TopicMessageQuery()
```

### Methods

| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTopicId` | TopicId | The topic ID to subsribe to | Required |
| `setStartTime` | Instant | The time to start subscribing to a topic's messages | Optional |
| `setEndTime` | Instant | The time to stop subscribing to a topic's messages | Optional |
| `setLimit` | long | The number of messages to return | Optional |
| `subscribe(<client, onNext)` | SubscriptionHandle | Client, Consumer&lt;TopicMessage&gt; | Required |

{% code title="Java" %}
```java
new TopicMessageQuery()
    .setTopicId(newTopicId)
    .subscribe(client, topicMessage -> {
        System.out.println("at " + topicMessage.consensusTimestamp + " ( seq = " + topicMessage.sequenceNumber + " ) received topic message of " + topicMessage.contents.length + " bytes");
    });

//v2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
new TopicMessageQuery()
        .setTopicId(topicId)
        .setStartTime(0)
        .subscribe(
            client,
            (message) => console.log(Buffer.from(message.contents, "utf8").toString())
        );
//v2.0.0
```
{% endcode %}

{% code title="Go" %}
```java
_, err = hedera.NewTopicMessageQuery().
	SetTopicID(topicID).
	Subscribe(client, func(message hedera.TopicMessage) {
		if string(message.Contents) == content {
		wait = false
	}
})

if err != nil {
	panic(err)
}

//v2.0.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}


| Constructor | Description |
| :--- | :--- |
| `new MirrorConsensusTopicQuery()` | Initializes the MirrorConsensusTopicQuery object |

```java
new MirrorConsensusTopicQuery()
```

### Methods

| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTopicId` | TopicId | The topic ID to subsribe to | Required |
| `setStartTime` | Instant | The time to start subscribing to a topic's messages | Optional |
| `setEndTime` | Instant | The time to stop subscribing to a topic's messages | Optional |
| `setLimit` | long | The number of messages to return | Optional |
| `subscribe(<mirrorClient, onNext onError)` | MirrorClient, Consumer &lt;MirrorConsensusTopicResponse&gt;, Consumer&lt;Throwable&gt; | Subscribe and get the  messages for a topic | Required |

{% code title="Java" %}
```java
new MirrorConsensusTopicQuery()
    .setTopicId(topicId)
    .subscribe(mirrorClient, resp -> {
                String messageAsString = new String(resp.message, StandardCharsets.UTF_8);

                System.out.println(resp.consensusTimestamp + " received topic message: " + messageAsString);
            },
            // On gRPC error, print the stack trace
            Throwable::printStackTrace);
//v1.3.2
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
new MirrorConsensusTopicQuery()
    .setTopicId(topicId)
    .subscribe(
        consensusClient,
        (message) => console.log(message.toString()),
        (error) => console.log(`Error: ${error}`)
    );
```
{% endcode %}
{% endtab %}
{% endtabs %}

## 

