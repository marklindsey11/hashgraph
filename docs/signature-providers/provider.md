# Provider

{% hint style="info" %}
This feature is available in the Hedera JavaScript SDK only. (version >2.12.0).
{% endhint %}

`Provider` provides access to a Hedera network to which requests should be submitted to. The Hedera network can be specified to `previewnet`, `testnet`, or `mainnet`.

## abstract class Provider

### **Methods**

<mark style="color:purple;">**`getLedgerId()`**</mark><mark style="color:purple;">**->**</mark>**  `LedgerId`**

Returns the ledger ID of the current network.

<mark style="color:purple;">**`getNetwork()`**</mark><mark style="color:purple;">**->**</mark>**  `Map` < `[key: string]: (string | AccountId)`>**

Returns the entire network map for the current network.&#x20;

<mark style="color:purple;">**`getMirrorNetwork()`**</mark><mark style="color:purple;">**->**</mark>**  `List` < `string` >**

Returns the mirror network. The mirror network corresponds with `previewnet`, `testnet`, and `mainnet` mirror node.

**`async`**<mark style="color:purple;">**`getAccountBalance(`**</mark>**`accountId: AccountId`**<mark style="color:purple;">**`)`**</mark><mark style="color:purple;">**->**</mark>**  `Promise<AccountBalance>`**

Get the balance for an account.

**`async`**<mark style="color:purple;">**`getAccountInfo(`**</mark>**`accountId: AccountId`**<mark style="color:purple;">**`)`**</mark><mark style="color:purple;">**->**</mark>**  `Promise<AccountInfo>`**

Get the info for an account.

**`async`**<mark style="color:purple;">**`getAccountRecords(`**</mark>**`accountId: AccountId`**<mark style="color:purple;">**`)`**</mark><mark style="color:purple;">**->**</mark>**  `Promise<TransactionRecord[]>`**

Get the account record.

**`async`**<mark style="color:purple;">**`getTransactionReceipt(`**</mark>**`transactionId:TransactionId`**<mark style="color:purple;">**`)`**</mark>**: `TransactionReceipt`**

Get a receipt for a transaction ID.

**`async`**<mark style="color:purple;">**`sendRequest(`**</mark>**`request: Executable`**<mark style="color:purple;">**`)`**</mark><mark style="color:purple;">**->**</mark>**  `Response` **<mark style="color:red;">**(REMOVE)**</mark>

Sign and send a request using the wallet.

**`async`**<mark style="color:purple;">**`waitForReceipt(`**</mark>**`response: TransactionResponse`**<mark style="color:purple;">**`)`**</mark><mark style="color:purple;">**->**</mark>**  `TransactionReceipt`**

Wait for the receipt for a transaction response.

**`async`**<mark style="color:purple;">**`call(`**</mark>**`<RequestT, ResponseT, OutputT>(request: Executable<RequestT, ResponseT, OutputT>`**<mark style="color:purple;">**`)`**</mark><mark style="color:purple;">**->**</mark>**  `Promise <Output>`**

`<enter description>`

**NOTE**: This is different from `getTransactionReceipt()` this method requires a `nodeId` which is set inside `TransactionResponse` and as a result should not be able to fail with `RECEIPT_NOT_FOUND`

\
