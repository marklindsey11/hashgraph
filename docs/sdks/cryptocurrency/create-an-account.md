# Create an account

A transaction that creates a Hedera account. A Hedera account is required to interact with any of the Hedera network services as you need an account to pay for all associated transaction/query fees. You can visit portal.hedera.com to create a previewnet/testnet/mainnet account. To process an account create transaction, you will need an exisiting account to pay for the transaction fee. To obtain the new account ID, request the receipt of the transaction. 

{% hint style="info" %}
When creating a **new account** an existing account will need to pay for the transaction fee to create the account.
{% endhint %}

**Transaction Signing Requirements**

* The account paying for the transaction fee is required to the transaction \(usually client.operator account key\)

**Transaction Properties**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Key</b>
      </td>
      <td style="text-align:left">The key for the new account.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Initial balance</b>
      </td>
      <td style="text-align:left">The initial balance of the account, transferred from the operator account,
        in Hbar</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Receiver signature required</b>
      </td>
      <td style="text-align:left">
        <p>If true, all the account keys must sign any transaction depositing into
          this account (in addition to all withdrawals)</p>
        <p><em>default: false</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Send record threshold</b>
      </td>
      <td style="text-align:left">The new threshold to generate records for transferring hbars out of the
        account<b> </b>[deprecated]</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Receive Record Threshold</b>
      </td>
      <td style="text-align:left">The new threshold to generate records for receiving hbars into the account<b> </b>[deprecated]</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Auto Renew Period</b>
      </td>
      <td style="text-align:left">
        <p>The period of time in which the account will auto-renew in seconds. The
          account is charged tinybars for every auto-renew period. Duration type
          is in seconds. For example, one hour would result in the input value of
          3,600 seconds.
          <br />
          <br /><b>NOTE:</b> This is fixed to approximately 3 months (7890000 seconds).
          Any other value will return the following error: AUTORENEW_DURATION_NOT_IN_RANGE.</p>
        <p><em>default: 2,592,000 seconds</em><b> </b>(DISABLED)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Proxy Account</b>
      </td>
      <td style="text-align:left">ID of the account to which this account is proxy staked <b>(</b>DISABLED)</td>
    </tr>
  </tbody>
</table>

| Constructor | Description |
| :--- | :--- |
| `new AccountCreateTransaction()` | Initializes the AccountCreateTransaction object |

```java
new AccountCreateTransaction()
```

### Methods

{% tabs %}
{% tab title="V2" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setKey(<key>)` | Key | Required |
| `setInitialBalance(<initialBalance>)` | HBar | Optional |
| `setReceiverSignatureRequired(<booleanValue>)` | boolean | Optional |
| `setAutoRenewPeriod(<autoRenewPeriod>)` | Duration | Disabled |
| `setProxyAccount(<accountId>)` | AccountId | Disabled |

{% code title="Java" %}
```java
//Create the transaction
AccountCreateTransaction transaction = new AccountCreateTransaction()
    .setKey(privateKey.getPublicKey())
    .setInitialBalance(new Hbar(1000));

//Submit the transaction to a Hedera network
TransactionResponse txResponse = transaction.execute(client);

//Request the receipt of the transaction
TransactionReceipt receipt = txResponse.getReceipt(client);

//Get the account ID
AccountId newAccountId = receipt.accountId;

System.out.println("The new account ID is " +newAccountId);

//Version 2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create the transaction
const transaction = new AccountCreateTransaction()
    .setKey(privateKey.getPublicKey())
    .setInitialBalance(new Hbar(1000));

//Sign the transaction with the client operator private key and submit to a Hedera network
const txResponse = await transaction.execute(client);

//Request the receipt of the transaction
const receipt = await txResponse.getReceipt(client);

//Get the account ID
const newAccountId = receipt.accountId;

console.log("The new account ID is " +newAccountId);

```
{% endcode %}

{% code title="Go" %}
```go
//Create the transaction
transaction := hedera.NewAccountCreateTransaction().
		SetKey(privateKey.PublicKey()).
		SetInitialBalance(hedera.NewHbar(1000))

//Sign the transaction with the client operator private key and submit to a Hedera network
txResponse, err := AccountCreateTransaction.Execute(client)
if err != nil {
    panic(err)
}

//Request the receipt of the transaction
receipt, err := txResponse.GetReceipt(client)
if err != nil {
    panic(err)
}

//Get the account ID
newAccountId := *receipt.AccountID

fmt.Printf("The new account ID is %v\n", newAccountId)

//Version 2.0.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setKey(<key>)` | Ed25519PubicKey | Required |
| `setInitialBalance(<initialBalance>)` | Hbar/long | Optional |
| `setAutoRenewPeriod(<autoRenewPeriod>)` | Duration | Disabled |
| `setReceiverSignatureRequired(<booleanValue>)` | boolean | Optional |
| `setProxyAccount(<accountId>)` | AccountId | Disabled |

{% code title="Java" %}
```java
//Create the transaction
AccountCreateTransaction transaction = new AccountCreateTransaction()
     .setKey(newPublicKey)
     .setInitialBalance(new Hbar(1));

//Sign with the client operator account private key and submit to a Hedera network
TransactionId txId = transaction.execute(client);

//Request the receipt of the transaction
TransactionReceipt receipt = txId.getReceipt(client);

//Get the new account ID
AccountId newAccountId = receipt.getAccountId();

System.out.println("The new account ID is " +newAccountId);

//v1.3.2
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create the transaction
const transaction = new AccountCreateTransaction()
     .setKey(newPublicKey)
     .setInitialBalance(new Hbar(1));

//Sign with the client operator account private key and submit to a Hedera network
const txId = await transaction.execute(client);

//Request the receipt of the transaction
const receipt = await txId.getReceipt(client);

//Get the new account ID
const newAccountId =  receipt.getAccountId();

System.out.println("The new account ID is " +newAccountId);

//v2.0.0
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### 

## Get transaction values

{% tabs %}
{% tab title="V2" %}
| Method | Type | Description |
| :--- | :--- | :--- |
| `getKey()` | Key | Returns the public key on the account |
| `getInitialBalance()` | Hbar | Returns the initial balance of the account |
| `getAutoRenewPeriod()` | Duration | Returns the auto renew period on the account |
| `getReceiverSignatureRequired()` | boolean | Returns whether the receiver signature is required or not |

{% code title="Java" %}
```java
//Create an account with 1,000 hbar
AccountCreateTransaction transaction = new AccountCreateTransaction()
    // The only _required_ property here is `key`
    .setKey(newKey.getPublicKey())
    .setInitialBalance(new Hbar(1000));

//Return the key on the account
Key accountKey = transaction.getKey();
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create an account with 1,000 hbar
const transaction = new AccountCreateTransaction()
    // The only _required_ property here is `key`
    .setKey(newKey.getPublicKey())
    .setInitialBalance(new Hbar(1000));

//Return the key on the account
const accountKey = transaction.getKey();
```
{% endcode %}

{% code title="Go" %}
```go
//Create an account with 1,000 hbar
AccountCreateTransaction := hedera.NewAccountCreateTransaction().
    SetKey(newKey.PublicKey()).
		SetInitialBalance(hedera.NewHbar(1000))

//Return the key on the account
accountKey, err := AccountCreateTransaction.GetKey()
```
{% endcode %}
{% endtab %}
{% endtabs %}

