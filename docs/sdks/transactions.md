# Transactions

Transactions are requests that are submitted by a client to a node in the Hedera network. Every transaction has a fee associated with it that will pay for processing the transaction. The following table lists the transaction type requests for each service.

{% hint style="info" %}
Transactions have a 6,144 kb transaction size limit. This includes the signatures on the transaction. The estimated single signature size is about 80-100 bytes.
{% endhint %}

| Cryyptocurrency Accounts | File Service | Smart Contracts |
| :--- | :--- | :--- |
| AccountCreateTransaction | FileCreateTransaction | ContractCreateTransaction |
| AccountUpdateTransaction | FileAppendTransaction | ContractUpdateTransaction |
| CryptoTransferTransaction | FileUpdateTransaction | ContractDeleteTransaction |
| AccountDeleteTransaction | FileDeleteTransaction |  |



The following methods can be called when building the above transaction types:

| Methods | Type | Description |
| :--- | :--- | :--- |
| `setMaxTransactionFee(<fee>)` | long | Sets the maximum fee, in tinybar, that the client is willing to pay to execute this transaction, which is split between the network and the node. The actual fee assessed may be less than this, in which case you will only be charged that amount. An error is thrown if the assessed fee is greater than this. |
| `setTransactionMemo(<memo>)` | String | Sets any notes or description that should be put into the transaction record \(if one is requested\). Note that a max of length of 100 is enforced. |
| `setTransactionValidDuration(<Duration>)` | Duration | The Duration in which the transaction will be valid from transactionValidStart time |
| `setNodeAccountId(<accountId>)` | AccountId | The account of the node that submits the client's transaction to the network |
| `setTransactionId(<transactionId>)` | TransactionId | The ID for this transaction, which includes the payer's account \(the account paying the transaction fee\). If two transactions have the same transactionID, they won't both have an effect |
| `build(<client>)` | Client | Builds the transaction |
| `sign(<key>)` | PrivateKey&lt;? extends PublicKey&gt; | Expliclity sign the transaction with a private key |
| `execute(<client>)` | Client | Submits the transaction to the Hedera network for consensus  |

## Transaction Receipt

The receipt of a transaction returns whether the transaction has reached consensus or not. It also returns the a new `accountId`, `consensusTopicId`, `contractId`, and `fileId` if generated in the transaction.

| Method | Type | Description |
| :--- | :--- | :--- |
| `getReceipt(<client>)` | TransactionReceipt | Gets the receipt for a transaction object |

{% tabs %}
{% tab title="Java" %}
```java
TransactionReceipt receipt = txId.getReceipt(client);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const transactionReceipt = await transactionId.getReceipt(client);
```
{% endtab %}
{% endtabs %}

### Modifiers

| Modifier | Type | Description |
| :--- | :--- | :--- |
| `getAccountId()` | AccountId | The newly generated account ID |
| `getConsensusTopicId()` | ConsensusTopicId | The newly generated topic ID |
| `getConsensusTopicRunningHash()` | byte \[ \] | The topic running hash |
| `getConsensusTopicSequenceNumber()` | long | The topic sequence number |
| `getContractId()` | ContractId | The newly generated contract ID |
| `getFileId()` | FileId | The newly generated file ID |

## Transaction Record

A transaction record returns the following information about a transaction:

* Transaction ID
* Transaction hash
* Transaction fee
* List of transfers
* Consensus timestamp
* Receipt 
* Memo

{% hint style="info" %}
**Transfers**  
With the R4 release, how the HBAR balance changes of accounts involved in the transaction \(either directly or node\) are represented within the transaction record has been modified. In the past, each transfer of HBARs , whether a payment from one account to another or a fee paid to a Hedera node or to Hedera – was listed individually. The list of transfers might include one for the payer making the fundamental payment, one for that same account paying a fee to the network, and another for the same account paying a fee to the node. The new model combines all those individual transfers and shows, for each account involved in the transaction, only the net transfer value.
{% endhint %}

| Method | Type | Description |
| :--- | :--- | :--- |
| `getRecord(<client>)` | TransactionRecord | Gets the record for a transaction object |

{% tabs %}
{% tab title="Java" %}
```java
TransactionRecord record = txId.getRecord(client);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const transactionRecord = await transactionId.getRecord(client)
```
{% endtab %}
{% endtabs %}

### Modifiers

| Modifier | Type | Description |
| :--- | :--- | :--- |
| `transactionId` | TransactionId | The ID of the transaction this record represents |
| `transactionHash` | byte \[ \] | The hash of the Transaction that executed |
| `transactionFee` | long | The actual transaction fee charged, unless there were insufficient funds in the operator account |
| `transfers` | List\(&lt;Transfer&gt;\) | All Hbar transfers as a result of this transaction, such as fees, or transfers performed by the transaction, or by a smart contract it calls, or by the creation of threshold records that it triggers. |
| `consensusTimeStamp` | Instant | The consensus timestamp |
| `receipt` | TransactionReceipt | The status \(reach consensus, or failed, or is unknown\), and the ID of any new account/file/instance created |
| `transactionMemo` | String | The memo that was submitted as part of the transaction \(max 100 bytes\) |

