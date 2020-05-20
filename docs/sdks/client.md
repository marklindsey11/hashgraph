# Client



You will need the following pieces of information to construct your Hedera client. 

**User Information**

The operator is the user paying for the transactions fees.  

* **Operator ID:** The account ID of the user paying for the transaction/query fees
* **Operator key:** The private key of the user paying for the transaction/query fees

You can store these variables in a .env file at the root directory of the sdk. Please see the env.sample file in the SDK for how to set this up.

| Constructor | Type | Description |
| :--- | :--- | :--- |
| `Client(<nodes>)` | Map&lt;accountId, string&gt; | Constructs a client object |

```java
new Client()
```

## Basic

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
      <td style="text-align:left"><code>forTestnet()</code>
      </td>
      <td style="text-align:center"></td>
      <td style="text-align:left">Configures a client for Hedera testnet access</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>forMainnet()</code>
      </td>
      <td style="text-align:center"></td>
      <td style="text-align:left">Configures a client for Hedera mainnet access</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>setOperator(&lt;operatorId&gt;, &lt;operatorKey&gt;)</code>
      </td>
      <td style="text-align:center">
        <p>AccountId,</p>
        <p>ED25519PrivateKey</p>
      </td>
      <td style="text-align:left">Defaults the operator account ID and key such that all generated transactions
        will be paid for by this account Id and and signed by this key</td>
    </tr>
  </tbody>
</table>{% tabs %}
{% tab title="Java" %}
```java
// Configures testnet client
Client client = Client.forTestnet()

// Defaults the operator account ID and key such that all generated transactions will be paid for
// by this account and be signed by this key
client.setOperator(OPERATOR_ID, OPERATOR_KEY);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
// Configures testnet client
const client = Client.forTestnet()

// Defaults the operator account ID and key such that all generated transactions will be paid for
// by this account and be signed by this key
client.setOperator(operatorAccount, operatorPrivateKey);
```
{% endtab %}
{% endtabs %}

## Advanced

| Method | Type | Description |
| :--- | :--- | :--- |
| `fromJson(<json>)` | String | Configures a client based off the given JSON string |
| `fromJson(<json>)` | Reader | Configures a client based off the given JSON reader |
| `fromFile(<fileName>)` | String | Configures a client based on a JSON file at the given path |
| `fromFile(<file>)` | File | Configures a client based on a JSON file. |
| `replaceNodes(<nodes>)` | Map&lt;AccountId, String&gt; | Replace all nodes in this Client with a new set of nodes \(e.g. for an Address Book update\). If a node URL for a given account ID is the same, it is not replaced. |
| `setMaxTransactionFee(<fee>)` | long | Set the maximum fee to be paid for transactions executed by this client. The actual fee may be less, but will never be greater than this value. |
| `setMaxTransactionFee(<fee>)` | Hbar | Set the maximum fee to be paid for transactions executed by this client. The actual fee may be less, but will never be greater than this value. |
| `setMaxQueryPayment(<maxQueryPayment>)` | long | Set the maximum default payment value allowable for queries. |
| `setMaxQueryPayment(<maxQueryPayment>)` | Hbar | Set the maximum default payment allowable for queries. |
| `getMaxQueryPayment()` | long | Returns the maximum payment value |
| `getMaxTransactionFee()` | long | Returns the set maximum fee |

{% hint style="warning" %}
The **max transaction fee** and **max query payment** are both set to 100\_000\_000 tinybar \(1 hbar\).  This amount can be modified by using `setMaxTransactionFee()`and `setMaxQueryPayment().`
{% endhint %}

