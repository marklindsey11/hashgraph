# Transfer hbar

In this section, you will learn how to transfer hbar from your account to another account on the Hedera test network.

## Pre-requisites:

{% page-ref page="../introduction.md" %}

{% page-ref page="environment-set-up.md" %}

{% page-ref page="create-an-account.md" %}

{% hint style="warning" %}
Note: This example uses **Hedera Go SDK v2.0.** The latest Hedera Go SDK version can be found [here](https://github.com/hashgraph/hedera-sdk-go), however may not be compatible with this tutorial. 
{% endhint %}

## Step 1. Create a transfer transaction

You should already have a new account ID from the account you created in the "[Create an account](create-an-account.md)" section. You will transfer 1,000 tinybars from your testnet account to the new account. The sender account's private key is required to sign the transaction. The sender account is your testnet account so the client is already set-up to sign with yout testnet account's private key to authorize the transfer. 

```java
//Print the balance of tinybars
//fmt.Println("The account balance for the new account is ", accountBalance.Hbars.AsTinybar())
//-----------------------<enter code below>--------------------------------------

//Transfer hbar from your testnet account to the new account
transaction := hedera.NewTransferTransaction().
		AddHbarTransfer(myAccountId, hedera.HbarFrom(-1000, hedera.HbarUnits.Tinybar)).
		AddHbarTransfer(newAccountId,hedera.HbarFrom(1000, hedera.HbarUnits.Tinybar))

//Submit the transaction to a Hedera network
txResponse, err := transaction.Execute(client)

if err != nil {
    panic(err)
}
```

{% hint style="info" %}
The net value of the transfer must equal zero \(total number of hbars sent by the sender must equal the total number of hbars received by the recipient\). 
{% endhint %}

## Step 2. Verify the transfer transaction reached consensus

To verify the transfer transaction reached consensus by the network, you will submit a request to obtain the receipt of the transfer transaction. The receipt will let you know if the transaction was successful or not.

```java
//Request the receipt of the transaction
transferReceipt, err := txResponse.GetReceipt(client)

if err != nil {
    panic(err)
}

//Get the transaction consensus status
transactionStatus := transferReceipt.Status

fmt.Printf("The transaction consensus status is %v\n", transactionStatus)

```

## Step 3. Get the account balance

### 3.1 Get the cost of requesting the query

You can request the cost of a query prior to submitting the query to the Hedera network. Checking an account balance is free of charge today. You can verify that by the method below.

```java
//Create the query that you want to submit
balanceQuery := hedera.NewAccountBalanceQuery().
     SetAccountID(newAccountId)

//Get the cost of the query
cost, err := balanceQuery.GetCost(client)

if err != nil {
		panic(err)
}

println("The account balance query cost is:", cost.String())
```

### 3.2 Get the account balance

You will verify the account balance was updated for the new account by submitting a get account balance query. The current account balance should be the sum of the initial balance \(1,000 tinybar\) plus the transfer amount \(1,000 tinybar\) and equal to 2,000 tinybars. 

```java
//Check the new account's balance
newAccountBalancequery := hedera.NewAccountBalanceQuery().
     SetAccountID(newAccountId)

//Sign with client operator private key and submit the query to a Hedera network
newAccountBalance, err := newAccountBalancequery.Execute(client)
if err != nil {
    panic(err)
}

//Print the balance of tinybars
fmt.Println("The hbar account balance for this account is", newAccountBalance.Hbars.AsTinybar())
```

⭐ Congratulations! You have successfully transferred hbars to another account on the Hedera testnet! If you have followed the tutorial from the beginning, you have completed the following thus far:

* Set-up your Hedera environment to submit transactions and queries
* Created an account 
* Transferred hbars to another account

Do you want to keep learning? Visit our "[Resources](../../resources/starter-projects.md)" and "[Documentation](../../docs/sdks/)" section to take your learning experience to the next level. You can also find additional Hedera Go SDK examples [here](https://github.com/hashgraph/hedera-sdk-go/tree/master/examples). 

## Code Check ✅ 

Your complete code file should look something like this:

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
	fmt.Println("The account balance for the new account is", accountBalance.Hbars.AsTinybar())

	//Transfer hbar from your testnet account to the new account
	transaction := hedera.NewTransferTransaction().
		AddHbarTransfer(myAccountId, hedera.HbarFrom(-1000, hedera.HbarUnits.Tinybar)).
		AddHbarTransfer(newAccountId, hedera.HbarFrom(1000, hedera.HbarUnits.Tinybar))

	//Submit the transaction to a Hedera network
	txResponse, err := transaction.Execute(client)

	if err != nil {
		panic(err)
	}

	//Request the receipt of the transaction
	transferReceipt, err := txResponse.GetReceipt(client)

	if err != nil {
		panic(err)
	}

	//Get the transaction consensus status
	transactionStatus := transferReceipt.Status

	fmt.Printf("The transaction consensus status is %v\n", transactionStatus)

	//Create the query that you want to submit
	balanceQuery := hedera.NewAccountBalanceQuery().
		SetAccountID(newAccountId)

	//Get the cost of the query
	cost, err := balanceQuery.GetCost(client)

	if err != nil {
		panic(err)
	}

	fmt.Println("The account balance query cost is:", cost.String())

	//Check the new account's balance
	newAccountBalancequery := hedera.NewAccountBalanceQuery().
		SetAccountID(newAccountId)

	//Sign with client operator private key and submit the query to a Hedera network
	newAccountBalance, err := newAccountBalancequery.Execute(client)
	if err != nil {
		panic(err)
	}

	//Print the balance of tinybars
	fmt.Println("The hbar account balance for this account is", newAccountBalance.Hbars.AsTinybar())
}
```

