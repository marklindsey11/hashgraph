# Burn a token

Burns tokens from the Treasury Account. If no Supply Key is defined, the transaction will resolve to TOKEN\_HAS\_NO\_SUPPLY\_KEY. 

* The operation decreases the Total Supply of the Token. 
* Total supply cannot go below zero. 
* The amount provided must be in the lowest denomination possible. 
* Example: Token A has 2 decimals. In order to burn 100 tokens, one must provide amount of 10000. In order to burn 100.55 tokens, one must provide amount of 10055.

| Constructor | Description |
| :--- | :--- |
| `new TokenBurnTransaction()` |      Initializes the TokenBurnTransaction object |

```java
new TokenBurnTransaction()
```

### Methods

| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | The ID of the token to burn supply | Required |
| `setTokenAmount(<amount>)` | long | The number of tokens to burn | Required |

{% tabs %}
{% tab title="Java" %}
```java
//Burn 1,000 tokens
TokenBurnTransaction transaction = new TokenBurnTransaction()
    .setTokenId(newTokenId)
    .setAmount(1000)

Status transactionStatus = transaction.build(client) //Build the transaction,
    .sign(supplyKey) //Sign with the supply key of the token
    .execute(client) //Submit the transaction to the Hedera network
    .getReceipt(client) //Request the receipt of the transaction
    .status; //Return the consensus status of the transaction

System.out.println("The transaction consensus status is " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Burn 1,000 tokens
const transaction = await new TokenBurnTransaction()
    .setTokenId(newTokenId)
    .setAmount(1000)

const transactionStatus = await (await (await transaction.build(client) //Build the transaction,
    .sign(supplyKey) //Sign with the supply key of the token
    .execute(client)) //Submit the transaction to the Hedera network
    .getReceipt(client)) //Request the receipt of the transaction
    .status; //Return the consensus status of the transaction

console.log("The transaction consensus status is " +transactionStatus);
//Version 1.4.1
```
{% endtab %}
{% endtabs %}





