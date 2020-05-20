# Get smart contract record

`ContractRecordsQuery()` returns all the records for a smart contract instance, for any function call \(or the constructor call\) during the last 24 hours, for which a record was requested.

| Constructor | Description |
| :--- | :--- |
| `ContractRecordsQuery()` | Initializes the ContractRecordQuery object |

```java
new ContractRecordsQuery()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setContractId(<contractId>)` | ContractId | The ID of the contract to retreive the record for |

## Example

{% tabs %}
{% tab title="Java" %}
```java
new ContractRecordsQuery()
    .setContractId(newContractId)
    .execute(client);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const record = await new ContractRecordsQuery()
    .setContractId(newContractId)
    .execute(client);
    
console.log(record)
```
{% endtab %}
{% endtabs %}

