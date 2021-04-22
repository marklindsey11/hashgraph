# Get a transaction receipt

The transaction receipt gives you information about a transaction including whether or not the transaction reached consensus on the network. You request the receipt for every transaction type and there is currently no transaction fee associated with this network request. 

#### Transaction Receipt Fields

* Whether the transaction reached consensus or not \(success or fail\)
* The newly generated account ID, topic ID, token ID, file ID, schedule ID, or smart contract ID
* The exchange rate
* The topic running hash
* The topic sequence number

Receipts can be requested from the Hedera network for up to 3 minutes. 

**Transaction Signing Requirements**

* Transaction receipt requests do not have an associated fee at this time

### Methods

{% tabs %}
{% tab title="V2" %}
| Method | Type | Description |
| :--- | :--- | :--- |
| `<TransactionResponse>.getReceipt(<client>)` | TransactionReceipt | Returns the receipt of a transaction |
| `<TransactionResponse>.getReceipt(<client, timeout>)` | Client, Duration | Request the receipt from the network for this duration |
| `<TransactionResponse>.getReceiptAsync(<client, timeout>)` | Client, Duration | Request receipt asynchronously for the provided duration |
| `<TransactionReceipt>.status` | Status | Whether the transaction reached consensus or not |
| `<TransactionReceipt>.accountId` | AccountId | The newly generated account ID |
| `<TransactionReceipt>.topicId` | TopicId | The newly generated topic ID |
| `<TransactionReceipt>).fileId` | FileId | The newly generated file ID |
| `<TransactionReceipt>).contractId` | ContractId | The newly generated contract ID |
| `<TransactionReceipt>).tokenId` | TokenId | The newly generated token ID |
| `<TransactionReceipt>).scheduleId` | ScheduleId | The newly generated schedule ID |
| `<TransactionReceipt>).exchangeRate` | ExchangeRate | The exchange rate in hbar, cents, and expiration time |
| `<TransactionReceipt>.topicRunningHash` | ByteString | The topic running hash |
| `<TransactionReceipt>.topicSequenceNumber` | long | The topic sequence number |
| `<TransactionReceipt>.totalSupply` | long | The total supply of a token |

{% code title="Java" %}
```java
//Get the receipt of the transaction
TransactionReceipt receipt = txResponse.getReceipt(client);

System.out.println("The transaction receipt: " +receipt);

//v2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Get the receipt of the transaction
const receipt = await txResponse.getReceipt(client);

console.log("The transaction receipt: " +receipt);

//v2.0.0
```
{% endcode %}

{% code title="Go" %}
```java
//Request the receipt of the transaction
receipt, err := txResponse.GetReceipt(client)

if err != nil {
    panic(err)
}

fmt.Printf("The transaction receipt %v\n", receipt)

//v2.0.0
```
{% endcode %}

#### Sample Output:

`TransactionReceipt{  
     status=SUCCESS,  
     exchangeRate=ExchangeRate{  
          hbars=1,  
          cents=12,   
          expirationTime=2100-01-01T00:00:00Z  
     },   
     accountId=null,  
     fileId=null,   
     contractId=null,   
     topicId=null,   
     tokenId=null,   
     topicSequenceNumber=null,   
     topicRunningHash=null,   
     totalSupply=0,   
     scheduleId=0.0.2531  
}`
{% endtab %}
{% endtabs %}

