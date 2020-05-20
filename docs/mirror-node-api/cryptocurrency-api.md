---
description: >-
  The mirror node REST API offers the ability to query cryptocurrency
  transactions and account information from a Hedera managed mirror node. This
  REST API is only available for whitelisted partners
---

# REST API

{% hint style="danger" %}
For our whitelisted partners, you may use the following root endpoints:  
[https://testnet.mirrornode.hedera.com](https://testnet.mirrornode.hedera.com/)  
[https://mainnet.mirrornode.hedera.com](https://mainnet.mirrornode.hedera.com/)  
  
For all other users, you may check out [DragonGlass](https://app.dragonglass.me/hedera/home) and [Kabuto](https://kabuto.sh/) as alternatives.‌
{% endhint %}

## Accounts <a id="accounts"></a>

The **accounts** object represents the information associated with an account and returns a list of account information.‌

Account IDs take the following format: **0.0.&lt;account number&gt;**.‌

Example: 0.0.1000‌

Account IDs can also take the account number as an input value. For example, for account ID 0.0.1000, the number 1000 can be specified in the request.

{% api-method method="get" host="" path=" /api/v1/accounts" %}
{% api-method-summary %}
accounts
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{account ID}" type="string" %}
Returns information for a specific account ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="account.id" type="string" required=false %}
The ID of the account to return account information for
{% endapi-method-parameter %}

{% api-method-parameter name="account.balance" type="number" %}
Returns a list of account IDs that have the specified balance
{% endapi-method-parameter %}

{% api-method-parameter name="account.publickey" type="string" %}
Returns the account information for the specified public key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "accounts": [
        {
            "balance": {
                "timestamp": "1568420100.066845000",
                "balance": 628318531
            },
            "account": "0.0.1",
            "expiry_timestamp": null,
            "auto_renew_period": null,
            "key": null,
            "deleted": null,
            "entity_type": "account"
        }
    ],
    "links": {
        "next": "/api/v1/accounts?limit=1&account.id=gt:0.0.1"
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Response Details <a id="response-details"></a>

| Response Item | Description |
| :--- | :--- |
| **accounts** | The list of information returned for all accounts |
| **balance** | The timestamp and account balance of the account |
| **account** | The ID of the account |
| **expiry timestamp** | The expiry date for the entity as set by a create or update transaction |
| **auto renew period** | The period in which the account autorenews |
| **key** | The key associated with the account |
| **deleted** | Whether the account was deleted or not \(Boolean\) |
| **entity type** | The type of Hedera service: account, file, or contract |
| **links.next** | Hyperlink to the next page of results |

### Optional Filtering <a id="optional-filtering"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left">Operator</th>
      <th style="text-align:left">Example</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>lt</code> (less than)</td>
      <td style="text-align:left"><code>/api/v1/accounts?account.id=lt:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns account IDs less then 1000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>lte</code> (less than or equal to)</td>
      <td style="text-align:left"><code>/api/v1/accounts?account.id=lte:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns account IDs less than or equal to 1000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>gt</code> (greater than)</td>
      <td style="text-align:left"><code>/api/v1/accounts?account.id=gt:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns account IDs greater than 1000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>gte</code> (greater than or equal to)</td>
      <td style="text-align:left"><code>/api/v1/accounts?account.id=gte:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns account IDs greater than or equal to 1000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>order</code> (order <code>asc</code> or <code>desc</code> values)</td>
      <td
      style="text-align:left">
        <p><code>/api/v1/accounts?order=asc</code>
        </p>
        <p>&#x200B;</p>
        <p><code>/api/v1/accounts?order=desc</code>
        </p>
        </td>
        <td style="text-align:left">
          <p>Returns account information in ascending order</p>
          <p>Returns account information in descending order</p>
        </td>
    </tr>
  </tbody>
</table>### Addtional Examples <a id="addtional-examples"></a>

| Example Requests | Description |
| :--- | :--- |
| `/api/v1/accounts?account.id=0.0.1001` | Returns the account information of account 1001 |
| `/api/v1/accounts?account.balance=gt:1000` | Returns all account information that have a balance greater than 1000 tinybars |
| `/api/v1/accounts?account.publickey=2b60955bcbf0cf5e9ea880b52e5b63f664b08edf6ed 15e301049517438d61864` | Returns all account information for 2b60955bcbf0cf5e9ea880b52e5b63f664b08edf6ed15e301049517438d61864 public key |

## Balances <a id="balances"></a>

The **balance** object represents the balance of accounts on the Hedera network. You can retrieve this to view the **most recent** balance of all the accounts on the network at that given time. The balances object returns the account ID and the balance in hbars. Balances are checked on a periodic basis and thus return the most recent snapshot of time captured prior to the request.

{% api-method method="get" host="" path=" /api/v1/balances" %}
{% api-method-summary %}
balances
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="account.id" type="string" required=false %}
The ID of the account to return the balance for
{% endapi-method-parameter %}

{% api-method-parameter name="account.balance" type="number" required=false %}
Returns a list of account IDs that have the specified balance \(tinybars\)
{% endapi-method-parameter %}

{% api-method-parameter name="timestamp" type="string" required=false %}
The timestamp the user would like to return account balances for. The timestamp can be provided in seconds format \(15000000000\) or in seconds.nanoseconds \(15000000000.010000000\).
{% endapi-method-parameter %}

{% api-method-parameter name="account.publickey" type="string" required=false %}
Returns the balance object for a specific public key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "timestamp": "1568420100.066845000",
    "balances": [
        {
            "account": "0.0.16316",
            "balance": 500005000
        },
        {
            "account": "0.0.16315",
            "balance": 500005000
        },
        {
            "account": "0.0.16314",
            "balance": 500005000
        },
        {
            "account": "0.0.16313",
            "balance": 500005000
        },
        {
            "account": "0.0.16312",
            "balance": 500005000
        }
    ],
    "links": {
        "next": "/api/v1/balances?limit=5&account.id=lt:0.0.16312"
    }
}

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Response Details <a id="response-details-1"></a>

| Response Item | Description |
| :--- | :--- |
| **timestamp** | The seconds.nanoseconds of the timestamp at which the list of balances for each account are returned |
| **balances** | List of balances for each account |
| **account** | The ID of the account |
| **balance** | The balance of the account |
| **links.next** | Hyperlink to the next page of results |

### Optional Filtering <a id="optional-filtering-1"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left">Operator</th>
      <th style="text-align:left">Example</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>lt</code> (less than)</td>
      <td style="text-align:left"><code>/api/v1/balances?account.id=lt:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns the balances of account IDs less than 1,000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>lte</code> (less than or equal to)</td>
      <td style="text-align:left"><code>/api/v1/balances?account.id=lte:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns the balances account IDs less than or equal to 1,000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>gt</code> (greater than)</td>
      <td style="text-align:left"><code>/api/v1/balances?account.id=gt:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns the balances of account IDs greater than to 1,000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>gte</code> (greater than or equal to)</td>
      <td style="text-align:left"><code>/api/v1/balances?account.id=gte:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns the balances of account IDs greater than or equal to 1,000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>order</code> (order <code>asc</code> or <code>desc</code> values)</td>
      <td
      style="text-align:left">
        <p><code>/api/v1/balances?order=asc</code>
        </p>
        <p>&#x200B;</p>
        <p><code>/api/v1/balances?order=desc</code>
        </p>
        </td>
        <td style="text-align:left">
          <p>Lists balances in ascending order</p>
          <p>&#x200B;</p>
          <p>Lists balances in descending order</p>
        </td>
    </tr>
  </tbody>
</table>### Additional Examples <a id="additional-examples"></a>

| Example Requests | Description |
| :--- | :--- |
| `/api/v1/balances?account.id=0.0.1000` | Returns balance for account ID 1,000 |
| `/api/v1/balances?account.balance=gt:1000` | Returns all account IDs that have a balance greater than 1000 tinybars |
| `/api/v1/balances?timestamp=1566562500.040961001` | Returns all account balances referencing the latest snapshot that occured prior to 1566562500 seconds and 040961001 nanoseconds |
| `/api/v1/balances?account.publickey=2b60955bcbf0cf5e9ea880b52e5b6 3f664b08edf6ed15e301049517438d61864` | Returns balance information for 2b60955bcbf0cf5e9ea880b52e5b63f664b08edf6ed 15e301049517438d61864 public key |

## Transactions <a id="transactions"></a>

The **transaction** object represents the transactions processed on the Hedera network. You can retrieve this to view the transaction metadata information including transaction id, timestamp, transaction fee, transfer list, etc. If a transaction was submitted to multiple nodes, the successful transaction and duplicate transaction\(s\) will be returned as separate entries in the response with the same transaction ID. Duplicate transactions will still be assessed [network fees](https://www.hedera.com/fees).

{% api-method method="get" host="" path="/api/v1/transactions" %}
{% api-method-summary %}
transactions
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="account.id" type="string" required=false %}
The ID of the account the user would like to return transactions for within the transferlist.
{% endapi-method-parameter %}

{% api-method-parameter name="timestamp" type="string" required=false %}
The specific timestamp the user would like to return transactions for
{% endapi-method-parameter %}

{% api-method-parameter name="result" type="string" required=false %}
If `result=fail`l the query returns all failed cryptocurrency transactions  
If the `result=success` the query returns all successful cryptocurrency transactions
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=false %}
If `type=credit` the query returns all transactions that deposited into an account ID  
If `type=debit` the query returns all transactions that withdrew from an account ID
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "transactions":[
        {
            "consensus_timestamp":"1568542824.686097000",
            "valid_start_timestamp":"1568542814.468848000",
            "charged_tx_fee":85828,
            "memo_base64":"aGFzaC1oYXNoLmluZm8=",
            "result":"SUCCESS",
            "name":"CRYPTOTRANSFER",
            "max_fee":"184000",
            "valid_duration_seconds":"120",
            "node":"0.0.3",
            "transaction_id":"0.0.995-1568542814-468848000",
            "transfers":[
                {
                    "account":"0.0.3",
                    "amount":84000
                },
                {
                    "account":"0.0.3",
                    "amount":3091
                },
                {
                    "account":"0.0.98",
                    "amount":880
                },
                {
                    "account":"0.0.98",
                    "amount":81857
                },
                {
                    "account":"0.0.995",
                    "amount":-84000
                },
                {
                    "account":"0.0.995",
                    "amount":-880
                },
                {
                    "account":"0.0.995",
                    "amount":-84948
                }
            ]
        }
    ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Response Details <a id="response-details-2"></a>

| Response Item | Description |
| :--- | :--- |
| **consensus timestamp** | The consensus timestamp in seconds.nanoseconds |
| **valid start timestamp** | The time the transaction is valid |
| **charged tx fee** | The transaction fee that was charged for that transaction |
| **transaction id** | The ID of the transaction |
| **memo base64** | The memo attached to the transaction encoded in Base64 format |
| **result** | Whether the cryptocurrency transaction was successful or not |
| **name** | The type of transaction |
| **max fee** | The maximum transaction fee the client is willing to pay |
| **valid duration seconds** | The seconds for which a submitted transaction is to be deemed valid beyond the start time. The transaction is invalid if consensusTimestamp is greater than transactionValidStart + valid\_duration\_seconds. |
| **node** | The ID of the node that submitted the transaction to the network |
| **transfers** | A list of the account IDs the crypto transfer occurred between and the amount that was transferred. A negative \(-\) sign indicates a debit to that account. The transfer list includes the transfers between the from account and to account, the transfer of the [node fee](https://www.hedera.com/fees), the transfer of the [network fee](https://www.hedera.com/fees), and the transfer of the [service fee](https://www.hedera.com/fees) for that transaction. If the transaction was not processed, a [network fee](https://www.hedera.com/fees) is still assessed. |
| **links.next** | A hyperlink to the next page of responses |

### Optional Filtering <a id="optional-filtering-2"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left">Operator</th>
      <th style="text-align:left">Example</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>lt</code> (less than)</td>
      <td style="text-align:left"><code>/api/v1/transactions?account.id=lt:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns account.id transactions less than 1,000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>lte</code> (less than or equal to)</td>
      <td style="text-align:left"><code>/api/v1/transactions?account.id=lte:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns account.id transactions less than or equal to 1,000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>gt</code> (greater than)</td>
      <td style="text-align:left"><code>/api/v1/transactions?account.id=gt:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns account.id transactions greater than 1,000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>gte</code> (greater than or equal to)</td>
      <td style="text-align:left"><code>api/v1/transactions?account.id=gte:0.0.1000</code>
      </td>
      <td style="text-align:left">Returns account.id transactions greater than or equal to 1,000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>order</code> (order <code>asc</code> or <code>desc</code> values)</td>
      <td
      style="text-align:left">
        <p><code>/api/v1/transactions?order=asc</code>
        </p>
        <p>&#x200B;</p>
        <p><code>/api/v1/transactions?order=desc</code>
        </p>
        </td>
        <td style="text-align:left">
          <p>Lists transactions in ascending order Lists transactions descending order</p>
          <p>&#x200B;</p>
        </td>
    </tr>
  </tbody>
</table>**Note**: It is recommended that the **account.id** query should not select no more than 1000 accounts in a query. If the range specified in the query results in selecting more than 1000 accounts, the API will automatically only search for the first 1000 accounts that match the query in the database and return the transactions for those. For example, if you use `?account.id=gt:0.0.15000` or if you use`?account.id=gt:0.0.15000&account.id=lt:0.0.30000`, then the API will only return results or some 1000 accounts in this range that match the rest of the query filters.‌

A single transaction can also be returned by specifying the transaction ID in the request. If a transaction was submitted to multiple nodes, the response will return entries for the successful transaction along with separate entries for the duplicate transaction\(s\). The "result" key indicates "success" for the node that processed the transaction and "DUPLICATE\_TRANSACTION" for each additional node submission. Duplicate entries are still charged network fees.

| Parameter | Description |
| :--- | :--- |
| `{transaction_ID}` | A specific transaction can be returned by specifying a transaction ID |

### Additional Examples <a id="additional-examples-1"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left">Example Request</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>/api/v1/transactions/?account.id=0.0.1000</code>
      </td>
      <td style="text-align:left">Returns transaction for account ID 1,000</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/api/v1/transactions?timestamp=1565779209.711927001</code>
      </td>
      <td style="text-align:left">Returns transactions at 1565779209 seconds and 711927001 nanoseconds</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/api/v1/transactions?result=fail</code>
      </td>
      <td style="text-align:left">Returns all transactions that have failed</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>/api/v1/transactions?account.id=0.0.13622&amp;type=credit</code>  <code>/api/v1/transactions?account.id=0.0.13622&amp;type=debit</code>
      </td>
      <td style="text-align:left">
        <p>Returns all transactions that deposited into an account ID 0.0.13622</p>
        <p>&#x200B;</p>
        <p>Returns all transactions that withdrew from account ID 0.0.13622
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>{% api-method method="get" host="" path="/api/v1/topics/:topicId/messages/" %}
{% api-method-summary %}
topic messages
{% endapi-method-summary %}

{% api-method-description %}
Returns topic messages for a given consensus timestamp
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="sequenceNumber" type="number" required=false %}
The sequence number of the message relative to other messages submitted to the same topic
{% endapi-method-parameter %}

{% api-method-parameter name="topicID" type="string" required=true %}
The ID of the topic in x.y.z or z format
{% endapi-method-parameter %}

{% api-method-parameter name="consensusTimestamp" type="string" required=false %}
The consensus timestamp of a message in seconds.nanoseconds
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

  "responseJson": {
    "consensus_timestamp": "1234567890.000000002",
    "topic_id": "0.0.7",
    "message": "bWVzc2FnZQ==",
    "running_hash": "cnVubmluZ19oYXNo",
    "sequence_number": 2
  }

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Response Details

| Response Item | Description |
| :--- | :--- |
| **consensus\_timestamp** | The consensus timestamp of the message in seconds.nanoseconds |
| **topic\_id** | The ID of the topic the message was submitted to |
| **message** | The content of the message |
| **running\_hash** | The new running hash of the topic that received the message |
| **sequence\_number** | The sequence number of the message relative to all other messages for the same topic |

