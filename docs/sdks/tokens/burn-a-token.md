# Burn a token

Burns tokens from the Treasury Account. If no Supply Key is defined, the transaction will resolve to TOKEN\_HAS\_NO\_SUPPLY\_KEY. 

* The operation decreases the Total Supply of the Token. 
* Total supply cannot go below zero. 
* The amount provided must be in the lowest denomination possible. 
* Example: Token A has 2 decimals. In order to burn 100 tokens, one must provide amount of 10000. In order to burn 100.55 tokens, one must provide amount of 10055.

| Constructor | Description |
| :--- | :--- |
| `new TokenBurnTransaction()` |     Initializes the TokenBurnTransaction object |

```java
new TokenBurnTransaction()
```

### Methods

| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | [TokenId](token-id.md) | The ID of the token to burn supply | Required |
| `setTokenAmount(<amount>)` | long | The number of tokens to burn | Required |

{% tabs %}
{% tab title="Java" %}
```java
//Burn 1,000 tokens
TokenBurnTransaction transaction = new TokenBurnTransaction()
    .setTokenId(newTokenId)
    .setAmount(1000);

//Build the unsigned transaction, sign with the supply private key of the token, submit the transaction to a Hedera network
TransactionId transactionId = transaction.build(client).sign(supplyKey).execute(client);
    
//Request the receipt of the transaction
TransactionReceipt getReceipt = transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
Status transactionStatus = getReceipt.status;

System.out.println("The transaction consensus status is " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Burn 1,000 tokens
const transaction = new TokenBurnTransaction()
    .setTokenId(newTokenId)
    .setAmount(1000)

//Build the unsigned transaction, sign with the supply private key of the token, submit the transaction to a Hedera network
const transactionId = await transaction.build(client).sign(supplyKey).execute(client);
    
//Request the receipt of the transaction
const getReceipt = await transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
const transactionStatus = getReceipt.status;

console.log("The transaction consensus status is " +transactionStatus);
//Version 1.4.2
```
{% endtab %}
{% endtabs %}





