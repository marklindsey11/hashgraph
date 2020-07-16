# Submit a message

`ConsensusMessageSubmitTransaction()` submits a message to a topic. If you are trying to submit a message to a private topic, you will need the associated `submitKey` to successfully submit messages to it.

| Constructor | Description |
| :--- | :--- |
| `ConsensusMessageSubmitTransaction()` | Initializes a ConsensusMessageSubmitTransaction object |

```java
new ConsensusMessageSubmitTransaction()
```

## Basic

<table>
  <thead>
    <tr>
      <th style="text-align:left">Methods</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>setTopicID(&lt;topic&gt;</code>
      </td>
      <td style="text-align:left">TopicID</td>
      <td style="text-align:left">The ID of the topic to submit a message to</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setMessage(&lt;message&gt;)</code>
      </td>
      <td style="text-align:left">byte[ ]</td>
      <td style="text-align:left">The message to submit in byte format. Max size of the transaction (including
        signatures) is 6144 bytes.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setMessage(&lt;message&gt;)</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">The message to submit in string format</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setMaxChunks(&lt;chunks&gt;)</code>
      </td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">
        <p>Number of transactions to break the entire message into</p>
        <p>Default Value: 10</p>
        <p>v1.2.0</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setChunkInfo(&lt;initaliId, total, number&gt;)</code>
      </td>
      <td style="text-align:left">TransactionID, int, int</td>
      <td style="text-align:left">
        <p>initialId: TransactionID of the first chunk, gets copied to every subsequent
          chunk in a fragmented message.</p>
        <p>total: total number of chunks</p>
        <p>number: The sequence number (from 1 to total) of the current chunk in
          the message.</p>
        <p>v1.2.0</p>
      </td>
    </tr>
  </tbody>
</table>

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



### Submit a message by chunks

A message that is more than 4-6kb can be sent in multiple transactions by chunking the entire message. Use `setMaxChunks()` in your transaction to designate the number of chunks you would like the message  to be broken into.  

{% tabs %}
{% tab title="Java" %}
```java
// SDK version 1.2.0
// send a message that would fit into more than one chunk (4-6k per chunk)
List<TransactionId> ids = new ConsensusMessageSubmitTransaction()
     .setMaxChunks(5) // this is 10 by default
     .setTopicId(newTopicId)
     .setMessage(bigContents.toString())
     .execute(client);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
// SDK version 1.2.0
await new ConsensusMessageSubmitTransaction()
     .setTopicId(topicId)
     .setMaxChunks(4) // default: 10
     .setMessage(bigContents)
     .execute(client); //transactionId []
```
{% endtab %}
{% endtabs %}

