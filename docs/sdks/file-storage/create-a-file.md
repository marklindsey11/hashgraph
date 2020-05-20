# Create a file

`FileCreateTransaction()` creates a new file. The file is referenced by its file ID which can be obtained from the receipt or record of the transaction. The file does not have a file name. If the file is too big to create with a single `FileCreateTransaction()`, the file can be appended with the remaining content multiple times using the `FileAppendTransaction()` constructor.

| Constructor | Description |
| :--- | :--- |
| `FileCreateTransaction` | Initializes the FileCreateTransaction object |

```java
new FileCreateTransaction()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `addKey(<key>)` | [Ed25519PublicKey](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/crypto/ed25519/Ed25519PublicKey.java) | The public key of the owner of the file |
| `setContents(<contents>)` | bytes\[\] | The file contents |
| `setExpirationTime(<expiration>)` | Instant | The time at which this file should expire \(unless FileUpdateTransaction is used before then to extend its life\) |

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
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const { Client, FileCreateTransaction, Ed25519PrivateKey, Hbar } = require("@hashgraph/sdk");
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
}

main();
```
{% endtab %}
{% endtabs %}

