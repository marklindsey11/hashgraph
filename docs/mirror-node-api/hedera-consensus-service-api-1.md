---
description: >-
  The Hedera Consensus Service (HCS) gRPC API is a public mirror node managed by
  Hedera for the testnet. It offers the ability to subscribe to HCS topics and
  receive messages for the topic subscribed.
---

# Hedera Consensus Service gRPC API

{% hint style="info" %}
**Hedera Consensus Service Mainnet Mirror Node Access**  
To gain access to the Hedera managed mirror node for mainnet, please complete this [form](https://learn.hedera.com/hcs-mirror-api-mainnet).  
  
**HCS Mirror Node Endpoints:**  
hcs.testnet.mirrornode.hedera.com:5600   
hcs.mainnet.mirrornode.hedera.com:5600
{% endhint %}

Community supported mirror node information can be found here:

{% page-ref page="../../mainnet/nodes/mirror-nodes.md" %}

## Build a Mirror Node Client

| Constructor | Description |
| :--- | :--- |
| `MirrorClient(<endpoint>)` | Initializes the MirrorClient object |

{% tabs %}
{% tab title="Java" %}
```java
final MirrorClient mirrorClient = new MirrorClient(MIRROR_NODE_ADDRESS);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const mirrorClient = new MirrorClient(mirrorNodeAddress);
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**Concurrent Subscription Limit**  
A single client can make a maximum of **5** concurrent subscription calls per connection. 
{% endhint %}

### Subscribe to a topic

| Constructor | Description |
| :--- | :--- |
| `MirrorConsensusTopicQuery()` | Initializes the MirrorConsensusTopicQuery object |

| Method | Type | Description |
| :--- | :--- | :--- |
| `setTopicId(<topicId>)` | ConsensusTopicId | ID of the topic |
| `subscribe(<mirrorClient, onNext, onError>)` | MirrorClient, Consumer&lt;MirrorConsensusTopicResponse&gt;, Consumer&lt;Throwable&gt; | Subscribe to a topic |
| `setStartTime(<startTime>)` | Instant | The time to start receiving messages from the topic |
| `setEndTime(<endTime>)` | Instant | The time to stop receiving messages from the topic |
| `setLimit(<limit>)` | long | The limit to the number of messages to receive for that topic |

{% tabs %}
{% tab title="Java" %}
```java
new MirrorConsensusTopicQuery()
    .setTopicId(topicId)
    .subscribe(mirrorClient, resp -> {
        String messageAsString = new String(resp.message, StandardCharsets.UTF_8);

        System.out.println(resp.consensusTimestamp + " received topic message: " + messageAsString);
    },
        // On gRPC error, print the stack trace
        Throwable::printStackTrace);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
new MirrorConsensusTopicQuery()
    .setTopicId(topicId)
    .subscribe(
        consensusClient,
        (message) => console.log(message.toString()),
        (error) => console.log(`Error: ${error}`)
    );
```
{% endtab %}
{% endtabs %}

