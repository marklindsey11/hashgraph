# Get account token balance

Get the token balances for a given account. 

| Constructor | Description |
| :--- | :--- |
| `new TokenBalanceQuery()` | Initializes the TokenBalanceQuery object |

```java
new TokenBalanceQuery()
```

### Methods

| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setAccountId(<tokenId>)` | TokenId | Required |

{% tabs %}
{% tab title="Java" %}
```java
Map<TokenId, Long> tokenBalance = new TokenBalanceQuery()
    .setAccountId(accountId)
    .execute(client);

System.out.println("The token balance(s) for this account: " +tokenBalance);
//Version: 1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
 const tokenBalance = await new TokenBalanceQuery()
    .setAccountId(accountId)
    .execute(client);

console.log("The token balance(s) for this account: " +tokenBalance);
//Version 1.4.2
```
{% endtab %}
{% endtabs %}





