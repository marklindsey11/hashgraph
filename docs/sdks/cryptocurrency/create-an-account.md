# Create an account

The account represents your account specific to the Hedera network. Accounts are required to utilize the Hedera network services and to pay network transaction fees. 

{% hint style="info" %}
When creating a **new account** an existing account will need to fund the initial balance and pay for the transaction fee.
{% endhint %}

| Constructor | Description |
| :--- | :--- |
| `AccountCreateTransaction()` | Initializes the AccountCreateTransaction object |

```java
new AccountCreateTransaction()
```

## Basic

| Method | Type | Description |
| :--- | :---: | :--- |
| `setKey(<key>)` | Ed25519 | The public key generated for the new account. |
| `setInitialBalance(<initialBalance>)` | Hbar/long | Set the initial balance of the account, transferred from the operator account, in tinybar. |

### Example:

{% tabs %}
{% tab title="Java" %}
```java
Transaction tx = new AccountCreateTransaction()
     // The only _required_ property here is `key`
     .setKey(newKey.PublicKey())
     .setInitialBalance(1000)
     .setMaxTransactionFee(Hbar.fromTinybar(1000))
     .build(client);

tx.execute(client);

// This will wait for the receipt to become available
TransactionReceipt receipt = tx.getReceipt(client);

AccountId newAccountId = receipt.getAccountId();

System.out.println("account = " + newAccountId);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { Client, Ed25519PrivateKey, AccountCreateTransaction } = require("@hashgraph/sdk");
require("dotenv").config();

async function main() {
    const operatorPrivateKey = process.env.OPERATOR_KEY;
    const operatorAccount = process.env.OPERATOR_ID;

    if (operatorPrivateKey == null || operatorAccount == null) {
        throw new Error("environment variables OPERATOR_KEY and OPERATOR_ID must be present");
    }

    const client = new Client({
        network: { "0.testnet.hedera.com:50211": "0.0.3" },
        operator: {
            account: operatorAccount,
            privateKey: operatorPrivateKey
        }
    });

    const privateKey = await Ed25519PrivateKey.generate();

    console.log("Automatic signing example");
    console.log(`private = ${privateKey.toString()}`);
    console.log(`public = ${privateKey.publicKey.toString()}`);

    const transactionId = await new AccountCreateTransaction()
        .setKey(privateKey.publicKey)
        .setInitialBalance(0)
       // .setGenerateRecord Available in the JS SDK but not in the JAVA SDK
        .execute(client);

    const transactionReceipt = await transactionId.getReceipt(client);
    const newAccountId = transactionReceipt.getAccountId();

    console.log(`account = ${newAccountId}`);
    }
main();
```
{% endtab %}
{% endtabs %}

## Advanced

<table>
  <thead>
    <tr>
      <th style="text-align:left">Methods</th>
      <th style="text-align:center">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>setAutoRenewPeriod(&lt;autoRenewPeriod&gt;)</code>
      </td>
      <td style="text-align:center">Duration</td>
      <td style="text-align:left">
        <p>The period of time in which the account will auto-renew in seconds. The
          account is charged tinybars for every auto-renew period. Duration type
          is in seconds. For example, one hour would result in the input value of
          3,600 seconds.NOTE: This is fixed to approximately 3 months (7890000 seconds).
          Any other value will return the following error: AUTORENEW_DURATION_NOT_IN_RANGE.</p>
        <p><em>default: 2,592,000 seconds</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setReceiverSignatureRequired(&lt;booleanValue&gt;)</code>
      </td>
      <td style="text-align:center">boolean</td>
      <td style="text-align:left">
        <p>If true, all the account keys must sign any transaction depositing into
          this account (in addition to all withdrawals)</p>
        <p><em>default: false</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setReceiveRecordThreshold(&lt;receiveRecordThreshold&gt;)</code>
      </td>
      <td style="text-align:center">Hbar/long</td>
      <td style="text-align:left">
        <p>Creates a record for any transaction that deposits more than x value of
          tinybars.
          <br />
        </p>
        <p>Note: You will incur a charge each time the record is generated.</p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setSendRecordThreshold(&lt;sendRecordThreshold&gt;)</code>
      </td>
      <td style="text-align:center">Hbar/long</td>
      <td style="text-align:left">
        <p>Creates a record for any transaction that withdraws more than x value
          of tinybars.</p>
        <p></p>
        <p>Note: You will incur a charge each time the record is generated.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setProxyAccount(&lt;accountId&gt;)</code>
      </td>
      <td style="text-align:center">AccountID</td>
      <td style="text-align:left">ID of the account to which this account is proxy staked</td>
    </tr>
  </tbody>
</table>