# Get a transaction record

You can request a transaction record for up to 3 minutes after a transaction has reached consensus. The transaction record provides the following information about a transaction:

#### Transaction Record Fields

| Fields | Description |
| :--- | :--- |
| **Transaction ID** | The ID of the transaction |
| **Consensus timestamp** | The time the transaction reached consensus and was added to the ledger |
| **Contract Function Result** | The contract function result |
| **Receipt** | The receipt of the transaction |
| **Transaction Fee** | The transaction fee that was charged |
| **Transaction Hash** | The transaction hash |
| **Transaction Memo** | The transaction memo if there was one added |
| **Transfers** | A list of transfers made in the transaction. The list of transfers includes a payment made to the node, the service fee, and transaction fee |
| **Token Transfers** | A list of the token transfers  |

**Transaction Signing Requirements**

* The client operator account private key is required to sign

### Methods

{% tabs %}
{% tab title="V2" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `<TransactionResponse>.getRecord(<client>)` | TransactionRecord | Required |
| `<TransactionRecord>.transactionId` | TransactionId | Optional |
| `<TransactionRecord>.consensusTimestamp` | Instant | Optional |
| `<TransactionRecord>.contractFunctionResult` | ContractFunctionResult | Optional |
| `<TransactionRecord>.receipt` | TransactionReceipt | Optional |
| `<TransactionRecord>.transactionFee` | Hbar | Optional |
| `<TransactionRecord>.transactionHash` | ByteString | Optional |
| `<TransactionRecord>.transactionMemo` | String | Optional |
| `<TransactionRecord>.transfers` | List&lt;Transfer&gt; | Optional |
| `<TransactionRecord>.tokentransfers` | Map&lt;TokenId, Map&lt;AccountId, List&lt;Long&gt;&gt;&gt; | Optional |

{% code title="Java" %}
```java
//Create a transaction
AccountCreateTransaction transaction = new AccountCreateTransaction()
        .setKey(newKey.getPublicKey())
        .setInitialBalance(new Hbar(1));

//Sign with the client operator account key and submit to a Hedera network
TransactionResponse txResponse = transaction.execute(client);

//Request the record of the transaction
TransactionRecord record = txResponse.getRecord(client);

System.out.println("The transaction record is " +record);

//v2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create a transaction
const transaction = new AccountCreateTransaction()
        .setKey(newKey.getPublicKey())
        .setInitialBalance(new Hbar(1));

//Sign with the client operator account key and submit to a Hedera network
const txResponse = await transaction.execute(client);

//Request the record of the transaction
const record = await txResponse.getRecord(client);

console.log("The transaction record is " +record);

//v2.0.0
```
{% endcode %}

{% code title="Go" %}
```java
//Create a transaction
transaction := hedera.NewAccountCreateTransaction().
		SetKey(privateKey.PublicKey()).
		SetInitialBalance(hedera.NewHbar(1000))

//Sign with the client operator account key and submit to a Hedera network
txResponse, err := transaction.Execute(client)

//Request the record of the transaction
record, err := txResponse.GetRecord(client)

fmt.Printf("The transaction record is %v\n", record)

//v2.0.0
```
{% endcode %}

#### Sample Output:

`TransactionRecord{  
     receipt=TransactionReceipt{  
          status=SUCCESS,   
          exchangeRate=ExchangeRate{  
               hbars=30000, cents=116646,   
               expirationTime=2020-09-04T03:00:007  
          },   
         accountId=0.0.97001,   
         fileId=null,   
         contractId=null,   
         topicId=null,   
         topicSequenceNumber=null  
    },                    
    transactionHash=e005670a1f49c4fd776b2d432db3e5cb31441 bb5a35bff412ec3b41cb1 3366ce00b5c1b9900aad1467f9709a649ccc20,   
     consensusTimestamp=2020-11-05T08:34:31.107311002Z,  
     transactionId=0.0.9401@160456525 8.479476328,  
     transactionMemo=,   
     transactionFee=0.25401241 ℏ,   
     contractFunctionResult=null,   
     transfers=[  
          Transfer{accountId=0.0.5, amount=0.01501152 ℏ}, (node fee)  
          Transfer{accountId=0.0.98, amount=0.23900089 ℏ}, (service fee)  
          Transfer{accountId=0.0.9401, amount=-1.25401241 ℏ}, (transaction fee) initial balance of new account  
          Transfer{accountId=0.0.97001, amount=1 ℏ} (Initial balance of the new account)  
     ]  
}`
{% endtab %}

{% tab title="V1" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `<TransactionId>.getRecord(<client>)` | TransactionRecord | Required |
| `<TransactionRecord>.transactionId` | TransactionId | Optional |
| `<TransactionRecord>.consensusTimestamp` | Instant | Optional |
| `<TransactionRecord>.contractFunctionResult` | ContractFunctionResult | Optional |
| `<TransactionRecord>.receipt` | TransactionReceipt | Optional |
| `<TransactionRecord>.transactionFee` | long | Optional |
| `<TransactionRecord>.transactionHash` | byte \[ \] | Optional |
| `<TransactionRecord>.transactionMemo` | String | Optional |
| `<TransactionRecord>.transfers` | List&lt;Transfer&gt; | Optional |
| `<TransactionRecord>.tokentransfers` | Map&lt;TokenId, Map&lt;AccountId, List&lt;Long&gt;&gt;&gt; | Optional |

{% code title="Java" %}
```java
//Create a transaction
AccountCreateTransaction transaction = new AccountCreateTransaction()
        .setKey(newKey.getPublicKey())
        .setInitialBalance(new Hbar(1));

//Sign with the client operator account key and submit to a Hedera network
TransactionId txId = transaction.execute(client);

//Request the record of the transaction
TransactionRecord record = txId.getRecord(client);

System.out.println("The transaction record is " +record);

//v1.3.2
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create a transaction
const transaction = new AccountCreateTransaction()
        .setKey(newKey.getPublicKey())
        .setInitialBalance(new Hbar(1));

//Sign with the client operator account key and submit to a Hedera network
const txId = await transaction.execute(client);

//Request the record of the transaction
const record = await txId.getRecord(client);

console.log("The transaction record is " +record);

//v1.4.4
```
{% endcode %}
{% endtab %}
{% endtabs %}

## 

