# Mint a token

Minting tokens allows you to increase the total supply of the token. The Supply Key must sign the transaction. If no Supply Key is defined, the transaction will resolve to TOKEN\_HAS\_NO\_SUPPLY\_KEY. The maximum total supply a token can have is 2^63-1. The amount provided must be in the lowest denomination possible. Example: Token A has 2 decimals. In order to mint 100 tokens, one must provide amount of 10000. In order to mint 100.55 tokens, one must provide amount of 10055.

| Constructor | Description |
| :--- | :--- |
| `new TokenMintTransaction()` | Initializes a TokenMintTransaction object |

```java
new TokenMintTransaction()
```

### Methods

| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | The token for which to mint tokens | Required |
| `setAmount(<amount>)` | long | The amount to mint to the Treasury Account. Amount must be a positive non-zero number represented in the lowest denomination of the token. The new supply must be lower than 2^63. | Required |

{% tabs %}
{% tab title="Java" %}
```java
//Mint another 1,000 tokens
TokenMintTransaction transaction = new TokenMintTransaction()
    .setTokenId(newTokenId)
    .setAmount(1000);

Status transactionStatus = transaction.build(client) //Build the unsigned transaction
    .sign(supplyKey) //Sign with the supply private key of the token
    .execute(client) //Submit the transaction to a Hedera network
    .getReceipt(client) //Request the receipt of the transaction
    .status; //Return the consensus status of the transaction

System.out.println("The transaction consensus status is " +transactionStatus);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Mint another 1,000 tokens
const transaction = await new TokenMintTransaction()
    .setTokenId(newTokenId)
    .setAmount(1000);

const transactionStatus = await (await (await transaction.build(client) //Build the unsigned transaction
    .sign(supplyKey) //Sign with the supply private key of the token
    .execute(client)) //Submit the transaction to a Hedera network
    .getReceipt(client)) //Request the receipt of a transaction
    .status; //Return the consensus status of the transaction

console.log("The transaction consensus status is " +transactionStatus);
//Version 1.4.1
```
{% endtab %}
{% endtabs %}





