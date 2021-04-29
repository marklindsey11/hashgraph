# Environment Set-up

In this section you will complete the following:

* Create your project directory
* Create a .env file and store your Hedera testnet account ID and private key
* Set-up your Hedera testnet client

{% hint style="warning" %}
Note: This example uses **Hedera Go SDK v2.0.** The latest Hedera Go SDK version can be found [here](https://github.com/hashgraph/hedera-sdk-go), however may not be compatible with this tutorial.
{% endhint %}

## Pre-requisites:

{% page-ref page="../introduction.md" %}

## Step 1: Create your Go project

Open your terminal and create a project directory called something like hedera-go-examples to store your Go source code.

```bash
mkdir hedera-go-examples && cd hedera-go-examples
```

## Step 2: Create a .env file in your project

Open the project in your favorite IDE and create a **.env** file in the root directory of your project. Enter your Hedera testnet account ID and private key provided to you from your Hedera portal account.

{% tabs %}
{% tab title=".env" %}
```text
MY_ACCOUNT_ID= <Enter testnet account ID (0.0.x)>
MY_PRIVATE_KEY= <Enter testnet private key (302e...)>
```
{% endtab %}

{% tab title="Sample" %}
```text
MY_ACCOUNT_ID= 0.0.9401534
MY_PRIVATE_KEY= 302e020100300506032b65700422042012a4a4add3d885bd61d7ce5cff99c5ef2d510651add00a7f64cb90de3359bc5e
```
{% endtab %}
{% endtabs %}

## Step 3: Install the Hedera Go SDK

Create a hedera\_examples.go file in hedera-go-examples directory. You will write all of your code in this file.

Import the following packages to your hedera\_examples.go file:

```go
package main

import (
    "fmt"
    "os"

    "github.com/joho/godotenv"
    "github.com/hashgraph/hedera-sdk-go/v2"
)
```

Next, you will load your account ID and private key variables from the .env file created in the previous step.

```go
package main

import (
    "fmt"
    "os"

    "github.com/joho/godotenv"
    "github.com/hashgraph/hedera-sdk-go/v2"
)

func main() {

    //Loads the .env file and throws an error if it cannot load the variables from that file correctly
    err := godotenv.Load(".env")
    if err != nil {
        panic(fmt.Errorf("Unable to load environment variables from .env file. Error:\n%v\n", err))
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
}
```

In your terminal, enter the following command to create your go.mod file. This module is used for tracking dependencies and is required.

```bash
go mod init hedera_examples.go
```

Run your code to see your testnet account ID and private key printed to the console.

```go
go run hedera_examples.go
```

## Step 4: Create your Hedera testnet client

You have the option to create a client for the Hedera previewnet, testnet, and mainnet. Since we are using a Hedera testnet account ID and private key, we will create a client for the Hedera testnet. This allows you to submit transactions and queries to the test network.

After you create your Hedera testnet client, you will need to set the operator account ID and private key. The operator is the default account that will pay for the transaction and query fees. You will need to sign the transactions or queries with the private key of the operator account to authorize the payment. The operator in this example will be your testnet account ID and private key.

```go
//Create your testnet client
client := hedera.ClientForTestnet()
client.SetOperator(myAccountId, myPrivateKey)
```

{% hint style="info" %}
The client has a default **max transaction fee** of 100,000,000 tinybars \(1 hbar\) and default **max query payment** of 100,000,000 tinybars \(1 hbar\). If you need to change these values, you can use`.setMaxTransactionFee()` for transactions and `.setMaxQueryPayment()` for queries. You are only charged the actual cost of the transaction or query.
{% endhint %}

Your project environment is now set-up to successfully submit transactions/queries to the Hedera test network!

Next, you will learn how to create a Hedera testnet account.

### Code Check ✅

What your code should look like at this point:

```go
package main

import (
    "fmt"
    "os"

    "github.com/hashgraph/hedera-sdk-go/v2"
    "github.com/joho/godotenv"
)

func main() {

    //Loads the .env file and throws an error if it cannot load the variables from that file correctly
    err := godotenv.Load(".env")
    if err != nil {
        panic(fmt.Errorf("Unable to load environment variables from .env file. Error:\n%v\n", err))
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
}
```

