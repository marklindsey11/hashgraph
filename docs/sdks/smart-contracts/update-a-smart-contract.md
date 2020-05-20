# Update a smart contract

`ContractUpdateTransaction()` updates an existing smart contract instance to the given parameter values. Any null field is left unchanged.

| Constructor | Description |
| :--- | :--- |
| `ContractUpdateTransaction()` | Initializes the ContractUpdateTransaction object |

```java
new ContractUpdateTransaction()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setContractId(<contractId>)` | ContractId | The contract ID instance to update |
| `setFileId(<fileId>)` | FileId | The file ID of file containing the smart contract bytecode |
| `setAdminKey(<key>)` | [Ed25519PublicKey](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/crypto/ed25519/Ed25519PublicKey.java) | The state of the instance can be modified arbitrarily if this key signs a transaction to modify it. If this is null, then such modifications are not possible, and there is no administrator that can override the normal operation of this smart contract instance. |
| `setAutoRenewPeriod(<duration>)` | Duration | The instance will charge its account every this many seconds to renew for this long. Duration type is in seconds. For example, one hour duration would result in the value of 3,600 seconds. |
| `setExpirationTime(<expiration>)` | Instant | Extend the expiration of the instance and its account to this time. |
| `setProxyAccount(<accountId>)` | AccountId | ID of the account to which this account is proxy staked. |

## Example

{% tabs %}
{% tab title="Java" %}
```java
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

TransactionId contractUpdatetxId = new ContractUpdateTransaction()
     .setContractId(newContractId)
     .setContractMemo("Update the memo of the smart contract")
     .execute(client);
        
TransactionReceipt contractUpdateResult = contractUpdatetxId.getReceipt(client);

if (contractUpdateResult.status != Status.Success) {
    System.out.println("error updating contract: " + contractUpdateResult.status);
   return;
System.out.println("Contract successfully updated");
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const updateContract = new ContractUpdateTransaction()
     .setContractId(newContractId)
     .setContractMemo("Update the memo of the smart contract")
     .execute(client);
```
{% endtab %}
{% endtabs %}

