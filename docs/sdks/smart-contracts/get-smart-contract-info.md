# Get smart contract info

`ContractInfoQuery()` returns information about a smart contract instance.

* Account ID \(cryptocurrency account owned by the smart contract instance\)
* Contract ID
* Admin key
* Expiration time
* Number of bytes of storage being used
* Auto renew period
* Memo

| Constructor | Description |
| :--- | :--- |
| `ContractInfoQuery()` | Initializes a ContractCallInfoQuery object |

```java
new ContractInfoQuery()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setContractId(<contractId>)` | ContractId | The ID of the smart contract to return the information for |

## Example

{% tabs %}
{% tab title="Java" %}
```java
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
    .setGas(100000000)
    .setConstructorParams(
        new ContractFunctionParams()
            .addString("hello from hedera!"))
    .execute(client);

TransactionReceipt contractReceipt = contractTxId.getReceipt(client);
ContractId newContractId = contractReceipt.getContractId();

System.out.println("new contract ID: " + newContractId);

ContractInfo getContractInfo = new ContractInfoQuery()
    .setContractId(newContractId)
    .execute(client);

System.out.println("Contract ID is " +getContractInfo.accountId);
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
    console.log(`Transaction status: ${record.receipt.status}`)

    // Get the smart contract info 
    const contractInfo = await new ContractInfoQuery()
        .setContractId(newContractId)
        .execute(client);

     console.log(`The contract auto renew period: ${contractInfo.autoRenewPeriod}`)   

    }

    main();
```
{% endtab %}
{% endtabs %}

