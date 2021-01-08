# Create an account

In this section, you will learn how to make a simple Hedera account. Hedera accounts are the entry  point by which you can interact with the Hedera APIs. Accounts hold a balance of hbars used to pay for API calls for the various transaction and query types.

## Pre-requisites:

{% page-ref page="../introduction.md" %}

{% page-ref page="environment-set-up.md" %}

{% page-ref page="../../core-concepts/accounts.md" %}

{% hint style="warning" %}
Note: Please follow the example in the version of the SDK you are using. The examples may may be not be compatible if you are using a different version than what is listed.
{% endhint %}

## Step 1. Generate keys for the new account

Create keys for the new account you are going create. The public key will be associated with the new account and the corresponding private key is used to sign transactions. 

Continue building on the HederaExamples class from the previous section.

{% tabs %}
{% tab title="v2.0" %}
```java
//Create your Hedera testnet client
//Client client = Client.forTestnet();
//client.setOperator(myAccountId, myPrivateKey)
//-----------------------<enter code below>--------------------------------------

// Generate a new key pair
PrivateKey newAccountPrivateKey = PrivateKey.generate();
PublicKey newAccountPublicKey = newAccountPrivateKey.getPublicKey();
```
{% endtab %}

{% tab title="v1.0" %}
```java
//Create your Hedera testnet client
//Client client = Client.forTestnet();
//client.setOperator(myAccountId, myPrivateKey)
//-----------------------<enter code below>--------------------------------------

// Generate a new key pair
Ed25519PrivateKey newAccountPrivateKey = Ed25519PrivateKey.generate();
Ed25519PublicKey newAccountPublicKey = newAccountPrivateKey.publicKey;
```
{% endtab %}
{% endtabs %}

## Step 2. Create a new account

To create a new account we will submit an account create transaction to the Hedera test network. The account minimally requires you to assign a public key to the account at creation. This means that the corresponding private key will be required to sign transactions for the new account. We will additionally have a starting balance of 1,000 tinybars. This initial balance is funded from your testnet account to the new account. You can optionally choose to create an account with a zero balance. 

{% tabs %}
{% tab title="v2.0" %}
```java
//Create new account and assign the public key
TransactionResponse newAccount = new AccountCreateTransaction()
     .setKey(newAccountPublicKey)
     .setInitialBalance( Hbar.fromTinybars(1000))
     .execute(client);
```
{% endtab %}

{% tab title="v1.0" %}
```java
//Create new account and assign the public key
TransactionId newAccount = new AccountCreateTransaction()
     .setKey(newAccountPublicKey)
     .setInitialBalance(1000)
     .execute(client);
```
{% endtab %}
{% endtabs %}

