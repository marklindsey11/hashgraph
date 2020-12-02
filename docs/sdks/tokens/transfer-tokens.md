# Transfer tokens

Transfer tokens from some accounts to other accounts. The transaction must be signed by the sending account. Each negative amount is withdrawn from the corresponding account \(a **sender**\), and each positive one is added to the corresponding account \(a **receiver**\). All amounts must have sum of zero. Each amount is a number with the lowest denomination possible for a token. Example: Token X has 2 decimals. Account A transfers amountof 100 tokens by providing 10000 as amount in the TransferList. If Account A wants to send 100.55 tokens, he must provide 10055 as amount. If any sender account fails to have sufficient token balance, then the entire transaction fails and none of the transfers occur, though transaction fee is still charged.

{% hint style="info" %}
The account must be associated to the token prior to transfering tokens to that account. See TokenAssociateTransaction.
{% endhint %}

| Constructor | Description |
| :--- | :--- |
| `new TransferTransaction()` | Initializes a TransferTransaction object |

```java
new TransferTransaction()
```

### Methods

{% tabs %}
{% tab title="V2" %}
| Method | Type | Description |
| :--- | :--- | :--- |
| `addHbarTransfer(<accountId, value>)` | AccountID, Hbar/long | Add the from and to account to transfer hbars \(you will need to call this method twice\). The sending account must sign the transaction. The sender and recipient values must net zero. |
| `addTokenTransfer(<tokenId, accountId,value>)` | TokenId, AccountId, long | Add the from and to account to transfer tokens \(you will need to call this method twice\).The ID of the token, the account ID to transfer the tokens from or to, and the value of the token to transfer. The sender and recipient values must net zero. |

{% code title="Java" %}
```java
//Create the transfer transaction
TransferTransaction transaction = new TransferTransaction()
     .addTokenTransfer(tokenId, OPERATOR_ID, -10)
     .addTokenTransfer(tokenId, accountId, 10);

//Sign with the client operator key and submit the transaction to a Hedera network
TransactionResponse txResponse = transaction.execute(client);

//Request the receipt of the transaction
TransactionReceipt receipt = txResponse.getReceipt(client);

//Get the transaction consensus status
Status transactionStatus = receipt.status;

System.out.println("The transaction consensus status is " +transactionStatus);

//v2.0.1
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create the transfer transaction
const transaction = await new TransferTransaction()
     .addTokenTransfer(tokenId, accountId, -10)
     .addTokenTransfer(tokenId, treasuryAccountId, 10)
     .freezeWith(client);

const signTx = await transaction.sign(accountKey)
    
const txResponse = await signTx.execute(client);
    
//Request the receipt of the transaction
const receipt = await txResponse.getReceipt(client);
    
//Obtain the transaction consensus status
const transactionStatus = receipt.status;

console.log("The transaction consensus status " +transactionStatus31.toString());

//v2.0.5
```
{% endcode %}

{% code title="Go" %}
```go
//Create the transfer transaction and freeze the transaction from further modification
transaction, err := hedera.NewTransferTransaction().
		AddTokenTransfer(tokenId, accountId1, -10).
		AddTokenTransfer(tokenId, accountId2, 10).
		FreezeWith(client)

//Sign with the accountID1 private key, sign with the client operator key and submit to a Hedera network
txResponse, err := transaction.Sign(accountKey1).Execute(client)

if err != nil {
		panic(err)
}

//Request the receipt of the transaction
receipt, err := txResponse.GetReceipt(client)
if err != nil {
		panic(err)
}

//Get the transaction consensus status
status := receipt.Status

fmt.Printf("The transaction consensus status is %v\n", status)
//v2.1.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
\*\*\*\*

| Method | Type | Description |
| :--- | :--- | :--- |
| `addHbarTransfer(<accountId, value>)` | AccountID, Hbar/long | Add the from and to account to transfer hbars \(you will need to call this method twice\). The sending account must sign the transaction. The sender and recipient values must net zero. |
| `addTokenTransfer(<tokenId, accountId,value>)` | TokenId, AccountId, long | Add the from and to account to transfer tokens \(you will need to call this method twice\).The ID of the token, the account ID to transfer the tokens from or to, and the value of the token to transfer. The sender and recipient values must net zero. |

{% code title="Java" %}
```java
//Create the transfer transaction
TransferTransaction transaction = new TransferTransaction()
    .addTokenTransfer(tokenId, accountId, -10)
    .addTokenTransfer(tokenId, OPERATOR_ID, 10);


//Sign with the client operator key and submit the transaction to a Hedera network
TransactionId txId = transaction.build(client).sign(accountKey).execute(client);
            
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
//Transfer 100 tokens between two accounts
const transaction = new TransferTransaction()
    .addTokenTransfer(tokenId, accountId, 100)
    .addTokenTransfer(tokenId, OPERATOR_ID, 100);

//Build the unsigned transaction, sign with sender account private key, submit the transaction to a Hedera network
const transactionId = await transaction.build(client).sign(accountKey).execute(client);
    
//Request the receipt of the transaction
const getReceipt = await transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
const transactionStatus = getReceipt.status;

console.log("The transaction consensus status " +transactionStatus);
```
{% endcode %}
{% endtab %}
{% endtabs %}



