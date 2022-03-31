# Adjust an allowance

{% hint style="info" %}
This feature is available on previewnet. API subject to change.
{% endhint %}

A transaction called by the token owner to increase or decrease the allowance of a spender. Tokens include hbar, fungible and non-fungible tokens.  The token owner can modify multiple allowances in a single transaction. The owner is the account that owns the tokens and grants the allowance to the spender. The spender is the account that spends tokens authorized by the owner from the owners account. The spender pays for the transaction fees when transferring tokens from the owners account to another recipient.&#x20;

You can request an [account info](get-account-info.md) to view all spender accounts for a given owner.

{% hint style="warning" %}
Note: If the `spender` does not have an allowance established with the owner for the specified token and the `amount` is positive, this transaction will implicitly create a new approved allowance for the `spender` for the specified `amount` of tokens.
{% endhint %}

**Transaction Fees**

* Please see the transaction and query [fees](../../../mainnet/fees/#transaction-and-query-fees) table for base transaction fee
* Please use the [Hedera fee estimator](https://hedera.com/fees) to estimate your transaction fee cost

**Transaction Signing Requirements**

* If the owner account is specified, the transaction needs to be signed by the owner account key and the transaction fee payer key. If the owner account key and transaction fee payer key are the same only one signature is required.
* If the owner account is not specified then the transaction fee payer account must be the owner account. The owner account key is required to sign the transaction.&#x20;

**Reference:** [HIP-336](https://github.com/hashgraph/hedera-improvement-proposal/blob/master/HIP/hip-336.md)

| **Constructor**                           | **Description**                                          |
| ----------------------------------------- | -------------------------------------------------------- |
| `new AccountAllowanceAdjustTransaction()` | Initializes the AccountAllowanceAdjustTransaction object |

### Methods



| **Method**                                                                           | **Type**                                                                                                                                                                    | **Description**                                                                                                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `grantHbarAllowance(<ownerAccountId>, <spenderAccountId>, <amount>)`                 | <p><a href="../specialized-types.md#accountid">AccountId</a>, <br><a href="../specialized-types.md#accountid">AccountId</a>, <br><a href="../hbars.md">Hbar</a></p>         | The account and amount of hbar the allowance is being adjusted for. The `amount` must be specified in terms of the `decimals` value for the token. If the addition of `amount` to the `spender`’s current allowance equals 0, the transaction will remove the `spender`’s allowance from the owner’s account, thereby freeing an allowance for future use.               |
| `revokeHbarAllowance(<ownerAccountId>, <spenderAccountId>, <amount>)`                | <p><a href="../specialized-types.md#accountid">AccountId</a>, <br><a href="../specialized-types.md#accountid">AccountId</a>, <br><a href="../hbars.md">Hbar</a></p>         | Revoke the hbar allowance provided to the spender account.                                                                                                                                                                                                                                                                                                               |
| `grantTokenAllowance(<tokenId>,<spenderAccountId>, <amount>)`                        | <p><a href="../tokens/token-id.md">TokenId</a>, <br><a href="../specialized-types.md#accountid">AccountId</a>, long</p>                                                     | The  account the allowance is adjusted for, the specified token and token amount. The `amount` must be specified in terms of the `decimals` value for the token. If the addition of `amount` to the `spender`’s current allowance equals 0, the transaction will remove the `spender`’s allowance from the owner’s account, thereby freeing an allowance for future use. |
| `revokeTokenAllowance(<tokenId>,<spenderAccountId>, <amount>)`                       | <p><a href="../tokens/token-id.md">TokenId</a>, <br><a href="../specialized-types.md#accountid">AccountId</a>, long</p>                                                     | The token the spending account is being revoked from.                                                                                                                                                                                                                                                                                                                    |
| `grantTokenNftAllowance(<nftId>, <ownerAccountId><spenderAccountId>)`                | [nftId](../tokens/nft-id.md), [AccountId](../specialized-types.md#accountid), [AccountId](../specialized-types.md#accountid)                                                | The specific NFT the spending account is being adjusted for.                                                                                                                                                                                                                                                                                                             |
| `revokeTokenNftAllowance(<nftId>, <ownerAccountId><spenderAccountId>)`               | [nftId](../tokens/nft-id.md), [AccountId](../specialized-types.md#accountid), [AccountId](../specialized-types.md#accountid)                                                | The specific NFT the spending account is being revoked for.                                                                                                                                                                                                                                                                                                              |
| `grantTokenNftAllowanceAllSerials`(`<tokenId>,<ownerAccountId>,<spenderAccountId>)`  | <p><a href="../tokens/token-id.md">TokenId</a>, <a href="../specialized-types.md#accountid">AccountId</a>,<br><a href="../specialized-types.md#accountid">AccountId</a></p> | The class of NFTs the spending account is being adjusted for.                                                                                                                                                                                                                                                                                                            |
| `revokeTokenNftAllowanceAllSerials`(`<tokenId>,<ownerAccountId>,<spenderAccountId>)` | <p><a href="../tokens/token-id.md">TokenId</a>, <a href="../specialized-types.md#accountid">AccountId</a>,<br><a href="../specialized-types.md#accountid">AccountId</a></p> | The class of NFTs the spending account will be revoked from.                                                                                                                                                                                                                                                                                                             |

{% tabs %}
{% tab title="Java" %}
```java
//Create the transaction
AccountAllowanceAdjustTransaction transaction = new AccountAllowanceAdjustTransaction()
    .addHbarAllowanceWithOwner(spenderAccountId, Hbar.from(100), ownerAccountId);

//Sign the transaction with the owner account key  
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
const transaction = new AccountAllowanceAdjustTransaction()
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
transaction := hedera.NewAccountAllowanceAdjustTransaction().
     AddHbarAllowanceWithOwner(spenderAccountId, Hbar.fromTinybars(100), ownerAccountId)

if err != nil {
    panic(err)
}

//Sign the transaction with the owner account private key and submit to the network  
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
