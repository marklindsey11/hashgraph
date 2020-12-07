---
description: >-
  The Hedera Consensus Service (HCS) gRPC API is a public mirror node managed by
  Hedera for the testnet. It offers the ability to subscribe to HCS topics and
  receive messages for the topic subscribed.
---

# Hedera Consensus Service gRPC API

{% hint style="info" %}
**HCS Mirror Node Endpoints:**  
hcs.testnet.mirrornode.hedera.com:5600   
hcs.mainnet.mirrornode.hedera.com:5600
{% endhint %}

Community supported mirror node information can be found here:

{% page-ref page="../../mirrornet/community-mirror-nodes.md" %}

## Build a Mirror Node Client

{% tabs %}
{% tab title="V2" %}
If you building your client with a predefined Hedera network \(previewnet, testnet, mainnet\), you do not need to define the mirror client as it is built in. If you would like to modify the mirror client, you can use [`Client.<network>.setMirrorNetwork(network)`](https://docs.hedera.com/guides/docs/sdks/client#1-configure-your-hedera-network).
{% endtab %}

{% tab title="V1" %}


| Constructor | Description |
| :--- | :--- |
| `new MirrorClient(<endpoint>)` | Initializes the MirrorClient object |

{% code title="Java" %}
```java
final MirrorClient mirrorClient = new MirrorClient(MIRROR_NODE_ADDRESS);
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
const mirrorClient = new MirrorClient(mirrorNodeAddress);
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**Concurrent Subscription Limit**  
A single client can make a maximum of **5** concurrent subscription calls per connection. 
{% endhint %}

### Subscribe to a topic

Please click the link below to see how you can subscribe to a topic.

{% page-ref page="../sdks/consensus/get-topic-message.md" %}





