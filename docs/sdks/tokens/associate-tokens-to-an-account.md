# Associate tokens to an account

Associates the provided Hedera account with the provided Hedera tokens. Hedera accounts must be associated with a token first before you can transfer tokens to that account. The Hedera account that is being associated to a token is required to sign the transaction.

* If the provided account is not found, the transaction will resolve to INVALID\_ACCOUNT\_ID.
* If the provided account has been deleted, the transaction will resolve to ACCOUNT\_DELETED.
* If any of the provided tokens is not found, the transaction will resolve to INVALID\_TOKEN\_REF.
* If any of the provided tokens has been deleted, the transaction will resolve to TOKEN\_WAS\_DELETED.
* If an association between the provided account and any of the tokens already exists, the transaction will resolve to TOKEN\_ALREADY\_ASSOCIATED\_TO\_ACCOUNT.
* If the provided account's associations count exceed the constraint of maximum token associations per account, the transaction will resolve to TOKENS\_PER\_ACCOUNT\_LIMIT\_EXCEEDED.
* On success, associations between the provided account and tokens are made and the account is ready to interact with the tokens.

| Constructor | Description |
| :--- | :--- |
| `new TokenAssociateTransaction()` | Initializes a TokenAssociateTransaction object |

```java
new TokenAssociateTransaction()
```

### Methods

{% tabs %}
{% tab title="V2" %}


| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `setAccountId(<accountId>)` | AccountId | The account to be associated with the provided tokens | Required |
| `setTokenIds(<tokenId>)` | TokenId | The tokens to be associated with the provided account | Required |

{% code title="Java" %}
```java
//Associate a token to an account
TokenAssociateTransaction transaction = new TokenAssociateTransaction()
        .setAccountId(accountId)
        .setTokenIds(tokenId);

//Freeze the unsigned transaction, sign with the private key of the account that is being associated to a token, submit the transaction to a Hedera network
TransactionResponse txResponse = transaction.freezeWith(client).sign(accountKey).execute(client);
    
//Request the receipt of the transaction
TransactionReceipt receipt = txResponse.getReceipt(client);
    
//Get the transaction consensus status
Status transactionStatus = receipt.status;

System.out.println("The transaction consensus status " +transactionStatus);
//v2.0.1
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Associate a token to an account
const transaction = await new TokenAssociateTransaction()
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
//Asscoiate the token to an account and freeze the unsigned transaction for signing
transaction, err := hedera.NewTokenAssociateTransaction().
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
| `setAccountId(<accountId>)` | AccountId | The account to be associated with the provided tokens | Required |
| `addTokenId(<tokenId>)` | TokenId | The tokens to be associated with the provided account | Required |

{% code title="Java" %}
```java
//Associate a token to an account
TokenAssociateTransaction transaction = new TokenAssociateTransaction()
        .setAccountId(accountId)
        .addTokenId(tokenId);

//Build the unsigned transaction, sign with the private key of the account that is being associated to a token, submit the transaction to a Hedera network
TransactionId transactionId = transaction.build(client).sign(accountKey).execute(client);
    
//Request the receipt of the transaction
TransactionReceipt getReceipt = transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
Status transactionStatus = getReceipt.status;

System.out.println("The transaction consensus status " +transactionStatus);
//Version: 1.2.2
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Associate a token to an account 
const transaction = new TokenAssociateTransaction()
        .setAccountId(accountId)
        .addTokenId(tokenId); //Will change to addTokenId()

//Build the unsigned transaction, sign with the private key of the account that is being associated to a token, submit the transaction to a Hedera network
const transactionId = await transaction.build(client).sign(accountKey).execute(client);
    
//Request the receipt of the transaction
const getReceipt = await transactionId.getReceipt(client);
    
//Obtain the transaction consensus status
const transactionStatus = getReceipt.status;

console.log("The transaction consensus status " +transactionStatus);
//Version 1.4.2
```
{% endcode %}
{% endtab %}
{% endtabs %}



