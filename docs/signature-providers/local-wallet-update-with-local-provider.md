# Local Wallet (Update with local provider)

{% hint style="info" %}
This feature is available in the Hedera JavaScript SDK only. (version >2.12.0).
{% endhint %}

Using the LocalWallet class, you do not need to hardcode the account and private key information in your code. This can be used for development and testing purposes. For production, use wallet providers offered by the community wallets.

The `LocalWallet()` requires the following variables to be defined in the `.env` file. The `.env` file is located in the root directory of the project.

* `OPERATOR_ID`
  * The wallet account ID in 0.0.x format (ex: 0.0.10)
* `OPERATOR_KEY`
  * The wallet private key
* `HEDERA_NETWORK`
  * The network the wallet submits transactions to

{% code title=".env" %}
```
//Example .env file
OPERATOR_ID= 0.0.x
OPERATOR_KEY= 302e020100300506032b6570042204202cc589a6343ff8d05b71edf54f69bff4cd8faeec9b04d16f55d1d78fe23841af
HEDERA_NETWORK= previewnet/testnet/mainnet (select one network)
```
{% endcode %}

## class LocalWallet implements Wallet&#x20;

### Constructor

#### &#x20;new <mark style="color:purple;">`LocalWallet()`</mark>

Instantiates the LocalWallet object. The local wallet is built using the `OPERATOR_ID`, `OPERATOR_KEY`, and `HEDERA_NETWORK` network specified in the .env file.&#x20;

### Methods

#### **`LocalWallet.`**<mark style="color:purple;">**`accountId`**</mark><mark style="color:purple;">** **</mark><mark style="color:purple;">**->**</mark>** AccountId**

Returns the account ID of the local wallet.

#### **`LocalWallet.`**<mark style="color:purple;">**`getAccountBalance()`**</mark><mark style="color:purple;">** **</mark><mark style="color:purple;">**->**</mark>** Promise \<AccountBalance>**

Returns the account balance of the account in the local wallet.

#### **`LocalWallet.`**<mark style="color:purple;">**`getAccountInfo()`**</mark><mark style="color:purple;">** **</mark><mark style="color:purple;">**->**</mark>** Promise \<AccountInfo>**

Returns the account information of the account in the local wallet.

#### **`LocalWallet.`**<mark style="color:purple;">**`getAccountRecords()`**</mark><mark style="color:purple;">** **</mark><mark style="color:purple;">**->**</mark>** Promise \<AccountInfo>**

Returns the last transaction records for this account using `TransactionRecordQuery`.

#### **`LocalWallet.`**<mark style="color:purple;">**`getAccountKey()`**</mark><mark style="color:purple;">**->**</mark>** Key**

Returns the key on the account in the local wallet.

#### **`LocalWallet.`**<mark style="color:purple;">**`getLedgerId()`**</mark><mark style="color:purple;">**->**</mark>** LedgerId**

Returns the ledger ID (`previewnet`, `testnet`, or `mainnet`).&#x20;

#### **`LocalWallet.`**<mark style="color:purple;">**`getMirrorNetwork()`**</mark><mark style="color:purple;">**->**</mark>** string**

The mirror network the wallet is connected to.

#### **`LocalWallet.`**<mark style="color:purple;">**`getNetwork()`**</mark><mark style="color:purple;">**->**</mark>** \[key: string]: string | **<mark style="color:purple;">****</mark>** AccountId**

Returns the network map information.

#### **`LocalWallet.`**<mark style="color:purple;">**`getProvider()`**</mark><mark style="color:purple;">**->**</mark>** Provider**

Returns the `LocalProvider` which allows you to execute requests.

#### `LocalWallet.`<mark style="color:purple;">`checkTransaction(Transaction: transaction)`</mark><mark style="color:purple;">**->**</mark>** Promise\<Transaction>**

Determines if all the properties required are set and sets the transaction ID. If the transaction ID was already set it checks if the account ID of it is the same as the users.

#### `LocalWallet.`<mark style="color:purple;">`populateTransaction(Transaction: transaction)`</mark><mark style="color:purple;">**->**</mark>** Promise\<Transaction>**

Sets the transaction ID of the transaction to the current account ID of the signer.

**`LocalWallet.`**<mark style="color:purple;">**`sign (`**</mark>**`messages: Uint8Array[]`**<mark style="color:purple;">**`)`**</mark><mark style="color:purple;">**->**</mark>**  `Promise<SignerSignature[]>`**

Sign a list of messages.

**NOTE**: Each element in the outer list of the result is all the signatures for the message at the same index.

**`LocalWallet`**<mark style="color:purple;">**`.signTransaction`**</mark><mark style="color:purple;">** **</mark><mark style="color:purple;">**(**</mark>** `transaction`: `Transaction` **<mark style="color:purple;">**)->**</mark>**  `Promise<Transaction>`**

Signs the transaction.

**NOTE**: Use `Transaction.getSignatures()` to see the actual signatures. message at the same index.

#### Local Wallet Example:

```javascript
require("dotenv").config();
const {LocalWallet} = require("@hashgraph/sdk");

async function main() {

    const wallet = new LocalWallet();
    
    const accountId = wallet.accountId;
    console.log("The wallet account ID " + accountId);

    const balance = wallet.getAccountBalance();
    console.log("The wallet account balance " + balance);

    const accountKey = wallet.getAccountKey();
    console.log("The wallet account key " + accountKey);

    const ledgerId = wallet.getLedgerId();
    console.log("The wallet ledgerId " + ledgerId);
}

main();
```

#### Sign with Local Wallet Example:

```javascript
require("dotenv").config();
const {LocalWallet, Signer, LocalProvider, TransferTransaction} = require("@hashgraph/sdk");

async function main() {

    const wallet = new LocalWallet();

    //Transfer 1 hbar from my wallet account to account 0.0.3
    const transaction = await new TransferTransaction()
        .addHbarTransfer(wallet.getAccountId(), -1)
        .addHbarTransfer("0.0.3", 1)
        .freezeWithSigner(wallet);
    
    //Sign the transaction
    const signTransaction = await transaction.signWithSigner(wallet);

    //Submit the transaction
    const response = await signTransaction.executeWithSigner(wallet);

    //Get the receipt
    const receipt = await wallet.getProvider().waitForReceipt(response);
    
    console.log(`status: ${receipt.status.toString()}`);
}

main();
```
