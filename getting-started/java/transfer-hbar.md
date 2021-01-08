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

## Step 1. Create a transfer transaction

You should already have a new account ID from the account you created in the "[Create an account](create-an-account.md)" section. You will transfer 1,000 tinybars from your account to the new account. The account sending hbars is the signature that is required for this transaction to be processed. 

{% tabs %}
{% tab title="v2.0" %}
```java
//System.out.println("The new account balance is: " +accountBalance.hbars);
//-----------------------<enter code below>--------------------------------------

//Transfer hbar
TransactionResponse sendHbar = new TransferTransaction()
     .addHbarTransfer(myAccountId, Hbar.fromTinybars(-1000)) //Sending account
     .addHbarTransfer(newAccountId, Hbar.fromTinybars(1000)) //Receiving account
     .execute(client);

```
{% endtab %}

{% tab title="v1.0" %}
```java
//System.out.println("The new account balance is: " +accountBalance);
//-----------------------<enter code below>--------------------------------------

//Transfer hbar
TransactionId sendHbar = new CryptoTransferTransaction()
     .addSender(myAccountId, 1000)
     .addRecipient(newAccountId, 1000)
     .execute(client);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The net value of the transfer must equal zero \(total number of hbars sent by the sender must equal the total number of hbars received by the recipient\). 
{% endhint %}

## Step 2. Verify the transfer transaction reached consensus

To verify the transfer transaction reached consensus by the network, you will submit a request to obtain the receipt of the transfer transaction. The receipt will let you know if the transaction was successful or not.

{% tabs %}
{% tab title="v2.0" %}
```java
System.out.println("The transfer transaction was: " +sendHbar.getReceipt(client).status);
```
{% endtab %}

{% tab title="v1.0" %}
```java
System.out.println("The transfer transaction was: " +sendHbar.getReceipt(client).status);
```
{% endtab %}
{% endtabs %}

## Step 3. Get the account balance

### 3.1 Get the cost of requesting the query

You can request the cost of a query prior to submitting the query to the Hedera network. Checking an account balance is free of charge today. You can verify that by the method below.

{% tabs %}
{% tab title="v2.0" %}
```java
//Request the cost of the query
Hbar queryCost = new AccountBalanceQuery()
     .setAccountId(newAccountId)
     .getCost(client);

System.out.println("The cost of this query is: " +queryCost);
```
{% endtab %}

{% tab title="v1.0" %}
```java
//Request the cost of the query
long queryCost = new AccountBalanceQuery()
     .setAccountId(newAccountId)
     .getCost(client);
        
System.out.println("The cost of this query is: " +queryCost);
```
{% endtab %}
{% endtabs %}

### 3.2 Get the account balance

You will verify the account balance was updated for the new account by requesting a get account balance query. The current account balance should be the sum of the initial balance \(1,000 tinybar\) plus the transfer amount \(1,000 tinybar\) and equal to 2,000 tinybars. 

{% tabs %}
{% tab title="v2.0" %}
```java
//Check the new account's balance
AccountBalance accountBalanceNew = new AccountBalanceQuery()
     .setAccountId(newAccountId)
     .execute(client);

System.out.println("The new account balance is: " +accountBalanceNew.hbars);
```
{% endtab %}

{% tab title="v1.0" %}
```java
//Check the new account's balance
Hbar accountBalanceNew = new AccountBalanceQuery()
     .setAccountId(newAccountId)
     .execute(client);

System.out.println("The new account balance is: " +accountBalanceNew);
```
{% endtab %}
{% endtabs %}

⭐ Congratulations! You have successfully transferred hbars to another account on the Hedera testnet! If you have followed the tutorial from the beginning, you have completed the following thus far:

* Set-up your Hedera environment to submit transactions and queries
* Created an account 
* Transferred hbars to another account

Do you want to keep learning? Visit our "Resources" and "Documentation" section to take your learning experience to the next level. You can also find additional Java SDK examples [here](https://github.com/hashgraph/hedera-sdk-java/tree/master/examples/src/main/java/com/hedera/hashgraph/sdk/examples). 

## Code Check ✅ 

Your complete code file should look something like this:

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
import com.hedera.hashgraph.sdk.TransferTransaction;
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

        //Transfer hbar
        TransactionResponse sendHbar = new TransferTransaction()
                .addHbarTransfer(myAccountId, Hbar.fromTinybars(-1000))
                .addHbarTransfer(newAccountId, Hbar.fromTinybars(1000))
                .execute(client);

        System.out.println("The transfer transaction was: " +sendHbar.getReceipt(client).status);

        //Request the cost of the query
        Hbar queryCost = new AccountBalanceQuery()
                .setAccountId(newAccountId)
                .getCost(client);

        System.out.println("The cost of this query is: " +queryCost);

        //Check the new account's balance
        AccountBalance accountBalanceNew = new AccountBalanceQuery()
                .setAccountId(newAccountId)
                .execute(client);

        System.out.println("The new account balance is: " +accountBalanceNew.hbars);

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
import com.hedera.hashgraph.sdk.account.CryptoTransferTransaction;
import com.hedera.hashgraph.sdk.crypto.ed25519.Ed25519PublicKey;
import com.hedera.hashgraph.sdk.crypto.ed25519.Ed25519PrivateKey;
import io.github.cdimascio.dotenv.Dotenv;

public class HederaExamples {

    public static void main(String[] args) throws InterruptedException, HederaStatusException {

        //Grab your account ID and private key from the .env file
        AccountId myAccountId = AccountId.fromString(Dotenv.load().get("MY_ACCOUNT_ID"));
        Ed25519PrivateKey myPrivateKey = Ed25519PrivateKey.fromString(Dotenv.load().get("MY_PRIVATE_KEY"));

        //Create a Hedera testnet client
        Client client = Client.forTestnet();
        client.setOperator(myAccountId, myPrivateKey);

        //Generate a new pair of keys
        Ed25519PrivateKey newAccountPrivateKey = Ed25519PrivateKey.generate();
        Ed25519PublicKey newAccountPublicKey = newAccountPrivateKey.publicKey;

        //Create new account and assign the public key
        TransactionId newAccount = new AccountCreateTransaction()
                .setKey(newAccountPublicKey)
                .setInitialBalance(1000)
                .execute(client);

        //Get the new account ID
        AccountId newAccountId = newAccount.getReceipt(client).getAccountId();

        System.out.println("The new account ID is: " +newAccountId);

        //Check the new account's balance
        Hbar accountBalance = new AccountBalanceQuery()
                .setAccountId(newAccountId)
                .execute(client);

        System.out.println("The new account balance is: " +accountBalance);

        //Transfer hbar
        TransactionId sendHbar = new CryptoTransferTransaction()
                .addSender(myAccountId, 1000)
                .addRecipient(newAccountId, 1000)
                .execute(client);

        System.out.println("The transfer transaction was: " +sendHbar.getReceipt(client).status);
        
        //Request the cost of the query
        long queryCost = new AccountBalanceQuery()
                .setAccountId(newAccountId)
                .getCost(client);
        
        System.out.println("The cost of this query is: " +queryCost);

        //Check the new account's balance
        Hbar accountBalanceNew = new AccountBalanceQuery()
                .setAccountId(newAccountId)
                .execute(client);

        System.out.println("The new account balance is: " +accountBalanceNew);
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Sample Output:

`The new account ID is: 0.0.215975   
The new account balance is: 1000 tℏ   
The transfer transaction was: SUCCESS The cost of this query is: 0   
The new account balance is: 2000 tℏ`

