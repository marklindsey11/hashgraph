# Create an account

The following sample will show you how to make a simple Hedera account. Hedera accounts are the entry  point by which you can interact with the Hedera APIs. Accounts hold a balance of hbars used to pay for API calls for the various transaction and query types.

## Pre-requisites:

{% page-ref page="../introduction.md" %}

{% page-ref page="environment-set-up.md" %}

{% page-ref page="../../core-concepts/accounts.md" %}

{% hint style="warning" %}
Note: This example uses **Hedera JavaScript SDK 1.1.2.** The latest version may not be compatible with the provided examples. View Hedera Hashgraph's JavaScript SDK [here](https://github.com/hashgraph/hedera-sdk-js). 
{% endhint %}

## Step 1: Import the following modules to your project

You will likely have a few of these modules from the previous section.

{% code title="index.js" %}
```javascript
const { Client, Ed25519PrivateKey, AccountCreateTransaction, AccountBalanceQuery } = require("@hashgraph/sdk");
require("dotenv").config();
```
{% endcode %}

## Step 2: Generate keys for the new account

You will need to generate a pair of keys to assign to the new account in the next step. Within the async function,  generate they private and public key pair for the new account. 

{% code title="index.js" %}
```javascript
//Create new keys
const newAccountPrivateKey = await Ed25519PrivateKey.generate(); 
const newAccountPublicKey = newAccountPrivateKey.publicKey;
```
{% endcode %}

## Step 3: Create the new account 

To create a new account you will submit an account create transaction to the Hedera test network. The account minimally requires you to set the key of the account at creation. This means that the corresponding private key will be required to sign transactions for the new account. The account will additionally have a starting balance of 1,000 tinybars. This initial balance is funded from your account to the new account. You can optionally choose to create an account with a zero balance. 

{% code title="index.js" %}
```javascript
//Create a new account with 1,000 tinybar starting balance
const newAccountTransactionId = await new AccountCreateTransaction()
    .setKey(newAccountPublicKey)
    .setInitialBalance(1000)
    .execute(client);
```
{% endcode %}

Additional properties can be set for accounts [here](https://docs.hedera.com/guides/docs/sdks/cryptocurrency/create-an-account). 

## Step 4: Get the new account ID

When you issue a transaction where it creates a new entity \(account, topic, etc\) the new entity ID is stored in the receipt of the transaction. You must request the receipt of the transaction to obtain the new account ID. Requesting a receipt is free of charge today.

{% code title="index.js" %}
```javascript
//Grab your Hedera testnet account ID and private key
const getReceipt = await newAccountTransactionId.getReceipt(client);
const newAccountId = getReceipt.getAccountId();

console.log("The new account ID is: " +newAccountId);
```
{% endcode %}

## Step 5: Verify the new account balance

Next, you will submit a query to the Hedera test network to return the balance of the new account using the new account ID. The current account balance for the new account should be 1,000 tinybars. 

{% code title="index.js" %}
```javascript
const accountBalance = await new AccountBalanceQuery()
    .setAccountId(newAccountId)
    .execute(client);

console.log("The new account balance is: " +accountBalance +" tinybar.");
```
{% endcode %}

⭐ Congratulations! You have successfully completed the following:

* Created new a Hedera account with an initial balance of 1,000 tinybar
* Obtained the new account ID by requesting the receipt of the transaction
* Verified the starting balance of the new account by submitting an query to the network

You are now ready to transfer some hbar to the new account 🤑!

## Code Check ✅ 

Your index.js file should look like this: 

```javascript
const { Client, Ed25519PrivateKey, AccountCreateTransaction, AccountBalanceQuery } = require("@hashgraph/sdk");
require("dotenv").config();

async function main() {

    //Grab your Hedera testnet account ID and private key
    const myAccountId = process.env.MY_ACCOUNT_ID;
    const myPrivateKey = process.env.MY_PRIVATE_KEY;

    // If we weren't able to grab it, we should throw a new error
    if (myAccountId == null ||
        myPrivateKey == null ) {
        throw new Error("Environment variables myAccountId and myPrivateKey must be present");
    }

    console.log(myAccountId, myPrivateKey);

    // Create our connection to the Hedera network
    // The Hedera JS SDK makes this reallyyy easy!
    const client = Client.forTestnet();

    client.setOperator(myAccountId, myPrivateKey);

    //Create new keys
    const newAccountPrivateKey = await Ed25519PrivateKey.generate(); 
    const newAccountPublicKey = newAccountPrivateKey.publicKey;

    //Create a new account with 1,000 tinybar starting balance
    const newAccountTransactionId = await new AccountCreateTransaction()
        .setKey(newAccountPublicKey)
        .setInitialBalance(1000)
        .execute(client);

    //Get the account ID
    const getReceipt = await newAccountTransactionId.getReceipt(client);
    const newAccountId = getReceipt.getAccountId();

    console.log("The new account ID is: " +newAccountId);

    //Verify the account balance
    const accountBalance = await new AccountBalanceQuery()
        .setAccountId(newAccountId)
        .execute(client);

    console.log("The new account balance is: " +accountBalance +" tinybar.");

}
main();
```

