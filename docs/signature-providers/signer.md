# Signer

{% hint style="info" %}
This feature is available in the Hedera JavaScript SDK only. (version >2.12.0).
{% endhint %}

The **Signer** class is abstract and cannot be directly instantiated. It is used by the wallet developers. Instead use one of the concrete&#x20;

## abstract class Signer

### **Methods**

<mark style="color:purple;">**`sign (`**</mark>**` ``messages: Uint8Array[]`**<mark style="color:purple;">**`)`**</mark><mark style="color:purple;">**->**</mark>**  `Promise<SignerSignature[]>`**

Signs a list of messages.

**NOTE**: Each element in the outer list of the result is all the signatures for the message at the same index.

<mark style="color:purple;">**`signTransaction`**</mark><mark style="color:purple;">** **</mark><mark style="color:purple;">**(**</mark>** `transaction`: `Transaction` **<mark style="color:purple;">**)->**</mark>**  `Promise<Transaction>`**

Signs the transaction.

**NOTE**: Use `Transaction.getSignatures()` to see the actual signatures. message at the same index.

<mark style="color:purple;">**`sendRequest`**</mark><mark style="color:purple;">** **</mark><mark style="color:purple;">**(**</mark>**  `request`: `Executable` **<mark style="color:purple;">**)->**</mark>**  `Response` **<mark style="color:red;">**(REMOVE)**</mark>

Sign and send a request using the wallet.

<mark style="color:purple;">**`checkTransaction`**</mark><mark style="color:purple;">** **</mark><mark style="color:purple;">**(**</mark>**  `transaction`: `Transaction`  **<mark style="color:purple;">**)->**</mark>**  `Promise<Transaction>`**

Determines if all the properties required are set and sets the transaction ID. If the transaction ID was already set it checks if the account ID of it is the same as the users.

<mark style="color:purple;">**`populateTransaction`**</mark><mark style="color:purple;">** **</mark><mark style="color:purple;">**(**</mark>** `transaction`: `Transaction`  **<mark style="color:purple;">**)->**</mark>**  `Promise<Transaction>`**

Sets the transaction ID of the transaction to the current account ID of the signer.

<mark style="color:purple;">**`getLedgerId()`**</mark><mark style="color:purple;">**->**</mark>**  `LedgerId`**

Returns the ledger ID.

<mark style="color:purple;">**`getAccountId()`**</mark><mark style="color:purple;">**->**</mark>**`AccountId`**

Returns the account ID associated with this signer.

<mark style="color:purple;">**`getAccountBalance()`**</mark><mark style="color:purple;">**->**</mark>**  `Promise<AccountBalance>`**

Returns the account balance.

<mark style="color:purple;">**`getAccountInfo`**</mark><mark style="color:purple;">**()->**</mark>**  `Promise<AccountInfo>`**

Returns the account info.

<mark style="color:purple;">**`getAccountRecords`**</mark><mark style="color:purple;">**()->**</mark>**  `Promise<TransactionRecord[]>`**

Fetch the last transaction records for this account using `TransactionRecordQuery`.

<mark style="color:purple;">**`call(`**</mark>**`<RequestT, ResponseT, OutputT>(request: Executable<RequestT, ResponseT, OutputT>`**<mark style="color:purple;">**`)`**</mark><mark style="color:purple;">**->**</mark>**  `Promise <Output>`**

`<enter description>`

