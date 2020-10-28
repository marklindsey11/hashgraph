# Transactions

Transactions are requests that are submitted by a client to a node in the Hedera network. Every transaction has a fee associated with it that will pay for processing the transaction. The following table lists the transaction type requests for each service.

{% hint style="info" %}
Transactions have a 6,144 kb transaction size limit. This includes the signatures on the transaction. The estimated single signature size is about 80-100 bytes.
{% endhint %}

| Cryyptocurrency Accounts | Consensus | File Service | Smart Contracts |
| :--- | :--- | :--- | :--- |
| [AccountCreateTransaction](cryptocurrency/create-an-account.md) | [ConsensusTopicCreateTransaction](consensus/create-a-topic.md) | [FileCreateTransaction](file-storage/create-a-file.md) | [ContractCreateTransaction](smart-contracts/create-a-smart-contract.md) |
| [AccountUpdateTransaction](cryptocurrency/update-an-account.md) | [ConsensusTopicUpdateTransaction](consensus/update-a-topic.md) | [FileAppendTransaction](file-storage/append-to-a-file.md) | [ContractUpdateTransaction](smart-contracts/update-a-smart-contract.md) |
| [CryptoTransferTransaction](cryptocurrency/transfer-cryptocurrency.md) | [ConsensusMessageSubmitTransaction](consensus/submit-a-message.md) | [FileUpdateTransaction](file-storage/update-a-file.md) | [ContractDeleteTransaction](smart-contracts/delete-a-smart-contract.md) |
| [AccountDeleteTransaction](cryptocurrency/delete-an-account.md) | [ConsensusTopicDeleteTransaction](consensus/delete-a-topic.md) | [FileDeleteTransaction](file-storage/delete-a-file.md) |  |



The following methods can be called when building the above transaction types:

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
      <td style="text-align:left"><code>setMaxTransactionFee(&lt;fee&gt;)</code>
      </td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">Sets the maximum fee, in tinybar, that the client is willing to pay to
        execute this transaction, which is split between the network and the node.
        The actual fee assessed may be less than this, in which case you will only
        be charged that amount. An error is thrown if the assessed fee is greater
        than this.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setTransactionMemo(&lt;memo&gt;)</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">Sets any notes or description that should be put into the transaction
        record (if one is requested). Note that a max of length of 100 is enforced.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setTransactionValidDuration(&lt;Duration&gt;)</code>
      </td>
      <td style="text-align:left">Duration</td>
      <td style="text-align:left">
        <p>The Duration in which the transaction will be valid from transactionValidStart
          time</p>
        <p>Max: 180 seconds</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setNodeAccountId(&lt;accountId&gt;)</code>
      </td>
      <td style="text-align:left">AccountId</td>
      <td style="text-align:left">The account of the node that submits the client&apos;s transaction to
        the network</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setTransactionId(&lt;transactionId&gt;)</code>
      </td>
      <td style="text-align:left">TransactionId</td>
      <td style="text-align:left">The ID for this transaction, which includes the payer&apos;s account (the
        account paying the transaction fee). If two transactions have the same
        transactionID, they won&apos;t both have an effect</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>build(&lt;client&gt;)</code>
      </td>
      <td style="text-align:left">Client</td>
      <td style="text-align:left">Builds the transaction</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sign(&lt;key&gt;)</code>
      </td>
      <td style="text-align:left">PrivateKey&lt; extends PublicKey&gt;</td>
      <td style="text-align:left">Expliclity sign the transaction with a private key</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>execute(&lt;client&gt;)</code>
      </td>
      <td style="text-align:left">Client</td>
      <td style="text-align:left">Submits the transaction to the Hedera network for consensus</td>
    </tr>
  </tbody>
</table>

## Transaction Receipt

The receipt of a transaction returns whether the transaction has reached consensus or not. It also returns the a new `accountId`, `consensusTopicId`, `contractId`, `tokenId` and `fileId` if generated in the transaction.

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
| `getTokenId()` | `TokenId` | The newly generated token ID |

## Transaction Record

A transaction record returns the following information about a transaction:

* Transaction ID
* Transaction hash
* Transaction fee
* List of transfers
* List of token transfers
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
| `tokenTransfers` | Map&lt;TokenId, Map&lt;AccountId, List&lt;Long&gt;&gt;&gt; | The token ID and the account ID the tokens were debited and creditied from |

