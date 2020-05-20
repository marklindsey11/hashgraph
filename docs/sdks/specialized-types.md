# Specialized Types

## [AccountId](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/account/AccountId.java)

An `AccountId` is composed of a &lt;shardNum&gt;.&lt;realmNum&gt;.&lt;accountNum&gt; \(eg. 0.0.10\).

* **shardNum** represents the shard number \(`shardId`\). It will default to 0 today, as Hedera only performs in one shard.
* **realmNum** represents the realm number \(`realmId`\). It will default to 0 today, as realms are not yet supported.
* **accountNum** represents the account number \(`accountId`\)

Together these values make up your `AccountId`. When an `AccountId` is requested, be sure all three values are included.

### Constructor

| Constructor | Type | Description |
| :--- | :---: | :--- |
| `AccountId(<shardNum>,<realmNum>,<accountNum>)` | long, long, long | Constructs an `AccountId` with 0 for `shardNum` and `realmNum` \(e.g., `0.0.<accountNum>`\) |

### Methods

| Methods | Type | Description |
| :--- | :--- | :--- |
| `fromString(<account>)` | String | Constructs an `AccountId` from a string formatted as &lt;shardNum&gt;.&lt;realmNum&gt;.&lt;accountNum&gt; |
| `fromSolidityAddress(<address>)` | String | Constructs an `AccountId` from a solidity address in string format  |

### Example

{% tabs %}
{% tab title="Java" %}
```java
AccountId accountId = new AccountId(0 ,0 ,10);
System.out.println(accountId);

// Constructs an accountId from String
AccountId accountId = AccountId.fromString("0.0.10");
System.out.println(accountId);

```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const acctId = new AccountId(100);
console.log(`${acctId}`);

// Construct accountId from String
const acctId = AccountId.fromString(`100`);
console.log(`${acctId}`);
```
{% endtab %}
{% endtabs %}

## [FileId](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/file/FileId.java)

A `FileId` is composed of a &lt;shardNum&gt;.&lt;realmNum&gt;.&lt;fileNum&gt; \(eg. 0.0.15\).

* **shardNum** represents the shard number \(`shardId`\). It will default to 0 today, as Hedera only performs in one shard.
* **realmNum** represents the realm number \(`realmId`\). It will default to 0 today, as realms are not yet supported.
* **fileNum** represents the file number

Together these values make up your accountId. When an `FileId` is requested, be sure all three values are included.

### Constructor

| Constructor | Type | Description |
| :--- | :---: | :--- |
| `FileId(<shardNum>,<realmNum>,<fileNum>)` | long, long, long | Constructs an `FileId` with 0 for `shardNum` and `realmNum` \(e.g., `0.0.<fileNum>`\) |

### Methods

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
      <td style="text-align:left"><code>fromString()</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Constructs an <code>FileId</code> from a string formatted as</p>
        <p>&lt;shardNum&gt;.&lt;realmNum&gt;.&lt;fileNum&gt;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>fromSolidityAddress()</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Constructs an <code>FileId</code> from a solidity address in string format</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>FileId.ADDRESS_BOOK</code>
      </td>
      <td style="text-align:left">FileId</td>
      <td style="text-align:left">The public node address book for the current network</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>FileId.EXCHANGE_RATES</code>
      </td>
      <td style="text-align:left">FileId</td>
      <td style="text-align:left">The current exchange rate of HBAR to USD</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>FileId.FEE_SCHEDULE</code>
      </td>
      <td style="text-align:left">FileId</td>
      <td style="text-align:left">The current fee schedule for the network</td>
    </tr>
  </tbody>
</table>### Example

{% tabs %}
{% tab title="Java" %}
```java
FileId fileId = new FileId(0,0,15);
System.out.println(fileId);

//Contructs a FileId from string
FileId fileId = FileId.fromString("0.0.15");
System.out.println(fileId);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const newFileId = new FileId(100);
console.log(`${newFileId}`);

