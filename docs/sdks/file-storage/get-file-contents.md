# Get file contents

`FileContentsQuery()` returns the contents of a file. If the file is empty the content field is empty. The response returns the file ID and the file contents in bytes.

| Constructor | Description |
| :--- | :--- |
| `FileContentsQuery()` | Initializes a FileContentQuery object |

```java
new FileContentsQuery()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setAccountId(<account>)` | AccountId | The ID of the file to get contents from |

## Example

{% tabs %}
{% tab title="Java" %}
```java
byte[] fileContents = ("Hedera is great!").getBytes();

// Create the new file and set its properties
TransactionId newFileTxId = new FileCreateTransaction()
    .addKey(OPERATOR_KEY.getPublicKey()) // The public key of the owner of the file
    .setContents(fileContents) // Contents of the file
    .setMaxTransactionFee(200000000) // 2h
    .execute(client);

FileId newFileId = newFileTxId.getReceipt(client).getFileId();

//Print the file ID to console
System.out.println("The new file ID is " + newFileId.toString());

// Get file contents
FileGetContentsResponse contents = new FileContentsQuery()
    .setFileId(newFileId)
    .execute(client);

// Prints query results to console
System.out.println("File content query results: " + contents.getFileContents().getContents().toStringUtf8());
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

}

main();

```
{% endtab %}
{% endtabs %}

