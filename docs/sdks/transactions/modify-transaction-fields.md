# Modify transaction fields

For every transaction submitted to a Hedera network you can modify the transaction ID, amount of time the transaction has to reach consensus, a memo field to attach a note, the account ID of the node the transaction will be submitted to, and the maximum fee the client is willing to pay for a given transaction. The SDKs do not require you to set these fields when submitting a transaction to a Hedera network as the SDK either creates the value at the time of submission or inputs default values. The methods listed below can be used to modify any of these values. 

{% hint style="info" %}
Note: The total size for a given transaction is limited to 6KiB
{% endhint %}

<table>
  <thead>
    <tr>
      <th style="text-align:left">Fields</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Transaction ID</b>
      </td>
      <td style="text-align:left">
        <p>Set the ID for this transaction. The transaction ID includes the operator&apos;s
          account ( the account paying the transaction fee). If two transactions
          have the same transaction ID, they won&apos;t both have an effect. One
          will complete normally and the other will fail with a duplicate transaction
          status.</p>
        <p>
          <br />Normally, you should not use this method. Just before a transaction is
          executed, a
          <br />transaction ID will be generated from the operator on the client.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Valid Duration</b>
      </td>
      <td style="text-align:left">
        <p>Set the duration that this transaction is valid for</p>
        <p>Note: Max network valid duration is 180 seconds. SDK default value is
          120 seconds</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Memo</b>
      </td>
      <td style="text-align:left">Set a note or description that should be recorded in the transaction record
        (maximum length of 100 characters). Anyone can view this memo on the network</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Node ID</b>
      </td>
      <td style="text-align:left">Set the account ID of the node that this transaction will be submitted
        to.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Max transaction fee</b>
      </td>
      <td style="text-align:left">
        <p>Set the max transaction fee for the operator (transaction fee payer account)
          is willing to pay</p>
        <p>Default: 1 hbar</p>
      </td>
    </tr>
  </tbody>
</table>

{% tabs %}
{% tab title="V2" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setTransactionID(<transactionId>)` | TransactionID | Optional |
| `setTransactionValidDuration(<validDuration>)` | Duration | Optional |
| `setTransactionMemo(<memo>)` | String | Optional |
| `setNodeAccountIds(<nodeAccountIds>)` | List&lt;AccountId&gt; | Optional |
| `setMaxTransactionFee(<maxTransactionFee>)` | Hbar | Optional |

{% code title="Java" %}
```java
//Create the transaction and set the transaction properties
Transaction transaction = new AccountCreateTransaction() //Any transaction can be applied here
    .setKey(key)
    .setInitialBalance(Hbar.fromTinybars(1000))
    .setMaxTransactionFee(new Hbar(2)) //Set the max transaction fee to 2 hbar
    .setTransactionMemo("Transaction memo"); //Set the node ID to submit the transaction to
    
//v2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create the transaction and set the transaction properties
const transaction = await new AccountCreateTransaction() //Any transaction can be applied here
    .setKey(key)
    .setInitialBalance(Hbar.fromTinybars(1000))
    .setMaxTransactionFee(new Hbar(2)) //Set the max transaction fee to 2 hbar
    .setTransactionMemo("Transaction memo"); //Set the node ID to submit the transaction to
```
{% endcode %}

{% code title="Go" %}
```go
//Create the transaction and set the transaction properties
transaction := hedera.NewAccountCreateTransaction(). //Any transaction can be applied here
    SetKey(newKey.PublicKey()).
    SetInitialBalance(hedera.NewHbar(1000)). 
    SetMaxTransactionFee(hedera.NewHbar(2)). //Set the max transaction fee to 2 hbar
    SetTransactionMemo("Transaction memo") //Set the transaction memo

//v2.0.0 
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}


| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setTransactionID(<transactionId>)` | TransactionID | Optional |
| `setTransactionValidDuration(<validDuration>)` | Duration | Optional |
| `setTransactionMemo(<memo>)` | String | Optional |
| `setNodeAccountId(<nodeAccountId>)` | AccountId | Optional |
| `setMaxTransactionFee(<maxTransactionFee>)` | long/Hbar | Optional |

{% code title="Java" %}
```java
//Create the transaction and set the transaction properties
Transaction transaction = new AccountCreateTransaction() //Any transaction can be applied here
    .setKey(publicKey)
    .setInitialBalance(new Hbar(100))
    .setMaxTransactionFee(new Hbar(2)) //Set the max transaction fee to 2 hbar
    .setTransactionMemo("Transaction memo"); //Set the node ID to submit the transaction to
    
//v1.3.2
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create the transaction and set the transaction properties
const transaction = new AccountCreateTransaction() //Any transaction can be applied here
    .setKey(publicKey)
    .setInitialBalance(new Hbar(100))
    .setMaxTransactionFee(new Hbar(2)) //Set the max transaction fee to 2 hbar
    .setTransactionMemo("Transaction memo"); 

//v1.4.4
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Get transaction properties

{% tabs %}
{% tab title="V2" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `getTransactionID()` | TransactionID | Optional |
| `getTransactionValidDuration()` | Duration | Optional |
| `getTransactionMemo()` | String | Optional |
| `getNodeAccountId()` | AccountID | Optional |
| `getMaxTransactionFee()` | Hbar | Optional |
| `getTransactionHash()` | byte\[ \] | Optional |
| `getTransactionHashPerNode()` | Map&lt;AccountId, byte \[ \]&gt; | Optional |
| `getSignatures()` | Map&lt;AccountId, Map&lt;PublicKey, byte \[ \]&gt;&gt; | Optional |

{% code title="Java" %}
```java
//Create the transaction and set the transaction properties
Transaction transaction = new AccountCreateTransaction() //Any transaction can be applied here
    .setInitialBalance(Hbar.fromTinybars(1000))
    .setMaxTransactionFee(new Hbar(100)) //Set the max transaction fee to 100 hbar
    .setNodeAccountId(new AccountId(3)) //Set the node ID to submit the transaction to
    .setTransactionMemo("Transaction memo"); //Add a transaction memo
    
Hbar maxTransactionFee = transaction.getMaxTransactionFee();
//v2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create the transaction and set the transaction properties
const transaction = await new AccountCreateTransaction() //Any transaction can be applied here
    .setInitialBalance(Hbar.fromTinybars(1000))
    .setMaxTransactionFee(new Hbar(100)) //Set the max transaction fee to 100 hbar
    .setNodeAccountId(new AccountId(3)) //Set the node ID to submit the transaction to
    .setTransactionMemo("Transaction memo"); //Add a transaction memo
    
const maxTransactionFee = transaction.getMaxTransactionFee();
```
{% endcode %}

{% code title="Go" %}
```java
//Create the transaction and set the transaction properties
transaction := hedera.NewAccountCreateTransaction(). //Any transaction can be applied here
    SetKey(newKey.PublicKey()).
    SetInitialBalance(hedera.NewHbar(1000)). 
    SetMaxTransactionFee(hedera.NewHbar(2)). //Set the max transaction fee to 2 hbar
    SetTransactionMemo("Transaction memo") //Add a transaction memo

maxtransactionFee := transaction.GetMaxTransactionFee()
//v2.0.0         
```
{% endcode %}
{% endtab %}
{% endtabs %}

## 

