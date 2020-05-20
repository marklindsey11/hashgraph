# Get account balance

`AccountBalanceQuery()` returns the current account balance of an account on the Hedera network. 

| Constructor | Description |
| :--- | :--- |
| `AccountBalanceQuery()` | Initializes the AccountBalanceQuery object |

```java
new AccountBalanceQuery()
```

| Method | Type | Description |
| :--- | :--- | :--- |
| `setAccountId(<account>)` | AccountId | The accountId of the account to retrieve the balance for |

## Example

{% tabs %}
{% tab title="Java" %}
```java
// Client.forMainnet()` is provided for connecting to Hedera mainnet
Client client = Client.forTestnet();

// Defaults the operator account ID and key such that all generated transactions will be paid for
// by this account and be signed by this key
client.setOperator(OPERATOR_ID, OPERATOR_KEY);

Hbar balance = new AccountBalanceQuery()
    .setAccountId(OPERATOR_ID)
    .execute(client);

System.out.println("balance = " + balance);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { Client, AccountBalanceQuery } = require("@hashgraph/sdk");

async function main() {
    const operatorPrivateKey = process.env.OPERATOR_KEY;
    const operatorAccount = process.env.OPERATOR_ID;

    if (operatorPrivateKey == null || operatorAccount == null) {
        throw new Error("environment variables OPERATOR_KEY and OPERATOR_ID must be present");
    }

    const client = Client.forTestnet();

    client.setOperator(operatorAccount, operatorPrivateKey);

    const balance = await new AccountBalanceQuery()
        .setAccountId(operatorAccount)
        .execute(client);

    console.log(`${operatorAccount} balance = ${balance.asTinybar()}`);
}

main();
```
{% endtab %}
{% endtabs %}

