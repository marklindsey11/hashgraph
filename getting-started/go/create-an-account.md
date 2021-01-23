# Create an account

In this section, you will learn how to make a simple Hedera account. Hedera accounts are the entry  point by which you can interact with the Hedera APIs. Accounts hold a balance of hbars used to pay for API calls for the various transaction and query types.

## Pre-requisites:

{% page-ref page="../introduction.md" %}

{% page-ref page="environment-set-up.md" %}

{% hint style="warning" %}
Note: This example uses **Hedera Go SDK v2.0.** The latest Hedera Go SDK version can be found [here](https://github.com/hashgraph/hedera-sdk-go), however may not be compatible with this tutorial. 
{% endhint %}

## Step 1. Generate keys for the new account

Create keys for the new account. The public key will be associated with the new account and the corresponding private key is used to sign transactions. 

Continue building on the hedera\_examples file from the previous section.

```go
//client := hedera.ClientForTestnet()
//client.SetOperator(myAccountId, myPrivateKey)
//-----------------------<enter code below>--------------------------------------

//Generate new keys for the account you will create
newAccountPrivateKey, err := hedera.GeneratePrivateKey()
if err != nil {
  panic(err)
}

newAccountPublicKey := newAccountPrivateKey.PublicKey()
```

## Step 2. Create a new account

To create a new account, you will submit an account create transaction to the Hedera test network. The account minimally requires you to assign a public key to the account at creation. This means that the corresponding private key will be required to sign transactions for the new account. This account will have a starting balance of 1,000 tinybars. This initial balance is funded from your testnet account to the new account. You can optionally choose to create an account with a zero balance. 

```java
//Create new account and assign the public key
newAccount, err := hedera.NewAccountCreateTransaction().
  SetKey(newAccountPublicKey).
	SetInitialBalance(hedera.HbarFrom(1000, hedera.HbarUnits.Tinybar)).
	Execute(client)
```

Additional properties can be set for accounts [here](../../docs/sdks/cryptocurrency/create-an-account.md). 

## Step 3. Get the new account ID

When you issue a transaction that creates a new entity \(account, token, topic, etc\) the entity ID is recovered from the receipt of the transaction. You must request the receipt of the transaction to obtain the new account ID. Requesting a receipt is free of charge today.

```java
//Request the receipt of the transaction
receipt, err := newAccount.GetReceipt(client)
if err != nil {
    panic(err)
}

//Get the new account ID from the receipt
newAccountId := *receipt.AccountID

//Print the new account ID to the console
fmt.Printf("The new account ID is %v\n", newAccountId)
```

## Step 4. Verify the new account balance

Next, you will submit a query to the Hedera test network to return the balance of the new account using the new account ID. The current account balance for the new account should be 1,000 tinybars. 

```java
//Create the account balance query
query := hedera.NewAccountBalanceQuery().
     SetAccountID(newAccountId)

//Sign with client operator private key and submit the query to a Hedera network
accountBalance, err := query.Execute(client)
if err != nil {
    panic(err)
}

//Print the balance of tinybars
fmt.Println("The account balance for the new account is ", accountBalance.Hbars.AsTinybar())
```

You can also verify the account balance by visiting a Hedera explorer like [Kabuto](https://explorer.kabuto.sh/testnet) or [DragonGlass](https://app.dragonglass.me) and entering the account ID. 

⭐ Congratulations! You have successfully completed the following:

* Created new a Hedera account with an initial balance of 1,000 tinybars
* Obtained the new account ID by requesting the receipt of the transaction
* Verified the starting balance of the new account by submitting an query to the network

You are now ready to transfer some hbar to the new account 🤑!

## Code Check ✅ 

What your code should look like at this point:

```java
package main

import (
	"fmt"
	"os"

	"github.com/hashgraph/hedera-sdk-go/v2"
	"github.com/joho/godotenv"
)

func main() {

	//Loads the .env file and throws an error if it cannot load the variables from that file corectly
	err := godotenv.Load(".env")
	if err != nil {
		panic(fmt.Errorf("Unable to load enviroment variables from .env file. Error:\n%v\n", err))
	}

	//Grab your testnet account ID and private key from the .env file
	myAccountId, err := hedera.AccountIDFromString(os.Getenv("MY_ACCOUNT_ID"))
	if err != nil {
		panic(err)
	}

	myPrivateKey, err := hedera.PrivateKeyFromString(os.Getenv("MY_PRIVATE_KEY"))
	if err != nil {
		panic(err)
	}

	//Print your testnet account ID and private key to the console to make sure there was no error
	fmt.Printf("The account ID is = %v\n", myAccountId)
	fmt.Printf("The private key is = %v\n", myPrivateKey)

	//Create your testnet client
	client := hedera.ClientForTestnet()
	client.SetOperator(myAccountId, myPrivateKey)

	//Generate new keys for the account you will create
	newAccountPrivateKey, err := hedera.GeneratePrivateKey()
	if err != nil {
		panic(err)
	}

	newAccountPublicKey := newAccountPrivateKey.PublicKey()

	//Create new account and assign the public key
	newAccount, err := hedera.NewAccountCreateTransaction().
		SetKey(newAccountPublicKey).
		SetInitialBalance(hedera.HbarFrom(1000, hedera.HbarUnits.Tinybar)).
		Execute(client)

	//Request the receipt of the transaction
	receipt, err := newAccount.GetReceipt(client)
	if err != nil {
		panic(err)
	}

	//Get the new account ID from the receipt
	newAccountId := *receipt.AccountID

	//Print the new account ID to the console
	fmt.Printf("The new account ID is %v\n", newAccountId)

	//Create the account balance query
	query := hedera.NewAccountBalanceQuery().
		SetAccountID(newAccountId)

	//Sign with client operator private key and submit the query to a Hedera network
	accountBalance, err := query.Execute(client)
	if err != nil {
		panic(err)
	}

	//Print the balance of tinybars
	fmt.Println("The account balance for the new account is ", accountBalance.Hbars.AsTinybar())
}
```

