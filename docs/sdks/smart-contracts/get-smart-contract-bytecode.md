# Get smart contract bytecode

`ContractByteCodeQuery()` returns the bytecode for a smart contract instance.

| Constructor | Description |
| :--- | :--- |
| `ContractByteCodeQuery()` | Initalizes a ContractByteCodeQuery object |

```java
new ContractByteCodeQuery()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setContractId(<contractId>)` | ContractId | The ID for the contract for which the bytecode is requested |

## Example

{% tabs %}
{% tab title="Java" %}
```java
ClassLoader cl = CreateStatefulContract.class.getClassLoader();

Gson gson = new Gson();

JsonObject jsonObject;

try (InputStream jsonStream = cl.getResourceAsStream("stateful.json")) {
    if (jsonStream == null) {
        throw new RuntimeException("failed to get stateful.json");
    }

    jsonObject = gson.fromJson(new InputStreamReader(jsonStream), JsonObject.class);
}

String byteCodeHex = jsonObject.getAsJsonPrimitive("object")
    .getAsString();
byte[] byteCode = byteCodeHex.getBytes();

// `Client.forMainnet()` is provided for connecting to Hedera mainnet
Client client = Client.forTestnet();

// Defaults the operator account ID and key such that all generated transactions will be paid for
// by this account and be signed by this key
client.setOperator(OPERATOR_ID, OPERATOR_KEY);

// default max fee for all transactions executed by this client
client.setMaxTransactionFee(new Hbar(100));
client.setMaxQueryPayment(new Hbar(10));

// create the contract's bytecode file
TransactionId fileTxId = new FileCreateTransaction()
    // Use the same key as the operator to "own" this file
    .addKey(OPERATOR_KEY.publicKey)
    .setContents(byteCode)
    .execute(client);

TransactionReceipt fileReceipt = fileTxId.getReceipt(client);
FileId newFileId = fileReceipt.getFileId();

System.out.println("contract bytecode file: " + newFileId);

TransactionId contractTxId = new ContractCreateTransaction()
    .setBytecodeFileId(newFileId)
    .setGas(100_000_000)
    .setConstructorParams(
        new ContractFunctionParams()
            .addString("hello from hedera!"))
    .execute(client);

TransactionReceipt contractReceipt = contractTxId.getReceipt(client);
ContractId newContractId = contractReceipt.getContractId();

System.out.println("new contract ID: " + newContractId);

byte [] byteCodeQuery = new ContractBytecodeQuery()
    .setContractId(newContractId)
    .execute(client);

System.out.println("Length " + byteCodeQuery.length);


```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const byteCodeQuery = new ContractBytecodeQuery()
    .setContractId(newContractId)
    .execute(client);
```
{% endtab %}
{% endtabs %}

