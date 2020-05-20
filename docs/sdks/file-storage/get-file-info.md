# Get file info

`FileInfoQuery()` returns all the information related to the file. If a file has expired, there will be no information to retrieve.

| Constructor | Description |
| :--- | :--- |
| `FileInfoQuery()` | Initializes the FileInfoQuery object |

```java
new FileInfoQuery()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setFileId(<fileId>)` | FileId | The `fileId` of the file to return information for |

## Example

{% tabs %}
{% tab title="Java" %}
```java
// `Client.forMainnet()` is provided for connecting to Hedera mainnet
Client client = Client.forTestnet();

// Defaults the operator account ID and key such that all generated transactions will be paid for
// by this account and be signed by this key
client.setOperator(OPERATOR_ID, OPERATOR_KEY);

// The file is required to be a byte array,
// you can easily use the bytes of a file instead.
byte[] fileContents = "Hedera hashgraph is great!".getBytes();

TransactionId txId = new FileCreateTransaction()
    // Use the same key as the operator to "own" this file
    .addKey(OPERATOR_KEY.publicKey)
    .setContents(fileContents)
    // The default max fee of 1 HBAR is not enough to make a file ( starts around 1.1 HBAR )
    .setMaxTransactionFee(200_000_000) // 2 HBAR
    .execute(client);

TransactionReceipt receipt = txId.getReceipt(client);
FileId newFileId = receipt.getFileId();

System.out.println("file: " + newFileId);

FileInfo info = new FileInfoQuery()
    .setFileId(newFileId)
    .execute(client);

System.out.println(info.size);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { Client, FileCreateTransaction, Ed25519PrivateKey, Hbar, FileInfoQuery } = require("@hashgraph/sdk");
require("dotenv").config();

async function main() {
  
  const operatorAccount = process.env.OPERATOR_ID;
  const operatorPrivateKey = Ed25519PrivateKey.fromString(process.env.OPERATOR_KEY);
  const operatorPublicKey = operatorPrivateKey.publicKey;

  if (operatorPrivateKey == null || operatorAccount == null) {
    throw new Error(
      "environment variables OPERATOR_KEY and OPERATOR_ID must be present"
    );
  }

  const client = Client.forTestnet()
  client.setOperator(operatorAccount, operatorPrivateKey);

  const transactionId = await new FileCreateTransaction()
    .setContents("Hello, Hedera's file service!")
    .addKey(operatorPublicKey) // Defines the "admin" of this file
    .setMaxTransactionFee(new Hbar(15))
    .execute(client);

  const receipt = await transactionId.getReceipt(client);  
  console.log("new file id = ", receipt.getFileId());

  const fileInfo = await new FileInfoQuery()
    .setFileId(receipt.getFileId())
    .execute(client);

  console.log(fileInfo.size);
}

main();
```
{% endtab %}
{% endtabs %}

