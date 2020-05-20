# Create a smart contract

{% hint style="info" %}
Before you get started with smart contracts consider if the Hedera Consensus Service is better for your use case. For most, it provides greater performance and lower costs. Learn more in the blog series, [Exploring Tokenized Assets on HCS](https://www.hedera.com/blog/exploring-tokenized-assets-on-hedera-consensus-part-1).
{% endhint %}

`ContractCreateTransaction()` creates a new smart contract instance. The ID of the smart contract can be obtained from the record or receipt. The instance will run the bytecode stored in the given file, referenced either by FileID or by the transaction ID of the transaction that created the file. The constructor will be executed using the given amount of gas. Similar to accounts, the instance will exist for autoRenewSeconds and when it is reached the instance will renew itself for another autoRenewSeconds seconds. The associated cryptocurrency account will be charged for each auto-renew period. 

{% hint style="warning" %}
**Solidity Support**  
Hedera smart contracts support Solidity versions up to **v0.5.9**.
{% endhint %}

{% hint style="warning" %}
**Smart Contract State Size**  
Each smart contract has a maximum state size of 1MB which can store up to approximately 16,000 key-value pairs.
{% endhint %}

| Constructor | Description |
| :--- | :--- |
| `ContractCreateTransaction()` | Initializes the ContractCreateTransaction\(\) |

```java
new ContractCreateTransaction()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setAdminKey(<key>)` | [Ed25519PublicKey](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/crypto/ed25519/Ed25519PublicKey.java) | The state of the instance and its fields can be modified arbitrarily if this key signs a transaction to modify it. If this is null, then such modifications are not possible, and there is no administrator that can override the normal operation of this smart contract instance. |
| `setByteCodeFile(<fileId>)` | FileId | The `fileId` of the file that contains the smart contract bytecode |
| `setGas(<gas>)` | long | Gas amount to run the constructor |
| `setInitialBalance(<amount>)` | long | The initial number of tinybars to put into the cryptocurrency account associated with and owned by the smart contract. |
| `setAutoRenewPeriod(<duration>)` | Duration | The period of time in which the smart contract will auto-renew in seconds. Duration type is in seconds. For example, one hour would result in the input value of 3600 seconds. |

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

```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
async function main() {
    const operatorAccount = process.env.OPERATOR_ID;
    const operatorPrivateKey = Ed25519PrivateKey.fromString(process.env.OPERATOR_KEY);

    // `Client.forMainnet()` is provided for connecting to Hedera mainnet
    const client = Client.forTestnet();

    // Defaults the operator account ID and key such that all generated transactions will be paid for
    // by this account and be signed by this key
    client.setOperator(operatorAccount, operatorPrivateKey);


    const smartContract = require("./stateful.json");
    const smartContractByteCode = smartContract.contracts[ "stateful.sol:StatefulContract" ].bin;

    console.log("contract bytecode size:", smartContractByteCode.length, "bytes");

    // First we must upload a file containing the byte code
    const byteCodeFileId = (await (await new FileCreateTransaction()
        .setMaxTransactionFee(new Hbar(3))
        .addKey(operatorPrivateKey.publicKey)
        .setContents(smartContractByteCode)
        .execute(client))
        .getReceipt(client))
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
        .execute(client))
        .getRecord(client);

    const newContractId = record.receipt.getContractId();

    console.log("contract create gas used:", record.getContractCreateResult().gasUsed);
    console.log("contract create transaction fee:", record.transactionFee.asTinybar());
    console.log("contract:", newContractId.toString());

    // Next let's ask for the current message (we set on creation)
    let callResult = await new ContractCallQuery()
        .setContractId(newContractId)
        .setGas(1000) // ~897
        .setFunction("getMessage", null)
        .execute(client);

    console.log("call gas used:", callResult.gasUsed);
    console.log("message:", callResult.getString(0));

    // Update the message
    const getRecord = await (await new ContractExecuteTransaction()
        .setContractId(newContractId)
        .setGas(7000) // ~6016
        .setFunction("setMessage", new ContractFunctionParams()
            .addString("hello from hedera again!"))
        .execute(client))
        // [getReceipt] or [getRecord] waits for consensus before continuing
        //      and will throw an exception
        //      on an error received during that process like INSUFFICENT_GAS
        .getRecord(client);

    console.log("execute gas used:", getRecord.getContractExecuteResult().gasUsed);

    // Next let's ask for the new message
    callResult = await new ContractCallQuery()
        .setContractId(newContractId)
        .setGas(1000) // ~897
        .setFunction("getMessage", null)
        .execute(client);

    console.log("call gas used:", callResult.gasUsed);
    console.log("message:", callResult.getString(0));

    client.close();
}

main();
```
{% endtab %}
{% endtabs %}

