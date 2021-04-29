# Transfer hbar

In this section, you will learn how to transfer hbar from your account to another account on the Hedera test network.

## Pre-requisites:

{% page-ref page="../introduction.md" %}

{% page-ref page="environment-set-up.md" %}

{% page-ref page="../../core-concepts/accounts.md" %}

{% page-ref page="create-an-account.md" %}

{% hint style="warning" %}
Note: Please follow the example in the version of the SDK you are using. The examples may may be not be compatible if you are using a different version than what is listed.
{% endhint %}

## Step 1: Import the following modules

Continue building on the index.js from the previous example \([Create an account](create-an-account.md)\) and add the following modules:

* TransferTransaction

{% tabs %}
{% tab title="v2.0" %}
```javascript
const { Client, PrivateKey, AccountCreateTransaction, AccountBalanceQuery, Hbar, TransferTransaction} = require("@hashgraph/sdk");
require("dotenv").config();
```
{% endtab %}

{% tab title="v1.0" %}
```javascript
//Import the following modules
const { Client, Ed25519PrivateKey, AccountCreateTransaction, AccountBalanceQuery,Hbar, TransferTransaction } = require("@hashgraph/sdk");
require("dotenv").config();
```
{% endtab %}
{% endtabs %}

## Step 2: Create a transfer transaction

You should already have a new account ID from the account you created from the "[Create an account](create-an-account.md)" section. You will transfer 1,000 tinybars from your account to the new account. The account sending hbars is the signature that is required for this transaction to be processed. 

{% tabs %}
{% tab title="v2.0" %}
```javascript
//console.log("The new account balance is: " +accountBalance.hbars.toTinybars() +" tinybar.");
//-----------------------<enter code below>--------------------------------------

//Create the transfer transaction
const transferTransactionResponse = await new TransferTransaction()
     .addHbarTransfer(myAccountId, Hbar.fromTinybars(-1000)) //Sending account
     .addHbarTransfer(newAccountId, Hbar.fromTinybars(1000)) //Receiving account
     .execute(client);
```
{% endtab %}

{% tab title="v1.0" %}
```javascript
//console.log("The new account balance is: " +accountBalance.hbars.toTinybars() +" tinybar.");
//-----------------------<enter code below>--------------------------------------

//Create the transfer transaction
const transferTransactionId = await new TransferTransaction()
     .addHbarTransfer(myAccountId, Hbar.fromTinybars(-1000)) //Sending account
     .addHbarTransfer(newAccountId, Hbar.fromTinybars(1000)) //Receiving account
     .execute(client);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The net value of the transfer must equal zero \(total number of hbars sent by the sender must equal the total number of hbars received by the recipient\). 
{% endhint %}

## Step 3: Verify the transfer transaction reached consensus 

To verify the transfer transaction reached consensus by the network, you will submit a request to obtain the receipt of the transaction. The receipt status will let you know if the transaction was successful \(reached consensus\) or not.

{% tabs %}
{% tab title="v2.0" %}
```javascript
//Verify the transaction reached consensus
const transactionReceipt = await transferTransactionResponse.getReceipt(client);
console.log("The transfer transaction from my account to the new account was: " + transactionReceipt.status.toString());
```
{% endtab %}

{% tab title="v1.0" %}
```javascript
//Verify the transaction reached consensus
const transactionReceipt = await transferTransactionId.getReceipt(client);
console.log("The transfer transaction from my account to the new account was: " + transactionReceipt.status);
```
{% endtab %}
{% endtabs %}

## Step 4: Get the updated account balance

### 4.1 Get the cost of requesting the query

You can request the cost of a query \(or transaction\) prior to submitting the query to the Hedera network. Checking an account balance is free of charge today. You can verify that by the method below.

{% tabs %}
{% tab title="v2.0" %}
```javascript
//Request the cost of the query
const getBalanceCost = await new AccountBalanceQuery()
     .setAccountId(newAccountId)
     .getCost(client);

console.log("The cost of query is: " +getBalanceCost);
```
{% endtab %}

{% tab title="v1.0" %}
{% code title="index.js" %}
```javascript
//Request the cost of the query
const getBalanceCost = await new AccountBalanceQuery()
     .setAccountId(newAccountId)
     .getCost(client);

console.log("The cost of query is: " +getBalanceCost);
```
{% endcode %}
{% endtab %}
{% endtabs %}

### 4.2  Get the account balance 

You will verify the account balance was updated for the new account by requesting a get account balance query. The current account balance should be the sum of the initial balance \(1,000 tinybar\) plus the transfer amount \(1,000 tinybar\) and equal to 2,000 tinybars. 

```javascript
//Check the new account's balance
const getNewBalance = await new AccountBalanceQuery()
     .setAccountId(newAccountId)
     .execute(client);

console.log("The account balance after the transfer is: " +getNewBalance.hbars.toTinybars() +" tinybar.")
```

⭐ Congratulations!  You have successfully transferred hbars to another account on the Hedera testnet! If you have followed the tutorial from the beginning, you have completed the following thus far:

* Set-up your Hedera environment to submit transactions and queries
* Created an account 
* Transferred hbars to another account

Do you want to keep learning? Visit our "Resources" and "Documentation" section to take your learning experience to the next level. You can also find additional JavaScript SDK examples [here](https://github.com/hashgraph/hedera-sdk-js/tree/master/examples). 



## Code Check ✅ 

Your complete index.js file should look something like this:

{% tabs %}
{% tab title="v2.0" %}
{% code title="index.js" %}
```javascript
const { Client, PrivateKey, AccountCreateTransaction, AccountBalanceQuery, Hbar, TransferTransaction} = require("@hashgraph/sdk");
require("dotenv").config();