//Construct a fileId from a String
const newFileIdFromString = FileId.fromString(`100`); 
console.log(`${newFileIdFromString}`);
```
{% endtab %}
{% endtabs %}

## [ContractId](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/contract/ContractId.java)

A `ContractId` is composed of a &lt;shardNum&gt;.&lt;realmNum&gt;.&lt;contractNum&gt; \(eg. 0.0.20\).

* **shardNum** represents the shard number \(`shardId`\). It will default to 0 today, as Hedera only performs in one shard.
* **realmNum** represents the realm number \(`realmId`\). It will default to 0 today, as realms are not yet supported.
* **contractNum** represents the contract number

Together these values make up your `ContractId`. When an `ContractId` is requested, be sure all three values are included. ContractId's are automatically assigned when you create a new smart contract.

### Constructor

| Constructor | Type | Description |
| :--- | :--- | :--- |
| `ContractId(<shardNum>,<realmNum>,<contractNum>)` | long, long, long | Constructs a `ContractId` with 0 for `shardNum` and `realmNum` \(e.g., `0.0.<contractNum>`\) |

### Methods

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
      <td style="text-align:left"><code>fromString(&lt;account&gt;)</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">
        <p>Constructs a <code>ContractId </code>from a string formatted as</p>
        <p>&lt;shardNum&gt;.&lt;realmNum&gt;.&lt;contractNum&gt;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>fromSolidityAddress(&lt;address&gt;)</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Constructs a <code>ContractId</code> from a solidity address in string format</td>
    </tr>
  </tbody>
</table>### Example

{% tabs %}
{% tab title="Java" %}
```java
ContractId contractId = new ContractId(0,0,20);
System.out.println(contractId);

// Constructs a ContractId from string
ContractId contractId = ContractId.fromString("0.0.20");
System.out.println(contractId);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const newContractId = new ContractId(100);
console.log(`${newContractId}`);

// Construct a contractId from a String
const newContractId = ContractId.fromString(`100`); 
console.log(`${newContractId}`);
```
{% endtab %}
{% endtabs %}

## [TransactionId](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/TransactionId.java)

A `TransactionId` is composed of the current time and account that is primarily signing the transaction. Every transaction has an associated `TransactionId`. Transaction IDs are automatically assigned for every transaction that is submitted to the network.

### Constructor

| Constructor | Type | Description |
| :--- | :--- | :--- |
| `TransactionId(<accountId>)` | AccountId | Generates a new transaction ID for the given `accountId`. |

### Example

{% tabs %}
{% tab title="Java" %}
```java
TransactionId transactionId = new TransactionId(myAccountId);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const txId = new TransactionId(newAccountId);
console.log(`${txId}`);
```
{% endtab %}
{% endtabs %}

## [TopicId](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/consensus/ConsensusTopicId.java)

A `topicId` is composed of a &lt;shardNum&gt;.&lt;realmNum&gt;.&lt;topicNum&gt; \(eg. 0.0.100\).

* **shardNum** represents the shard number \(`shardId`\). It will default to 0 today, as Hedera only performs in one shard.
* **realmNum** represents the realm number \(`realmId`\). It will default to 0 today, as realms are not yet supported.
* **topicNum** represents the topic number \(`topicId`\)

### Constructor

| Constructor | Type | Description |
| :--- | :--- | :--- |
| `ConsensusTopicId(<shardNum>,<realmNum>,<topicNum>)` | long, long, long | Constructs an `TopicId` with `0` for `shardNum` and `realmNum` \(e.g., `0.0.<topicNum>`\) |

| Methods | Type | Description |
| :--- | :--- | :--- |
| `fromString(<topic>)` | String | Constructs a topic ID from a String |
| `ConsensusTopicId.toString()` |  | Constructs a topic ID to String format |

### Example

{% tabs %}
{% tab title="Java" %}
```java
ConsensusTopicId topicId = new ConsensusTopicId(0,0,100);
System.out.println(topicId)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const txId = new TransactionId(newAccountId);
console.log(`${txId}`);
```
{% endtab %}
{% endtabs %}

