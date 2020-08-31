# Environment Set-up

In this section you will complete the following:

* Create your project directory
* Create a .env file and store your Hedera testnet account ID and private key
* Set-up your Hedera testnet client

{% hint style="warning" %}
Note: This example uses **Hedera Java SDK 1.1.5.** The latest Hedera Java SDK version can be found [here](https://github.com/hashgraph/hedera-sdk-java), however may not be compatible with the following sample. 
{% endhint %}

## Pre-requisites:

{% page-ref page="../introduction.md" %}

## Step 1: Create a new Gradle project in your favorite IDE

Open your favorite IDE and create a new gradle project. Add the following dependencies to your build.gradle file:

{% tabs %}
{% tab title="build.gradle" %}
```text
sourceCompatibility = 1.8

repositories {
    mavenCentral()
}

dependencies {
    
    implementation 'com.hedera.hashgraph:sdk:1.1.5'
    implementation 'io.grpc:grpc-netty-shaded:1.24.0'
    compile 'io.github.cdimascio:java-dotenv:5.2.1' // Module that stores your environment variables from a .env file
}
```
{% endtab %}
{% endtabs %}

## Step 2: Create a .env file in your project

Create a **.env** file in the root directory of your project. Grab the the Hedera testnet **account ID** and **private key** and enter them in the **MY\_ACCOUNT\_ID** and **MY\_PRIVATE KEY** fields.

{% tabs %}
{% tab title=".env" %}
```text
MY_ACCOUNT_ID= TESTNET ACCOUNT ID (0.0.x)
MY_PRIVATE_KEY= TESTNET PRIVATE KEY (302e...)
```
{% endtab %}
{% endtabs %}

## Step 3: Create a new class

Create a new class and title it something like HederaExamples. Within the main method, grab your testnet account ID and private key from the .env file.

```java
public class HederaExamples {

    public static void main(String[] args) throws InterruptedException, HederaStatusException {
        
        AccountId myAccountId = AccountId.fromString(Dotenv.load().get("MY_ACCOUNT_ID"));
        Ed25519PrivateKey myPrivateKey = Ed25519PrivateKey.fromString(Dotenv.load().get("MY_PRIVATE_KEY"));
    }
}
```

## Step 3: Create your Hedera testnet client

You have the option to create a client for the Hedera mainnet or testnet. Since we are using a Hedera testnet account ID and private key, we will create a client for the Hedera testnet.

After you create your Hedera testnet client, you will need to set the operator information. The operator is the account that will pay for the transaction and query fees. You will need to sign the transaction or query with the private key of that account to authorize the payment.

```java
Client client = Client.forTestnet();
client.setOperator(myAccountId, myPrivateKey);
```

{% hint style="info" %}
The client has a default **max transaction fee** of 100,000,000 tinybars \(1hbar\) and default **max query payment** of 100,000,000 tinybars \(1 hbar\). If you need to change these values, you can use`.setMaxTransactionFee()` for a transaction and `.setMaxQueryPayment()` for queries. You are only charged the actual cost of the transaction or query fee. 
{% endhint %}

Your project environment is now set-up to successfully submit transactions/queries to the Hedera test network! 

Next, you will learn how to create a Hedera testnet account.

### Code Check ✅ 

What your code should look like at this point:

{% code title="HederaExamples.java" %}
```java
import com.hedera.hashgraph.sdk.Client;
import com.hedera.hashgraph.sdk.HederaStatusException;
import com.hedera.hashgraph.sdk.account.AccountId;
import com.hedera.hashgraph.sdk.crypto.ed25519.Ed25519PublicKey;
import com.hedera.hashgraph.sdk.crypto.ed25519.Ed25519PrivateKey;
import io.github.cdimascio.dotenv.Dotenv;

public class HederaExamples {

    public static void main(String[] args) throws InterruptedException, HederaStatusException {
    
        //Grab your Hedera testnet account ID and private key
        AccountId myAccountId = AccountId.fromString(Dotenv.load().get("MY_ACCOUNT_ID"));
        Ed25519PrivateKey myPrivateKey = Ed25519PrivateKey.fromString(Dotenv.load().get("MY_PRIVATE_KEY"));

        //Create your Hedera testnet client
        Client client = Client.forTestnet();
        client.setOperator(myAccountId, myPrivateKey)
    }
}
```
{% endcode %}

