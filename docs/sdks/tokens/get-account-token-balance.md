# Get account token balance

Get the token balances for a given account. 

{% tabs %}
{% tab title="V2" %}
| Constructor | Description |
| :--- | :--- |
| `new AccountBalanceQuery()` | Initializes the AccountBalanceQuery object |

```java
new AccountBalanceQuery()
```

| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setAccountId(<tokenId>)` | TokenId | Required |

{% code title="Java" %}
```java
//Create the query
AccountBalanceQuery query = new AccountBalanceQuery()
    .setAccountId(accountId);

//Sign with the operator private key and submit to a Hedera network
AccountBalance tokenBalance = query.execute(client);

System.out.println("The token balance(s) for this account: " +tokenBalance.token);

//v2.0.1
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create the query
const query = new AccountBalanceQuery()
    .setAccountId(accountId);

//Sign with the client operator private key and submit to a Hedera network
const tokenBalance = await query.execute(client);

console.log("The token balance(s) for this account: " +tokenBalance.tokens);

//v2.0.7
```
{% endcode %}

{% code title="Go" %}
```go
//Create the query
query := hedera.NewAccountBalanceQuery().
	 SetAccountID(accountId)
	
//Sign with the client operator private key and submit to a Hedera network
tokenbalance, err := query.Execute(client)

if err != nil {
		panic(err)
	}

fmt.Printf("The token balance(s) for this account: %v\n", tokenBalance)

//v2.1.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Constructor | Description |
| :--- | :--- |
| `new TokenBalanceQuery()` | Initializes the TokenBalanceQuery object |

```java
new TokenBalanceQuery()
```

| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setAccountId(<tokenId>)` | TokenId | Required |

{% code title="Java" %}
```java
Map<TokenId, Long> tokenBalance = new TokenBalanceQuery()
    .setAccountId(accountId)
    .execute(client);

System.out.println("The token balance(s) for this account: " +tokenBalance);
//Version: 1.2.2
```
{% endcode %}

{% code title="JavaScript " %}
```javascript
 const tokenBalance = await new TokenBalanceQuery()
    .setAccountId(accountId)
    .execute(client);

console.log("The token balance(s) for this account: " +tokenBalance.get("<tokenId>"));
//Version 1.4.2
```
{% endcode %}
{% endtab %}
{% endtabs %}





