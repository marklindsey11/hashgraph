# Transfer cryptocurrency

A transaction that transfers hbars and tokens between Hedera accounts. You can enter multiple transfers in a single transaction. The net value of hbars between the sending accounts and receiving accounts must equal zero.

**Transaction Signing Requirements**

* The account sending the tokens is required to sign the transaction. 

{% tabs %}
{% tab title="V2" %}
| Constructor | Description |
| :--- | :--- |
| `new TransferTransaction()` | Initializes the TransferTransaction object |

```java
new TransferTransaction()
```

### Methods

| Method | Type | Description |
| :--- | :--- | :--- |
| `addHbarTransfer(<accountId, value>)` | AccountID, Hbar | The account the transfer is being debited from. The sending account must sign the transaction. The sender and recipient values must net zero. |
| `addTokenTransfer(<tokenId, accountId,value>)` | TokenId, AccountId, long | The ID of the token, the account ID to transfer the tokens from, value of the token to transfer. The sender and recipient values must net zero. |

{% code title="Java" %}
```java
// Create a transaction to transfer 100 hbars
TransferTransaction transaction1 = new TransferTransaction()
     .addHbarTransfer(OPERATOR_ID, new Hbar(-10))
     .addHbarTransfer(newAccountId, new Hbar(10));

//Submit the transaction to a Hedera network
TransactionResponse txResponse = transaction.execute(client);

//Request the receipt of the transaction
TransactionReceipt receipt = txResponse.getReceipt(client);

//Get the transaction consensus status
Status transactionStatus = receipt.status;

System.out.println("The transaction consensus status is " +transactionStatus);

//Version 2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
// Create a transaction to transfer 100 hbars
const transaction = new TransferTransaction()
    .addHbarTransfer(OPERATOR_ID, new Hbar(-100))
    .addHbarTransfer(newAccountId, new Hbar(100));
    
//Submit the transaction to a Hedera network
const txResponse = await transaction.execute(client);

//Request the receipt of the transaction
const receipt = await txResponse.getReceipt(client);

//Get the transaction consensus status
const transactionStatus = receipt.status;

console.log("The transaction consensus status is " +transactionStatus.toString());

//v2.0.5
```
{% endcode %}

{% code title="Go" %}
```java
// Create a transaction to transfer 100 hbars
transaction := hedera.NewTransferTransaction().
		AddHbarTransfer(client.GetOperatorAccountID(), hedera.NewHbar(-1)).
		AddHbarTransfer(hedera.AccountID{Account: 3}, hedera.NewHbar(1))

//Submit the transaction to a Hedera network
txResponse, err := transaction.Execute(client)

if err != nil {
    panic(err)
}

//Request the receipt of the transaction
receipt, err := txResponse.GetReceipt(client)

if err != nil {
    panic(err)
}

//Get the transaction consensus status
transactionStatus := receipt.Status

fmt.Printf("The transaction consensus status is %v\n", transactionReceipt.Status)

//Version 2.0.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Constructor | Description |
| :--- | :--- |
| `new TransferTransaction()` | Initializes the TransferTransaction object |

```java
new TransferTransaction()
```

| Method | Type | Description |
| :--- | :--- | :--- |
| `addHbarTransfer(<accountId, value>)` | AccountId, Hbar/long | The account the transfer is being debited from. The sending account must sign the transaction. The sender and recipient values must net zero. |
| `addTokenTransfer(<tokenId, accountId,value>)` | TokenId, AccountId, long | The ID of the token, the account ID to transfer the tokens from, value of the token to transfer. The sender and recipient values must net zero. |

{% code title="Java" %}
```java
//Create the transfer transaction
TransferTransaction transaction1 = new TransferTransaction()
    .addHbarTransfer(OPERATOR_ID, new Hbar(-10))
    .addHbarTransfer(newAccountId, new Hbar(10));

//Sign with the client operator key and submit the transaction to a Hedera network
TransactionId txId = transaction.execute(client);
        
//Request the receipt of the transaction
TransactionReceipt receipt = txId.getReceipt(client);

//Get the transaction consensus status
Status transactionStatus = receipt.status;

System.out.println("The transaction consensus status is " +transactionStatus);

//v1.3.2
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create the transfer transaction
const transaction = new TransferTransaction()
    .addHbarTransfer(OPERATOR_ID, new Hbar(-10))
    .addHbarTransfer(newAccountId, new Hbar(10));

//Sign with the client operator key and submit the transaction to a Hedera network
const txId = await transaction.execute(client);
        
//Request the receipt of the transaction
const receipt = await txId.getReceipt(client);

//Get the transaction consensus status
const transactionStatus = receipt.status;

console.log("The transaction consensus status is " +transactionStatus);

//v1.4.4
```
{% endcode %}
{% endtab %}
{% endtabs %}



## Get transaction values

{% tabs %}
{% tab title="V2" %}
| Method | Type | Description |
| :--- | :--- | :--- |
| `getHbarTransfers()` | Map&lt;AccountId,  Hbar&gt; | Returns a list of the hbar transfers in this transaction |
| `getTokenTransfers()` | Map&lt;TokenId, Map&lt;AccountId, long&gt;&gt; | Returns the list of token transfers in the transaction |

{% code title="Java" %}
```java
// Create a transaction 
CryptoTransferTransaction transaction = new CryptoTransferTransaction()
    .addSender(OPERATOR_ID, new Hbar(10))
    .addRecipient(newAccountId, new Hbar(10));

//Get transfers
List<Transfer> transfers = transaction.getTransfers();

//v2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
// Create a transaction 
const transaction = new CryptoTransferTransaction()
    .addSender(OPERATOR_ID, new Hbar(10))
    .addRecipient(newAccountId, new Hbar(10));

//Get transfers
const transfers = transaction.getTransfers();

//v2.0.0
```
{% endcode %}

{% code title="Go" %}
```go
// Create a transaction 
transaction := hedera.NewTransferTransaction().
		AddHbarTransfer(client.GetOperatorAccountID(), hedera.NewHbar(-1)).
		AddHbarTransfer(hedera.AccountID{Account: 3}, hedera.NewHbar(1))
//Get transfers
transfers := transaction.GetTransfers()

//v2.0.0
```
{% endcode %}
{% endtab %}
{% endtabs %}

