# Append to a file

`FileAppendTransaction()` appends content to the end of an existing file.

| Constructor | Description |
| :--- | :--- |
| `FileAppendTransaction()` | Initializes the FileAppendTransaction object |

```java
new FileAppendTransaction()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setFileId(<fileId>)` | FileId | The `fileId` of the file to append content to |
| `setContents(<content>)` | byte\[ \] | The content to append in byte format |

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

// Appends the content to the end of the file
TransactionId appendToFileTx = new FileAppendTransaction()
    .setFileId(newFileId)
    .setContents(("This is the appended content to the file ").getBytes())
    .execute(client);
    
// Get file contents
byte[] appendContents = new FileContentsQuery()
    .setFileId(newFileId)
    .execute(client);
    
// Prints query results to console
System.out.println("File content query results: " + new String(appendContents));
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

  // Create a new file with contents
  const transactionId = await new FileCreateTransaction()
    .setContents("Hello, Hedera's file service!")
    .addKey(operatorPublicKey) // Defines the "admin" of this file
    .setMaxTransactionFee(new Hbar(15))
    .execute(client);

  // Get the new file ID by requesting the receipt
  const receipt = await transactionId.getReceipt(client); 
  const fileId = receipt.getFileId(); 
  console.log("new file id = ", fileId);

  //Get file contents
  const fileContents = await new FileContentsQuery()
    .setFileId(fileId)
    .execute(client);


  console.log(`file contents: ${new TextDecoder().decode(fileContents)}`)

  // Append contents to the file
  const fileAppendTransactionId = await new FileAppendTransaction()
    .setFileId(receipt.getFileId())
    .setContents(" The appended contents at the end!") 
    .execute(client);

  // Request to the receipt to make sure the file update before requesting the new contents 
  const appendReceipt = await fileAppendTransactionId.getReceipt(client);
  console.log(`Transaction Status: ${appendReceipt.status}`)

  // Get the updated file contents
  const fileContentsAppend = await new FileContentsQuery()
    .setFileId(fileId)
    .execute(client);
  
  // Print the file contents to the console
  console.log(`file contents: ${new TextDecoder().decode(fileContentsAppend)}`)
}
```
{% endtab %}
{% endtabs %}

