# Approve an allowance

{% hint style="info" %}
This feature is available on previewnet. API subject to change.&#x20;
{% endhint %}

A transaction that allows a token owner to delegate a token spender to spend the specified token amount on behalf of the token owner. An owner can provide a token allowance for hbars, non-fungible and fungible tokens. The owner is the account that owns the tokens and grants the allowance to the spender. The spender is the account that spends tokens authorized by the owner from the owners account. The spender pays for the transaction fees when transferring tokens from the owners account to another recipient.&#x20;

There are two ways this API can be used:

* You can set the owner account ID in the transaction
* You can omit the owner account ID in the transaction and it will default to the caller of the transaction. This means that account paying for the transaction fee is represented as the owner account

The total number of approvals in this transaction cannot exceed 20. Note that each NFT serial number counts as a single approval, hence a transaction granting 20 serial numbers to a spender will use all of the approvals permitted for the transaction.&#x20;

An account can have a total of 100 allowances. Each NFT serial counts as an allowance.

You can request an [account info](get-account-info.md) to view all spender accounts for a given owner.

**Transaction Fees**

* Please see the transaction and query [fees](../../../mainnet/fees/#transaction-and-query-fees) table for base transaction fee
* Please use the [Hedera fee estimator](https://hedera.com/fees) to estimate your transaction fee cost

**Transaction Signing Requirements**

* If the owner account is specified, the transaction needs to be signed by the owner account key and the transaction fee payer key. If the owner account key and transaction fee payer key are the same only one signature is required.
* If the owner account is not specified then the transaction fee payer account must be the owner account. The owner account key is required to sign the transaction.&#x20;

| **Constructor**                            | **Description**                                           |
| ------------------------------------------ | --------------------------------------------------------- |
| `new AccountAllowanceApproveTransaction()` | Initializes the AccountAllowanceApproveTransaction object |

### Methods

| **Method**                                                                             | **Type**                                                                                                                                                                           | **Description**                                                                                                                                                                                                                                                         |
| -------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `addHbarAllowance(<spenderAccountId>, <amount>)`                                       | [AccountId](../specialized-types.md#accountid), [Hbar](../hbars.md)                                                                                                                | The spender account and amount of hbar the allowance is approved for. If `amount` is 0 the transaction will remove the `spender`’s allowance from the owner’s account, thereby freeing an allowance for future use.                                                     |
| `addHbarAllowanceWithOwner(<spenderAccountId>, <amount>, <ownerAccountId>)`            | [AccountId](../specialized-types.md#accountid), [Hbar](../hbars.md), [AccountId](../specialized-types.md#accountid)                                                                | The spender account ID, amount of hbar, and the owner account ID. If `amount` is 0 the transaction will remove the `spender`’s allowance from the owner’s account, thereby freeing an allowance for future use.                                                         |
| `addTokenAllowance(<tokenId>,<spenderAccountId>, <amount>)`                            | <p><a href="../tokens/token-id.md">TokenId</a>, <br><a href="../specialized-types.md#accountid">AccountId</a>, long</p>                                                            | The spender account the allowance is approved for, the specified token, and the token amount being approved by the owner. If `amount` is 0 the transaction will remove the `spender`’s allowance from the owner’s account, thereby freeing an allowance for future use. |
| `addTokenAllowanceWithOwner(<tokenId>,<spenderAccountId>, <amount>, <ownerAccountId>)` | <p><a href="../tokens/token-id.md">TokenId</a>, <br><a href="../specialized-types.md#accountid">AccountId</a>, long, <a href="../specialized-types.md#accountid">AccountId</a></p> | The spender account the allowance is approved for, the specified token, the token amount, and owner account ID. If `amount` is 0 the transaction will remove the `spender`’s allowance from the owner’s account, thereby freeing an allowance for future use.           |
| `addTokenNftAllowance(<nftId>, <spenderAccountId>)`                                    | [nftId](../tokens/nft-id.md), [AccountId](../specialized-types.md#accountid)                                                                                                       | The specific NFT the spender account is being approved for.                                                                                                                                                                                                             |
| `addTokenNftAllowanceWithOwner(<nftId>, <spenderAccountId>, <ownerAccountId>)`         | <p><a href="../tokens/nft-id.md">nftId</a>, <a href="../specialized-types.md#accountid">AccountId</a>,<br><a href="../specialized-types.md#accountid">AccountId</a></p>            | The specific NFT the spending account is approved for.                                                                                                                                                                                                                  |
| `addAllTokenNftAllowance(<tokenId>,<spenderAccountId>)`                                | [TokenId](../tokens/token-id.md), [AccountId](../specialized-types.md#accountid)                                                                                                   | The class of NFTs the spending account is approved for. This approves the spender to spend all NFTs in a given token class.                                                                                                                                             |
| `addAllTokenNftAllowanceWithOwner(<tokenId>,<spenderAccountId>, <ownerAccountId>)`     | <p><a href="../tokens/token-id.md">TokenId</a>, <a href="../specialized-types.md#accountid">AccountId</a>,<br><a href="../specialized-types.md#accountid">AccountId</a></p>        | The class of NFTs the spending account is approved for. This approves the spender to spend all NFTs in a given token class.                                                                                                                                             |



{% tabs %}
{% tab title="Java" %}
```java
//Create the transaction
AccountAllowanceApproveTransaction transaction = new AccountAllowanceApproveTransaction()
    .addHbarAllowanceWithOwner(spenderAccountId, Hbar.from(100), ownerAccountId);

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
    .addHbarAllowanceWithOwner(spenderAccountId, Hbar.from(100), ownerAccountId);
    
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
     AddHbarAllowance(spenderAccountId, Hbar.fromTinybars(100), ownerAccountId)
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

