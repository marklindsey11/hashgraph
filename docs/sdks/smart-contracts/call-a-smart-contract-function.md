# Call a smart contract function

`ContractCallQuery()` calls a function from a smart contract instance without updating its state or requiring consensus.

| Constructor | Description |
| :--- | :--- |
| `ContractCallQuery()` | Initializes a ContractCallQuery object |

```java
new ContractCallQuery()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setContractId(<contractId>)` | ContractId | The ID of the contract instance to call |
| `setGas(<gas>)` | long | Gas amount to run the constructor |
| `setFunctionParameters(<parameters>)` | byte \[ \] | Which funtion to call from the contract instance and the parameters |
| `setFunction(<functionName>)` | String | The name of the function in String format |
| `setMaxResultSize(<size>)` | long | Max number of bytes that the result might include. The run will fail if it would have returned more than this number of bytes. |

## Example

{% tabs %}
{% tab title="Java" %}
```java
ClassLoader cl = CreateSimpleContract.class.getClassLoader();

Gson gson = new Gson();

JsonObject jsonObject;

try (InputStream jsonStream = cl.getResourceAsStream("hello_world.json")) {
    if (jsonStream == null) {
        throw new RuntimeException("failed to get hello_world.json");
    }

    jsonObject = gson.fromJson(new InputStreamReader(jsonStream), JsonObject.class);
}

String byteCodeHex = jsonObject.getAsJsonPrimitive("object")
    .getAsString();

// `Client.forMainnet()` is provided for connecting to Hedera mainnet
Client client = Client.forTestnet();

// Defaults the operator account ID and key such that all generated transactions will be paid for
// by this account and be signed by this key
client.setOperator(OPERATOR_ID, OPERATOR_KEY);
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

ContractFunctionResult contractCallResult = new ContractCallQuery()
    .setContractId(newContractId)
    .setGas(1000)
    .setFunction("get_message")
    .execute(client);

if (contractCallResult.errorMessage != null) {
    System.out.println("error calling contract: " + contractCallResult.errorMessage);
    return;
}

String message = contractCallResult.getString(0);
System.out.println("contract returned message: " + message);

```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const [ operatorPrivateKey, hederaClient ] = createHederaClient();

const smartContract = require("./stateful.json");
const smartContractByteCode = smartContract.contracts[ "stateful.sol:StatefulContract" ].bin;

console.log("contract bytecode size:", smartContractByteCode.length, "bytes");

// First we must upload a file containing the byte code
const byteCodeFileId = (await (await new FileCreateTransaction()
    .setMaxTransactionFee(new Hbar(3))
    .addKey(operatorPrivateKey.publicKey)
    .setContents(smartContractByteCode)
    .execute(hederaClient))
    .getReceipt(hederaClient))
    .getFileId();

console.log("contract bytecode file:", byteCodeFileId.toString());

// Next we instantiate the contract instance
const record = await (await new ContractCreateTransaction()
    .setMaxTransactionFee(new Hbar(100))
    // Failing to set this to an adequate amount
    // INSUFFICIENT_GAS
    .setGas(2000) // ~1260
    // Failing to set parameters when parameters are required
    // CONTRACT_REVERT_EXECUTED
    .setConstructorParams(new ContractFunctionParams()
        .addString("hello from hedera"))
    .setBytecodeFileId(byteCodeFileId)
    .execute(hederaClient))
    .getRecord(hederaClient);

const newContractId = record.receipt.getContractId();

console.log("contract create gas used:", record.getContractCreateResult().gasUsed);
console.log("contract create transaction fee:", record.transactionFee.asTinybar());
console.log("contract:", newContractId.toString());

// Next let's ask for the current message (we set on creation)
let callResult = await new ContractCallQuery()
    .setContractId(newContractId)
    .setGas(1000) // ~897
    .setFunction("getMessage", null)
    .execute(hederaClient);

console.log("call gas used:", callResult.gasUsed);
console.log("message:", callResult.getString(0));

// Update the message
const getRecord = await (await new ContractExecuteTransaction()
    .setContractId(newContractId)
    .setGas(7000) // ~6016
    .setFunction("setMessage", new ContractFunctionParams()
        .addString("hello from hedera again!"))
    .execute(hederaClient))
    // [getReceipt] or [getRecord] waits for consensus before continuing
    //      and will throw an exception
    //      on an error received during that process like INSUFFICENT_GAS
    .getRecord(hederaClient);

console.log("execute gas used:", getRecord.getContractExecuteResult().gasUsed);

// Next let's ask for the new message
callResult = await new ContractCallQuery()
    .setContractId(newContractId)
    .setGas(1000) // ~897
    .setFunction("getMessage", null)
    .execute(hederaClient);

console.log("call gas used:", callResult.gasUsed);
console.log("message:", callResult.getString(0));

hederaClient.close();
```
{% endtab %}
{% endtabs %}

