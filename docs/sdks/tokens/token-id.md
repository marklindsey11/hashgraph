# Token ID

Constructs a `TokenId`.

| Constructor | Description |
| :--- | :--- |
| `new TokenId(<shard>,<realm>,<token>)` | Initializes the TokenCreateTransaction object |

```java
new TokenId()
```

### Methods

| Method | Type | Description |
| :--- | :--- | :--- |
| `TokenId.fromtString(<tokenId>)` | String | Constructs a token ID from a String value |
| `TokenId.fromSolidityAddress(<address>)` | String | Contructs a token ID from a solidity address |

{% tabs %}
{% tab title="Java" %}
```java
TokenId newTokenId =  TokenId.fromString("0.0.3");
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const tokenId = new TokenId(0,0,5);
console.log(tokenId);

const tokenIdFromString =  TokenId.fromString("0.0.3");
console.log(tokenIdFromString)
//Version 1.4.1
```
{% endtab %}
{% endtabs %}





