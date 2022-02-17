# Transfer cryptocurrency

A transaction that transfers hbars and tokens between Hedera accounts. You can enter multiple transfers in a single transaction. The net value of hbars between the sending accounts and receiving accounts must equal zero.&#x20;

{% hint style="warning" %}
* The maximum allowable balance adjustment in a single transfer transaction is 20. A debit from one account and credit to another account equals two balance adjustments.&#x20;
* If you are transferring a token with custom fees, only two levels of nesting of fees are allowed
* The sending account is responsible to pay for the custom token fees
{% endhint %}

**Transaction Signing Requirements**

* The account sending the tokens is required to sign the transaction
* The transaction fee paying account is required to sign the transaction
* The spending account is required to sign the transaction for accounts that have an approved allowance from another account

| Constructor                 | Description                                |
| --------------------------- | ------------------------------------------ |
| `new TransferTransaction()` | Initializes the TransferTransaction object |

```java
new TransferTransaction()
```

### Methods

{% tabs %}
{% tab title="V2" %}
###

| Method                                                                 | Type                                                                                                              | Description                                                                                                                                                                             |
| ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `addHbarTransfer(<accountId>, <value>)`                                | AccountId, Hbar                                                                                                   | <p>The account involved in the transfer and the number of hbars. <br><br>The sender and recipient values must net zero.</p>                                                             |
| `addTokenTransfer(<tokenId>, <accountId>,<value>)`                     | TokenId, AccountId, long                                                                                          | <p>The ID of the token, the account ID involved in the transfer, and the number of tokens to transfer. <br><br>The sender and recipient values must net zero.</p>                       |
| `addNftTransfer(<nftId>, <sender>, <receiver>)`                        | [NftId](../tokens/nft-id.md), [AcountId](../specialized-types.md), [AccountId](../specialized-types.md#accountid) | The NFT ID (token + serial number), the sending account, and receiving account.                                                                                                         |
| `addTokenTransferWithDecimals(<tokenId>, <accountId>, <value>, <int>)` | [TokenId](../tokens/token-id.md), AccountId, long, decimals                                                       | <p>The ID of the token, the account ID involved in the transfer, the number of tokens to transfer, the decimals of the token.<br><br>The sender and recipient values must net zero.</p> |
| `setHbarTransferApproval(<accountId>,<isApproved>)`                    | AccountId, boolean                                                                                                | The owner account ID the spender is authorized to transfer from                                                                                                                         |
| `setTokenTransferApproval(<tokenId>, <accountId>, <isApproved>)`       | TokenId, AccountId, boolean                                                                                       | The owner account ID and token the spender is authorized to transfer from                                                                                                               |
| `setNftTransferApproval(<nftId>,<isApproved>)`                         | NftId, boolean                                                                                                    | The NFT ID the  spender is authorized to transfer                                                                                                                                       |

{% code title="Java" %}
```java
// Create a transaction to transfer 100 hbars
TransferTransaction transaction = new TransferTransaction()
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
| Method                                         | Type                     | Description                                                                                                                                     |
| ---------------------------------------------- | ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `addHbarTransfer(<accountId, value>)`          | AccountId, Hbar/long     | The account the transfer is being debited from. The sending account must sign the transaction. The sender and recipient values must net zero.   |
| `addTokenTransfer(<tokenId, accountId,value>)` | TokenId, AccountId, long | The ID of the token, the account ID to transfer the tokens from, value of the token to transfer. The sender and recipient values must net zero. |

{% code title="Java" %}
```java
//Create the transfer transaction
TransferTransaction transaction = new TransferTransaction()
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
| Method                | Type                                 | Description                                              |
| --------------------- | ------------------------------------ | -------------------------------------------------------- |
| `getHbarTransfers()`  | Map\<AccountId,  Hbar>               | Returns a list of the hbar transfers in this transaction |
| `getTokenTransfers()` | Map\<TokenId, Map\<AccountId, long>> | Returns the list of token transfers in the transaction   |

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
