# Dissociate tokens from an account

Disassociates the provided Hedera account from the provided Hedera tokens. This transaction must be signed by the provided account's key. Once the association is removed, no token related operation can be performed to that account. AccountBalanceQuery and AccountInfoQuery will not return anything related to the token that was disassociated.

*  If the provided account is not found, the transaction will resolve to INVALID\_ACCOUNT\_ID.
*  If the provided account has been deleted, the transaction will resolve to ACCOUNT\_DELETED.
*  If any of the provided tokens is not found, the transaction will resolve to INVALID\_TOKEN\_REF.
* If any of the provided tokens has been deleted, the transaction will resolve to TOKEN\_WAS\_DELETED.
* If an association between the provided account and any of the tokens does not exist, the transaction will resolve to TOKEN\_NOT\_ASSOCIATED\_TO\_ACCOUNT.
* If the provided account has a nonzero balance with any of the provided tokens, the transaction will resolve to TRANSACTION\_REQUIRES\_ZERO\_TOKEN\_BALANCES.
* On success, associations between the provided account and tokens are removed.

{% hint style="info" %}
The account is required to have a zero balance of the token you wish disassociates. If a token balance is present, you will receieve a TRANSACTION\_REQUIRES\_ZERO\_TOKEN\_BALANCES error.
{% endhint %}

| Constructor | Description |
| :--- | :--- |
| `new TokenDissociateTransaction()` | Initializes the TokenDissociateTransaction object |

```java
new TokenDissociateTransaction()
```

### Methods

{% tabs %}
{% tab title="V2" %}


| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTokenIds(<tokenId>)` | TokenId | The tokens to be dissociated with the provided account | Required |
| `setAccountId(<accountId>)` | AccountId | The account to be dissociated with the provided tokens | Required |

{% code title="Java" %}
```java
//Disassociate a token from an account
TokenDissociateTransaction transaction = new TokenDissociateTransaction()
    .setAccountId(accountId)
    .setTokenIds(tokenId);
        
//Build the unsigned transaction, sign with the private key of the account that is being dissociated from a token, submit the transaction to a Hedera network
TransactionResponse txResponse = transaction.freezeWith(client).sign(accountKey).execute(client);
    
//Request the receipt of the transaction
TransactionReceipt receipt = txResponse.getReceipt(client);
    
//Obtain the transaction consensus status
Status transactionStatus = receipt.status;

System.out.println("The transaction consensus status is: " +transactionStatus);
//v2.0.1
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Dissociate a token to an account
const transaction = await new TokenDissociateTransaction()
     .setAccountId(accountId)
     .setTokenIds([tokenId])
     .freezeWith(client);

//Sign with the private key of the account that is being associated to a token 
const signTx = await transaction.sign(accountKey);

//Submit the transaction to a Hedera network    
const txResponse = await signTx.execute(client);

//Request the receipt of the transaction
const receipt = await txResponse.getReceipt(client);
    
//Get the transaction consensus status
const transactionStatus = receipt.status;

console.log("The transaction consensus status " +transactionStatus.toString());

//v2.0.5
```
{% endcode %}

{% code title="Go" %}
```go
//Disssociate the token from an account and freeze the unsigned transaction for signing
transaction, err := hedera.NewTokenDissociateTransaction().
		SetAccountID(accountId).
		SetTokenIDs(tokenId).
		FreezeWith(client)

if err != nil {
	panic(err)
}

//Sign with the private key of the account that is being associated to a token, submit the transaction to a Hedera network
txResponse, err = transaction.Sign(accountKey).Execute(client)

if err != nil {
	panic(err)
}

//Get the transaction consensus status
receipt, err = txResponse.GetReceipt(client)

if err != nil {
	panic(err)
}

//Get the transaction consensus status
status := receipt.Status

fmt.Printf("The transaction consensus status is %v\n", status)

//v2.1.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setTokenId(<tokenId>)` | TokenId | The tokens to be dissociated with the provided account | Required |
| `setAccountId(<accountId>)` | AccountId | The account to be dissociated with the provided tokens | Required |

{% code title="Java" %}
```java
//Disassociate a token from an account
TokenDissociateTransaction transaction = new TokenDissociateTransaction()
    .setAccountId(accountId)
    .addTokenId(tokenId);
        
//Build the unsigned transaction, sign with the private key of the account that is being dissociated from a token, submit the transaction to a Hedera network
TransactionId transactionId = transaction.build(client).sign(accountKey).execute(client);
    
//Request the receipt of the transaction
TransactionReceipt getReceipt = transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
Status transactionStatus = getReceipt.status;

System.out.println("The transaction consensus status is: " +transactionStatus);
//Version: 1.2.2
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Disassociate a token from an account
const transaction = new TokenDissociateTransaction()
    .setAccountId(accountId)
    .addTokenId(tokenId);
        
//Build the unsigned transaction, sign with the private key of the account that is being dissociated from a token, submit the transaction to a Hedera network
const transactionId = await transaction.build(client).sign(accountKey).execute(client);
    
//Request the receipt of the transaction
const getReceipt = await transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
const transactionStatus = getReceipt.status;

console.log("The transaction consensus status is: " +transactionStatus);
//Version 1.4.2
```
{% endcode %}
{% endtab %}
{% endtabs %}



