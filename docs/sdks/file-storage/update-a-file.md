# Update a file

`FileUpdateTransaction()` updates the metadata for a file. This transaction must be signed by all the keys assigned to the file.

| Constructor | Description |
| :--- | :--- |
| `FileUpdateTransaction()` | Intializes the FileUpdateTransaction object |

```java
new FileUpdateTransaction()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setFileId(<fileId>)` | FileId | The FileID of the file to update |
| `addKey(<key>)` | [Ed25519PublicKey](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/crypto/ed25519/Ed25519PublicKey.java) | The public key\(s\) to add to update the file with |
| `setContents(<contents>)` | byte\[ \] | The contents to update the file with |
| `setExpirationTime(<expiration>)` | Instant | The new expiration time  |

## Example

{% tabs %}
{% tab title="Java" %}
```java
// `Client.forMainnet()` is provided for connecting to Hedera mainnet
Client client = Client.forTestnet();

// Defaults the operator account ID and key such that all generated transactions will be paid for
// by this account and be signed by this key
client.setOperator(OPERATOR_ID, OPERATOR_KEY);

// Content to be stored in the file
byte[] fileContents = ("Hedera is great!").getBytes();

// Create the new file and set its properties
TransactionId newFileTxId = new FileCreateTransaction()
    .addKey(OPERATOR_KEY.publicKey) // The public key of the owner of the file
    .setContents(fileContents) // Contents of the file
    .setMaxTransactionFee(new Hbar(2))
    .execute(client);

FileId newFileId = newFileTxId.getReceipt(client).getFileId();

//Print the file ID to console
System.out.println("The new file ID is " + newFileId.toString());

// Get file contents
byte[] contents = new FileContentsQuery()
    .setFileId(newFileId)
    .execute(client);

// Prints query results to console
System.out.println("File content query results: " + new String(contents));

TransactionId updateFileTx = new FileUpdateTransaction()
    .setFileId(newFileId)
    .setContents(("This is the updated content to the file ").getBytes())
    .execute(client);

byte[] updateContents = new FileContentsQuery()
    .setFileId(newFileId)
    .execute(client);
    
System.out.println("File content query results: " + new String(updateContents));
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
async function main() {

    const operatorAccount = process.env.OPERATOR_ID;
    const operatorPrivateKey = Ed25519PrivateKey.fromString(process.env.OPERATOR_KEY);
    const operatorPublicKey = operatorPrivateKey.publicKey;

    if (operatorPrivateKey == null || operatorAccount == null) {
     throw new Error(
          "environment variables OPERATOR_KEY and OPERATOR_ID must be present"
     );
    }
    // `Client.forMainnet()` is provided for connecting to Hedera mainnet
    const client = Client.forTestnet()

    // Defaults the operator account ID and key such that all generated transactions will be paid for
    // by this account and be signed by this key   
    client.setOperator(operatorAccount, operatorPrivateKey);

    // Create a file with contents
    const transactionId = await new FileCreateTransaction()
        .setContents("Hello, Hedera's file service!")
        .addKey(operatorPublicKey) // Defines the "admin" of this file
        .setMaxTransactionFee(new Hbar(15))
        .execute(client);

    // Grabt the file ID from the receipt 
    const receipt = await transactionId.getReceipt(client); 
    const fileId = receipt.getFileId(); 
    console.log("new file id = ", fileId);

    //Get file contents
    const fileContents = await new FileContentsQuery()
        .setFileId(fileId)
        .execute(client);

    // Print the contents to the console
    console.log(`file contents: ${new TextDecoder().decode(fileContents)}`)

    // Update the file with new contents
    // Updating the file will replace the existing contents
    const fileUpdateTransactionId = await new FileUpdateTransaction()
        .setFileId(fileId)
        .setContents("You updated the file!")
        .execute(client);

    // Make sure the file update with the new contents before retreiving the contents
    const updateReceipt = await fileUpdateTransactionId.getReceipt(client);
    console.log(`Status: ${updateReceipt.status}`)

    // Get the new file contents
    const fileContentsUpdate = await new FileContentsQuery()
     .setFileId(fileId)
     .execute(client);

    // Print the updated file contents to the console
    console.log(`new file contents: ${new TextDecoder().decode(fileContentsUpdate)}`)

}

main();
```
{% endtab %}
{% endtabs %}