Additional properties for account creation are explained [here](https://docs.hedera.com/guides/docs/sdks/cryptocurrency/create-an-account). 

## Step 3. Get the new account ID

When you issue a transaction that creates a new entity \(account, topic, token, file, smart contract\), the new entity ID is stored in the receipt of the transaction. You must request the receipt of the transaction to obtain the new account ID. Requesting a receipt is free of charge today.

{% tabs %}
{% tab title="v2.0" %}
```java
// Get the new account ID
AccountId newAccountId = newAccount.getReceipt(client).accountId;

System.out.println("The new account ID is: " +newAccountId);
```
{% endtab %}

{% tab title="v1.0" %}
```java
// Get the new account ID
AccountId newAccountId = newAccount.getReceipt(client).getAccountId();

System.out.println("The new account ID is: " +newAccountId);
```
{% endtab %}
{% endtabs %}

## Step 4. Verify the new account balance

Next, you will submit a query to the Hedera test network to return the balance of the new account using the new account ID. The current account balance for the new account should be 1,000 tinybars. 

{% tabs %}
{% tab title="v2.0" %}
```java
//Check the new account's balance
AccountBalance accountBalance = new AccountBalanceQuery()
     .setAccountId(newAccountId)
     .execute(client);

System.out.println("The new account balance is: " +accountBalance);
```
{% endtab %}

{% tab title="v1.0" %}
```java
//Check the new account's balance
Hbar accountBalance = new AccountBalanceQuery()
     .setAccountId(newAccountId)
     .execute(client);

System.out.println("The new account balance is: " +accountBalance);
```
{% endtab %}
{% endtabs %}

⭐ Congratulations! You have successfully completed the following:

* Created new a Hedera account with an initial balance of 1,000 tinybar
* Obtained the new account ID by requesting the receipt of the transaction
* Verified the starting balance of the new account by submitting an query to the network

You are now ready to transfer some hbar to the new account 🤑!

## Code Check ✅ 

What your code should look like at this point:

{% tabs %}
{% tab title="v2.0" %}
{% code title="HederaExamples.java" %}
```java
import com.hedera.hashgraph.sdk.AccountId;
import com.hedera.hashgraph.sdk.HederaPreCheckStatusException;
import com.hedera.hashgraph.sdk.HederaReceiptStatusException;
import com.hedera.hashgraph.sdk.PrivateKey;
import com.hedera.hashgraph.sdk.Client;
import com.hedera.hashgraph.sdk.TransactionResponse;
import com.hedera.hashgraph.sdk.PublicKey;
import com.hedera.hashgraph.sdk.AccountCreateTransaction;
import com.hedera.hashgraph.sdk.Hbar;
import com.hedera.hashgraph.sdk.AccountBalanceQuery;
import com.hedera.hashgraph.sdk.AccountBalance;
import io.github.cdimascio.dotenv.Dotenv;

import java.util.concurrent.TimeoutException;

public class HederaExamples {

    public static void main(String[] args) throws TimeoutException, HederaPreCheckStatusException, HederaReceiptStatusException {

        //Grab your Hedera testnet account ID and private key
        AccountId myAccountId = AccountId.fromString(Dotenv.load().get("MY_ACCOUNT_ID"));
        PrivateKey myPrivateKey = PrivateKey.fromString(Dotenv.load().get("MY_PRIVATE_KEY"));

        //Create your Hedera testnet client
        Client client = Client.forTestnet();
        client.setOperator(myAccountId, myPrivateKey);

        // Generate a new key pair
        PrivateKey newAccountPrivateKey = PrivateKey.generate();
        PublicKey newAccountPublicKey = newAccountPrivateKey.getPublicKey();

        //Create new account and assign the public key
        TransactionResponse newAccount = new AccountCreateTransaction()
                .setKey(newAccountPublicKey)
                .setInitialBalance( Hbar.fromTinybars(1000))
                .execute(client);

        // Get the new account ID
        AccountId newAccountId = newAccount.getReceipt(client).accountId;

        System.out.println("The new account ID is: " +newAccountId);

        //Check the new account's balance
        AccountBalance accountBalance = new AccountBalanceQuery()
                .setAccountId(newAccountId)
                .execute(client);

        System.out.println("The new account balance is: " +accountBalance.hbars);

    }
}
```
{% endcode %}
{% endtab %}

{% tab title="v1.0" %}
{% code title="HederaExamples.java" %}
```java
import com.hedera.hashgraph.sdk.Client;
import com.hedera.hashgraph.sdk.Hbar;
import com.hedera.hashgraph.sdk.HederaStatusException;
import com.hedera.hashgraph.sdk.TransactionId;
import com.hedera.hashgraph.sdk.account.AccountBalanceQuery;
import com.hedera.hashgraph.sdk.account.AccountCreateTransaction;
import com.hedera.hashgraph.sdk.account.AccountId;
import com.hedera.hashgraph.sdk.crypto.ed25519.Ed25519PublicKey;
import com.hedera.hashgraph.sdk.crypto.ed25519.Ed25519PrivateKey;
import io.github.cdimascio.dotenv.Dotenv;

public class HederaExamples {

    public static void main(String[] args) throws InterruptedException, HederaStatusException {

        //Grab your account ID and private key from the .env file
        AccountId myAccountId = AccountId.fromString(Dotenv.load().get("MY_ACCOUNT_ID"));
        Ed25519PrivateKey myPrivateKey = Ed25519PrivateKey.fromString(Dotenv.load().get("MY_PRIVATE_KEY"));

        //Create your Hedera testnet client
        Client client = Client.forTestnet();
        client.setOperator(myAccountId, myPrivateKey);

        // Generate a new pair of keys
        Ed25519PrivateKey newAccountPrivateKey = Ed25519PrivateKey.generate();
        Ed25519PublicKey newAccountPublicKey = newAccountPrivateKey.publicKey;

        // Create new account and assign the public key
        TransactionId newAccount = new AccountCreateTransaction()
                .setKey(newAccountPublicKey)
                .setInitialBalance(1000)
                .execute(client);

        // Get the new account ID
        AccountId newAccountId = newAccount.getReceipt(client).getAccountId();

        System.out.println("The new account ID is: " +newAccountId);

        // Check the new account's balance
        Hbar accountBalance = new AccountBalanceQuery()
                .setAccountId(newAccountId)
                .execute(client);

        System.out.println("The new account balance is: " +accountBalance);
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

