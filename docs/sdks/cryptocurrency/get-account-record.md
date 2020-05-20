# Get account record

`AccountRecordsQuery()` gets all of the records for an account for transfers into and out, that were above the threshold limit that is set by the user, during the last 24 hours. The query response includes the header and account ID. The header can return the cost of the transaction, the state proof or both. The account ID is the account the record is for.

A record returns the following information about an account:

* Account ID
* Transaction ID
* Receipt 
* Consensus Timestamp
* Transaction Hash
* Memo \(if any\)
* Transaction Fee

| Constructor | Description |
| :--- | :--- |
| `AccountRecordsQuery()` | Initializes the AccountRecordsQuery object |

```java
new AccountRecordsQuery()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setAccountId(<accountId>)` | AccountId | The accountId of the account to return the record for |

## Example

{% tabs %}
{% tab title="Java" %}
```java
CryptoGetAccountRecordsResponse accountRecord = new AccountRecordsQuery()
     .setAccountId(accountId)
     .execute(client);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const accountRecord = await new AccountRecordsQuery()
    .setAccountId(accountId)
    .execute(client);
```
{% endtab %}
{% endtabs %}

