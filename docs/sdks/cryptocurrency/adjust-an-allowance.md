# Adjust an allowance

{% hint style="info" %}
This feature is available on previewnet.
{% endhint %}

A transaction called by the token owner to increase or decrease the allowance of a spender. Tokens include hbar, fungible and non-fungible tokens.  The token owner can modify multiple allowances in a single transaction. The transaction fee is paid by the owner.

{% hint style="warning" %}
Note: If the `spender` does not have an allowance established with the owner for the specified token and the `amount` is positive, this transaction will implicitly create a new approved allowance for the `spender` for the specified `amount` of tokens.
{% endhint %}

**NFTs**

If the NFT serial number is _positive_ then the NFT will be added to the approved list. Conversely, if the serial number is _negative_ the NFT will be removed from the approved list.

You can view the account allowances for an account by requesting the [account info](get-account-info.md).

**Transaction Signing Requirements:**

* The transaction must be signed by the token owner's account and the account paying for the transaction fee
* If the token owner account and the transaction fee-paying account is the same only one signature is required

| **Constructor**                           | **Description**                                          |
| ----------------------------------------- | -------------------------------------------------------- |
| `new AccountAllowanceAdjustTransaction()` | Initializes the AccountAllowanceAdjustTransaction object |

### Methods



| **Method**                                                  | **Type**                                                                                                                | **Description**                                                                                                                                                                                                                                                                                                                                                         |
| ----------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `addHbarAllowance(<spenderAccountId>, <amount>)`            | [AccountId](../specialized-types.md#accountid), [Hbar](../hbars.md)                                                     | The account and amount of hbar the allowance is approved for. The `amount` must be specified in terms of the `decimals` value for the token. If the addition of `amount` to the `spender`’s current allowance equals 0, the transaction will remove the `spender`’s allowance from the owner’s account, thereby freeing an allowance for future use.                    |
| `addTokenAllowance(<tokenId>,<spenderAccountId>, <amount>)` | <p><a href="../tokens/token-id.md">TokenId</a>, <br><a href="../specialized-types.md#accountid">AccountId</a>, long</p> | The  account the allowance is approved for the specified token and token amount. The `amount` must be specified in terms of the `decimals` value for the token. If the addition of `amount` to the `spender`’s current allowance equals 0, the transaction will remove the `spender`’s allowance from the owner’s account, thereby freeing an allowance for future use. |
| `addTokenNftAllowance(<nftId>, <spenderAccountId>)`         | [nftId](../tokens/nft-id.md), [AccountId](../specialized-types.md#accountid)                                            | The specific NFT the spending account is approved for.                                                                                                                                                                                                                                                                                                                  |
| `addAllTokenNftAllowance(<tokenId>,<spenderAccountId>)`     | [TokenId](../tokens/token-id.md), [AccountId](../specialized-types.md#accountid)                                        | The class of NFTs the spending account is approved for.                                                                                                                                                                                                                                                                                                                 |

{% tabs %}
{% tab title="Java" %}
```java
//Create the transaction
AccountAllowanceAdjustTransaction transaction = new AccountAllowanceAdjustTransaction()
    .addHbarAllowance(spenderAccountId, Hbar.from(100));

//Sign the transaction with the owner account  
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
    .addHbarAllowance(spenderAccountId, Hbar.from(100));

//Sign the transaction with the token owner
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
     AddHbarAllowance(spenderAccountId, Hbar.fromTinybars(10))

if err != nil {
    panic(err)
}

//Sign the transaction with the token owner account private key and submit to the network  
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
