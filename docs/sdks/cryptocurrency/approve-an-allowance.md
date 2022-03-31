# Approve an allowance

{% hint style="info" %}
This feature is available on previewnet. API subject to change.&#x20;
{% endhint %}

A transaction that allows a token owner to delegate a token spender to spend the specified token amount on behalf of the token owner. An owner can provide a token allowance for hbars, non-fungible and fungible tokens. The owner is the account that owns the tokens and grants the allowance to the spender. The spender is the account that spends tokens authorized by the owner from the owners account. The spender pays for the transaction fees when transferring tokens from the owners account to another recipient.&#x20;

The total number of approvals in this transaction cannot exceed 20. Note that each NFT serial number counts as a single approval, hence a transaction granting 20 serial numbers to a spender will use all of the approvals permitted for the transaction.&#x20;

An account can have a total of 100 allowances. Each NFT serial counts as an allowance.

You can request an [account info](get-account-info.md) to view all spender accounts for a given owner account.

**Transaction Fees**

* Please see the transaction and query [fees](../../../mainnet/fees/#transaction-and-query-fees) table for base transaction fee
* Please use the [Hedera fee estimator](https://hedera.com/fees) to estimate your transaction fee cost

**Transaction Signing Requirements**

* If the owner account is specified, the transaction needs to be signed by the owner account key and the transaction fee payer key. If the owner account key and transaction fee payer key are the same only one signature is required.
* If the owner account is not specified then the transaction fee payer account must be the owner account. The owner account key is required to sign the transaction.&#x20;

**Reference:** [HIP-336](https://github.com/hashgraph/hedera-improvement-proposal/blob/master/HIP/hip-336.md)

| **Constructor**                            | **Description**                                           |
| ------------------------------------------ | --------------------------------------------------------- |
| `new AccountAllowanceApproveTransaction()` | Initializes the AccountAllowanceApproveTransaction object |

### Methods

| **Method**                                                                           | **Type**                                                                                                                                                                                   | **Description**                                                                                                                                                                               |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `approveHbarAllowance(<ownerAccountId>,<spenderAccountId>, <amount>)`                | [AccountId](../specialized-types.md#accountid), [AccountId](../specialized-types.md#accountid), [Hbar](../hbars.md)                                                                        | The owner account ID that is authorizing the allowance, the spender account ID to authorize, the amount of hbar the owner account is authorizing the spender account to use.                  |
| `approveTokenAllowance(<tokenId>,<ownerAccountId>,<spenderAccountId>, <amount>)`     | <p><a href="../tokens/token-id.md">TokenId</a>, <br><a href="../specialized-types.md#accountid">AccountId</a>, </p><p><a href="../specialized-types.md#accountid">AccountId</a>, long</p>  | The token ID of the token being granted an allowance by the spender account, the account ID of the owner account, the account ID of the spender account.                                      |
| `approveTokenNftAllowance(<nftId>,<ownerAccountId>, <spenderAccountId>)`             | <p><a href="../tokens/nft-id.md">nftId</a>, <a href="../specialized-types.md#accountid">AccountId</a>,<br><a href="../specialized-types.md#accountid">AccountId</a></p>                    | The NFT ID of the NFT being granted an allowance by the owner account, the account ID of the owner account, the account ID of the spender account.                                            |
| `approveTokenNftAllowanceAllSerials(<tokenId>,<ownerAccountId>, <spenderAccountId>)` | <p><a href="../tokens/token-id.md">TokenId</a>, <br><a href="../specialized-types.md#accountid">AccountId</a>,  <br><a href="../specialized-types.md#accountid">AccountId</a>, </p><p></p> | Grant a spender account access to all NFTs in a given token class/collection. The token ID of the NFT collection, the account ID of the owner account, the account ID of the spender account. |



{% tabs %}
{% tab title="Java" %}
```java
//Create the transaction
AccountAllowanceApproveTransaction transaction = new AccountAllowanceApproveTransaction()
    .approveHbarAllowance(ownerAccount, spenderAccountId, Hbar.from(100));

//Sign the transaction with the owner account key and the transaction fee payer key (client)  
TransactionResponse txResponse = transaction.freezeWith(client).sign(ownerAccountKey).execute(client);

//Request the receipt of the transaction
TransactionReceipt receipt = txResponse.getReceipt(client);

//Get the transaction consensus status
Status transactionStatus = receipt.status;

System.out.println("The transaction consensus status is " +transactionStatus);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Create the transaction
const transaction = new AccountAllowanceApproveTransaction()
    .approveHbarAllowance(ownerAccount, spenderAccountId, Hbar.from(100));
    
//Sign the transaction with the owner account key
const signTx = await transaction.sign(ownerAccountKey);

//Sign the transaction with the client operator private key and submit to a Hedera network
const txResponse = await signTx.execute(client);

//Request the receipt of the transaction
const receipt = await txResponse.getReceipt(client);

//Get the transaction consensus status
const transactionStatus = receipt.status;

console.log("The transaction consensus status is " +transactionStatus.toString());
```
{% endtab %}

{% tab title="Go" %}
```go
//Create the transaction
transaction := hedera.NewAccountAllowanceApproveTransaction().
     ApproveHbarAllowance(ownerAccount, spenderAccountId, Hbar.fromTinybars(100), ownerAccountId)
        FreezeWith(client)

if err != nil {
    panic(err)
}

//Sign the transaction with the owner account private key   
txResponse, err := transaction.Sign(ownerAccountKey).Execute(client)

//Request the receipt of the transaction
receipt, err := txResponse.GetReceipt(client)
if err != nil {
    panic(err)
}

//Get the transaction consensus status
transactionStatus := receipt.Status

println("The transaction consensus status is ", transactionStatus)
```
{% endtab %}
{% endtabs %}

