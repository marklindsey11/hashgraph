# Create a topic

`ConsensusTopicCreateTransaction()` creates a new topic recognized by the Hedera network. The newly generated topic can be referenced by its `topicId`. The `topicId` is used to identify a specific topic to submit messages to. All messages within a topic are sequenced with respect to one another and are provided sequence number.

You can also create a private topic where only authorized parties can submit messages to that topic. To create a private topic you would need to set the `submitKey` property of the transaction. The `submitKey` value is then shared with the authorized parties and is required to successfully submit messages to the private topic. 

| Constructor | Description |
| :--- | :--- |
| `ConsensusTopicCreateTransaction()` | Initializes the ConsensusTopicCreateTransaction object |

```java
new ConsensusTopicCreateTransaction()
```



### Example

{% tabs %}
{% tab title="Java" %}
```java
 final TransactionId transactionId = new ConsensusTopicCreateTransaction()
     .execute(client);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const transactionId = await new ConsensusTopicCreateTransaction()
    .execute(client);
```
{% endtab %}
{% endtabs %}

## Advanced

The `adminKey` and `submitKey` on the topic can be any of the following key structures:

* **Simple Key**: one key has the authority to modify the topic \(`adminKey)` or to submit a message to that topic \(`submitKey`\)
* **Key List**: A list of keys that are all required to sign transactions to modify the properties of a  topic \(`adminKey)` or to submit a message to that topic  \(`submitKey`\)
* **Threshold Keys**: Requires a minimum of x number of signatures from a total of y signatures to modify the properties of a topic \(`adminKey)` or to submit a message to that topic  \(`submitKey`\)

| Method | Type | Description |
| :--- | :--- | :--- |
| `setAdminKey(<key>)` | PublicKey | The key that has the ability to update or delete the topic. `expirationTime` can be modified by anyone. If no `adminKey` is specified, `updateTopic` may only be used to extend the `expirationTime`, and `deleteTopic` is disallowed. |
| `setSubmitKey(<key>)` | PublicKey | Access control for `submitMessage`. If this property is not set, no access control is performed on `ConsensusService.submitMessage` \(all submissions allowed\).  |
| `setTopicMemo(<memo>)` | String | Short publicly visible memo about the topic. No guarantee of uniqueness. |
| `setAutoRenewPeriod(<autoRenewPeriod>)` | Duration | The initial lifetime of the topic and the amount of time to attempt to extend the topic's lifetime by \(once autoRenew functionality is supported by HAPI\) |
| `setAutoRenewAccountId(<autoRenewAccountId>)` | AccountId | Optional account to be used at the topic's `expirationTime` to extend the life of the topic \(once autoRenew functionality is supported by HAPI\) |

### Create a topic with a submitKey

Creating a topic with a submitKey creates a private topic. In order to submit messages to a private topic, you will need the `submitKey`. The `submitKey` can be a simple key that is shared amongst those who have been granted permission to submit messages to that topic. The `submitKey` can also be a KeyList or ThresholdKey.

#### Example

{% tabs %}
{% tab title="Java" %}
```java
// Generate a Ed25519 private, public key pair
submitKey = Ed25519PrivateKey.generate();
Ed25519PublicKey submitPublicKey = submitKey.publicKey;

final TransactionId transactionId = new ConsensusTopicCreateTransaction()
    .setMaxTransactionFee(20000000)
    .setTopicMemo("HCS topic with submit key")
    .setSubmitKey(submitPublicKey)// The key that is assigned to the topic and required when submitting messages to this topic
    .execute(hapiClient);

topicId = transactionId.getReceipt(hapiClient).getConsensusTopicId();
System.out.println("Created new topic " + topicId + " with ED25519 submitKey of " + submitKey);

```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { Client, ConsensusTopicCreateTransaction, Ed25519PrivateKey, Ed25519PublicKey} = require("@hashgraph/sdk");
require("dotenv").config();

async function main() {
    const operatorPrivateKey = process.env.OPERATOR_KEY;
    const operatorAccount = process.env.OPERATOR_ID;

    if (operatorPrivateKey == null || operatorAccount == null) {
        throw new Error("environment variables OPERATOR_KEY and OPERATOR_ID must be present");
    }

    const client = Client.forTestnet();

    client.setOperator(operatorAccount, operatorPrivateKey);

    const submitKey = await Ed25519PrivateKey.generate();
    const submitPublicKey = submitKey.publicKey;

    const transactionId = await new ConsensusTopicCreateTransaction()
        .setTopicMemo("HCS topic with submit key")
        .setSubmitKey(submitPublicKey)
        .execute(client);
    
    const receipt = await transactionId.getReceipt(client); 
    const topicId = receipt.getConsensusTopicId(); 

    console.log(`Created new topic ${topicId} with ED25519 submitKey of ${submitKey}`)

}

main();
```
{% endtab %}
{% endtabs %}