async function main() {

    //Grab your Hedera testnet account ID and private key from your .env file
    const myAccountId = process.env.MY_ACCOUNT_ID;
    const myPrivateKey = process.env.MY_PRIVATE_KEY;

    // If we weren't able to grab it, we should throw a new error
    if (myAccountId == null ||
        myPrivateKey == null ) {
        throw new Error("Environment variables myAccountId and myPrivateKey must be present");
    }

    // Create our connection to the Hedera network
    // The Hedera JS SDK makes this really easy!
    const client = Client.forTestnet();

    client.setOperator(myAccountId, myPrivateKey);

    //Create new keys
    const newAccountPrivateKey = await PrivateKey.generate(); 
    const newAccountPublicKey = newAccountPrivateKey.publicKey;

    //Create a new account with 1,000 tinybar starting balance
    const newAccountTransactionResponse = await new AccountCreateTransaction()
        .setKey(newAccountPublicKey)
        .setInitialBalance(Hbar.fromTinybars(1000))
        .execute(client);

    // Get the new account ID
    const getReceipt = await newAccountTransactionResponse.getReceipt(client);
    const newAccountId = getReceipt.accountId;

    console.log("The new account ID is: " +newAccountId);

    //Verify the account balance
    const accountBalance = await new AccountBalanceQuery()
        .setAccountId(newAccountId)
        .execute(client);

    console.log("The new account balance is: " +accountBalance.hbars.toTinybars() +" tinybar.");

    //Create the transfer transaction
    const transferTransactionResponse = await new TransferTransaction()
        .addHbarTransfer(myAccountId, Hbar.fromTinybars(-1000))
        .addHbarTransfer(newAccountId, Hbar.fromTinybars(1000))
        .execute(client);

    //Verify the transaction reached consensus
    const transactionReceipt = await transferTransactionResponse.getReceipt(client);
    console.log("The transfer transaction from my account to the new account was: " + transactionReceipt.status.toString());

    //Check the new account's balance
    const getNewBalance = await new AccountBalanceQuery()
        .setAccountId(newAccountId)
        .execute(client);

    console.log("The account balance after the transfer is: " +getNewBalance.hbars.toTinybars() +" tinybar.")

}
main();
```
{% endcode %}
{% endtab %}

{% tab title="v1.0" %}
{% code title="index.js" %}
```javascript
const { Client, Ed25519PrivateKey, AccountCreateTransaction, AccountBalanceQuery, Hbar, TransferTransaction  } = require("@hashgraph/sdk");
require("dotenv").config();

async function main() {

    //Grab your Hedera testnet account ID and private key from your .env file
    const myAccountId = process.env.MY_ACCOUNT_ID;
    const myPrivateKey = process.env.MY_PRIVATE_KEY;

    // If we weren't able to grab it, we should throw a new error
    if (myAccountId == null ||
        myPrivateKey == null ) {
        throw new Error("Environment variables myAccountId and myPrivateKey must be present");
    }

    // Create our connection to the Hedera network
    // The Hedera JS SDK makes this really easy!
    const client = Client.forTestnet();

    client.setOperator(myAccountId, myPrivateKey);

    //Create new keys
    const newAccountPrivateKey = await Ed25519PrivateKey.generate(); 
    const newAccountPublicKey = newAccountPrivateKey.publicKey;

    //Create a new account with 1,000 tinybar starting balance
    const newAccountTransactionId = await new AccountCreateTransaction()
        .setKey(newAccountPublicKey)
        .setInitialBalance(Hbar.fromTinybar(1000))
        .execute(client);

    // Get the new account ID
    const getReceipt = await newAccountTransactionId.getReceipt(client);
    const newAccountId = getReceipt.getAccountId();

    console.log("The new account ID is: " +newAccountId);

    //Verify the account balance
    const accountBalance = await new AccountBalanceQuery()
        .setAccountId(newAccountId)
        .execute(client);


    console.log("The new account balance is: " +accountBalance.hbars.toTinybars() +" tinybar.");

    //Create the transfer transaction
    const transferTransactionId = await new TransferTransaction()
        .addHbarTransfer(myAccountId, -1000)
        .addHbarTransfer(newAccountId, 1000)
        .execute(client);

    //Verify the transaction reached consensus
    const transactionReceipt = await transferTransactionId.getReceipt(client);
    console.log("The transfer transaction from my account to the new account was: " +transactionReceipt.status);

    //Request the cost of the query
    const getBalanceCost = await new AccountBalanceQuery()
        .setAccountId(newAccountId)
        .getCost(client);

    console.log("The cost of query is: " +getBalanceCost);

    //Check the new account's balance
    const getNewBalance = await new AccountBalanceQuery()
        .setAccountId(newAccountId)
        .execute(client);

    console.log("The account balance after the transfer is: " +getNewBalance.hbars.toTinybars() +" tinybar.")
}
main();
```
{% endcode %}
{% endtab %}
{% endtabs %}

