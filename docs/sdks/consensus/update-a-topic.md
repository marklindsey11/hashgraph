# Update a topic

`ConsensusTopicUpdateTransaction()` updates the properties of an existing topic. This includes the topic memo, admin key, submit key, and expiration time. If the `adminKey` was set upon the creation of the topic, the `adminKey` is required to sign the transaction to modify any of the topic properties.

| Constructor | Description |
| :--- | :--- |
| `ConsensusTopicUpdateTransaction()` | Initializes the ConsensusTopicUpdateTransaction object |

```java
new ConsensusTopicUpdateTransaction()
```

## Basic

The `adminKey` and `submitKey` on the topic can be updated to any of the following key structures:

* **Simple Key**: one key has the authority to modify the topic \(`adminKey)` or to submit a message to that topic \(`submitKey`\)
* **Key List**: A list of keys that are all required to sign transactions to modify the properties of a  topic \(`adminKey)` or to submit a message to that topic  \(`submitKey`\)
* **Threshold Keys**: Requires a minimum of x number of signatures from a total of y signatures to modify the properties of a topic \(`adminKey)` or to submit a message to that topic  \(`submitKey`\)

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
      <td style="text-align:left"><code>setTopicId(&lt;topicId&gt;)</code>
      </td>
      <td style="text-align:left">TopicId</td>
      <td style="text-align:left">The ID of the topic to update</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setTopicMemo(&lt;memo&gt;)</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Adds/updates the memo for a topic. No guarantee of uniqueness. Null for
        &quot;do not update&quot;.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setAdminKey(&lt;key&gt;)</code>
      </td>
      <td style="text-align:left">PublicKey</td>
      <td style="text-align:left">Access control for update/delete of the topic. If unspecified, no change.
        If empty keyList - the <code>adminKey</code> is cleared.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setSubmitKey(&lt;key&gt;)</code>
      </td>
      <td style="text-align:left">PublicKey</td>
      <td style="text-align:left">Access control for <code>ConsensusService.submitMessage</code>. If unspecified,
        no change. If empty keyList - the submitKey is cleared.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>setExpirationTime</code>
        </p>
        <p><code>(&lt;expirationTime&gt;)</code>
        </p>
      </td>
      <td style="text-align:left">Instant</td>
      <td style="text-align:left">Effective consensus timestamp at (and after) which all consensus transactions
        and queries will fail. The <code>expirationTime </code>may be no longer
        than 90 days from the consensus timestamp of this transaction. If unspecified,
        no change.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>setAutoRenewPeriod</code>
        </p>
        <p><code>(&lt;autoRenewPeriod&gt;)</code>
        </p>
      </td>
      <td style="text-align:left">Duration</td>
      <td style="text-align:left">The initial lifetime of the topic and the amount of time to attempt to
        extend the topic&apos;s lifetime by automatically at the topic&apos;s <code>expirationTime</code>,
        if the <code>autoRenewAccount</code> is configured (once autoRenew functionality
        is supported by HAPI). Limited to MIN_AUTORENEW_PERIOD and MAX_AUTORENEW_PERIOD
        value by server-side configuration.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>setAutoRenewAccountId</code>
        </p>
        <p><code>(&lt;autoRenewAccountId&gt;)</code>
        </p>
      </td>
      <td style="text-align:left">AccountId</td>
      <td style="text-align:left">Optional account to be used at the topic&apos;s expirationTime to extend
        the life of the topic (once autoRenew functionality is supported by HAPI).
        The topic lifetime will be extended up to a maximum of the autoRenewPeriod
        or however long the topic can be extended using all funds on the account
        (whichever is the smaller duration/amount and if any extension is possible
        with the account&apos;s funds).If specified, there must be an adminKey
        and the autoRenewAccount must sign this transaction.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>clearTopicMemo()</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Explicitly clear any memo on the topic</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>clearAdminKey()</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Explicitly clear any adminKey on the topic</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>clearSubmitKey()</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Explicitly clear any submitKey on the topic</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>clearAutoRenewAccountId()</code>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">Explicitly clear any auto renew account ID on the topic</td>
    </tr>
  </tbody>
</table>### Example

{% tabs %}
{% tab title="Java" %}
```java
TransactionId updateTopicTx = new ConsensusTopicUpdateTransaction()
    .setTopicId(topicId)
    .setTopicMemo("Update topic memo")
    .execute(client);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const updateTopicTx = await new ConsensusTopicUpdateTransaction()
    .setTopicId(topicId)
    .setTopicMemo("Update topic memo")
    .execute(client);
```
{% endtab %}
{% endtabs %}



