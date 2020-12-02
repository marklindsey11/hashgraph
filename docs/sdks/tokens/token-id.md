# Token ID

Constructs a `TokenId`.

| Constructor | Description |
| :--- | :--- |
| `new TokenId(<shard>,<realm>,<token>)` | Initializes the TokenId object |

```java
new TokenId()
```

### Methods

{% tabs %}
{% tab title="V2" %}


| Method | Type | Description |
| :--- | :--- | :--- |
| `TokenId.fromtString(<tokenId>)` | String | Constructs a token ID from a String value |
| `TokenId.fromSolidityAddress(<address>)` | String | Contructs a token ID from a solidity address |
| `TokenId.fromBytes(<bytes>)` | byte\[ | Constructs a token ID from bytes  |

{% code title="Java" %}
```java
TokenId tokenId = new TokenId(0,0,5);
System.out.println(tokenId);

TokenId tokenIdFromString = TokenId.fromString("0.0.3");
System.out.println(tokenIdFromString);

//Version: 2.0.1
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
const tokenId = new TokenId(0,0,5);
console.log(tokenId.toString());

const tokenIdFromString =  TokenId.fromString("0.0.3");
console.log(tokenIdFromString.toString())

//Version 2.0.7
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Method | Type | Description |
| :--- | :--- | :--- |
| `TokenId.fromtString(<tokenId>)` | String | Constructs a token ID from a String value |
| `TokenId.fromSolidityAddress(<address>)` | String | Contructs a token ID from a solidity address |

```java
TokenId newTokenId =  TokenId.fromString("0.0.3");
//Version: 1.2.2
```

```javascript
const tokenId = new TokenId(0,0,5);
console.log(tokenId);

const tokenIdFromString =  TokenId.fromString("0.0.3");
console.log(tokenIdFromString)
//Version 1.4.1
```
{% endtab %}
{% endtabs %}





