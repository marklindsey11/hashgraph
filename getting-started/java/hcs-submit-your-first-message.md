# HCS: Submit your first message!

## Background

With the Hedera Consensus Service you can develop applications like stock markets, audit logs, stable coins, or new network services that require high throughput and decentralized trust. This is made possible by having direct access to the native speed, security, and fair ordering guarantees of the hashgraph consensus algorithm, with the full trust of the Hedera ledger.

## Components of the Hedera Consensus Service/Terminology

* **Hedera client** - a Hedera client sends transactions to a Hedera network node for consensus. The corresponding transaction types for the Hedera Consensus Service include create a topic, update a topic, submit messages, delete a topic, and get the info for a topic. 
* **Hedera network node** - receives transactions from a client and submits it to the Hedera network for consensus
* **Mirror node client** - a mirror node client is used to subscribe to a topic and get messages that are in consensus order from a mirror node. 
* **Mirror node**: Mirror nodes receive information from Hedera network consensus nodes, but do not participate in consensus themselves. You can get more information about mirror nodes [here](https://docs.hedera.com/guides/core-concepts/mirror-nodes).
* **Topic** - a topic is the subject of information you would like to send messages to and what clients would subscribe to
* **Message** - a message is the content published to the Hedera network

  to a topic that gets placed in consensus order

* **Subscriber** - a client that subscribes to the desired topic in order to receive the appropriate messages
* **Publisher -** publishes messages to a topic 

## HCS Flow

Create a topic by submitting a transaction from the Hedera client to a Hedera network node ➡ Mirror node client subscribes to the topic from mirror node ➡ Publish a message to a topic by submitting a transaction from the Hedera client to a Hedera network node for consensus ➡ Mirror node client receives messages published to the topic from the mirror node

## Getting Started with Hedera Consensus Service \(Testnet\)

What you will need to be successful with this tutorial:

💥 [Testnet account ID and associated private key](https://portal.hedera.com/register)  
💥 [Hedera Java SDK](https://github.com/hashgraph/hedera-sdk-java)  
💥 IDE of your choice

### 1. Get a testnet account

* You will need a testnet account ID and private key to use HCS. If you do not already have one, visit the Hedera [portal](https://portal.hedera.com/register) to create your profile and receive your testnet account ID. A friend already on testnet could also generously create one for you.

### 2. Get access to a mirror node

* You will need to establish a connection to a mirror node to subscribe to a topic. When you build your client in a later step, the connection is automatically established to the Hedera testnet mirror node. The mirror node will return all messages that were sent to the specified topic.

### 3. Create a new maven project in your favorite IDE

* Add the following dependencies to your pom.xml file

```java
<!-- Android, Corda DJVM, Java 7+ -->
<dependency>
  <groupId>com.hedera.hashgraph</groupId>
  <artifactId>sdk-jdk7</artifactId>
  <version>2.0.5</version>
</dependency>

<!-- Java 9+, Kotlin -->
<dependency>
  <groupId>com.hedera.hashgraph</groupId>
  <artifactId>sdk</artifactId>
  <version>2.0.5</version>
</dependency>


<!-- netty transport (for server or desktop applications) -->
<dependency>
  <groupId>io.grpc</groupId>
  <artifactId>grpc-netty-shaded</artifactId>
  <version>1.35.0</version>
</dependency>

<!-- netty transport, unshaded (if you have a matching Netty dependency already) -->
<dependency>
  <groupId>io.grpc</groupId>
  <artifactId>grpc-netty</artifactId>
  <version>1.35.0</version>
</dependency>

<!-- okhttp transport (for lighter-weight applications or Android) -->
<dependency>
  <groupId>io.grpc</groupId>
  <artifactId>grpc-okhttp</artifactId>
  <version>1.35.0</version>
</dependency>
```

### 4. Set up your environment variables

* Create a .env file in the projects root directory 
* Add the following:
  * `OPERATOR_ID`: Your testnet account ID goes here 
  * `OPERATOR_KEY`: Your testnet account ID private key goes here
* Your environment set-up is now complete 

Sample .env file:

```text
# Operator ID and Key
OPERATOR_ID=
OPERATOR_KEY=
```

### 5. Create a new HCS class

* Create a new class and title it something like HederaConsensusService.java

### 6. Connect to the Hedera testnet

* Here we are going to connect to the Hedera testnet and set the operator information with your testnet account ID and private key. The operator is responsible to pay transaction fees and sign all transactions that will be generated in this tutorial. Luckily, this is testnet so you will have unlimited hbars to use in this development environment!
* Note the testnet client builds a connection to both the test network and testnet mirror node

```java
// Grab the OPERATOR_ID and OPERATOR_KEY from the .env file
AccountId OPERATOR_ID = AccountId.fromString(Objects.requireNonNull(Dotenv.load().get("OPERATOR_ID")));
PrivateKey OPERATOR_KEY = PrivateKey.fromString(Objects.requireNonNull(Dotenv.load().get("OPERATOR_KEY")));

// Build Hedera testnet and mirror node client
Client client = Client.forTestnet();

// Set the operator account ID and operator private key
client.setOperator(OPERATOR_ID, OPERATOR_KEY);
```

### 7. Create your first topic!

* To create your first topic, we will use the TopicCreateTransaction constructor, set its properties, and submit it to the Hedera network
* You will want to grab the topic ID so later you can subscribe to that topic via the mirror node
* Topic IDs are in the following format: `0.0.10`

```java
//Create a new topic
TransactionResponse txResponse = new TopicCreateTransaction()
   .execute(client);

//Grab the newly generated topic ID
TopicId topicId = txResponse.getReceipt(client).topicId;

System.out.println("Your topic ID is: " +topicId);
Thread.sleep(5000);
```

### 8. Subscribe to a topic

* Now we will shift our attention to the mirror node and subscribe to the topic created. The client establishes a connection to the Hedera testnet mirror node.
* We will subscribe to a topic by referencing the `topicId`
* We will also print the consensus timestamp and message that was submitted to the console

```java
new TopicMessageQuery()
    .setTopicId(topicId)
    .subscribe(client, resp -> {
            String messageAsString = new String(resp.contents, StandardCharsets.UTF_8);

            System.out.println(resp.consensusTimestamp + " received topic message: " + messageAsString);
    });
```

### 9. Submit a message to a topic

* Now that we have created a topic and subscribed to that topic, we are ready to submit a message using the TopicMessageSubmitTransaction constructor and submit it to the Hedera network
* The below example will submit a message with the message as "hello, HCS!"

```java
//Submit a message to a topic
new TopicMessageSubmitTransaction()
     .setTopicId(topicId)
     .setMessage("hello, HCS!")
     .execute(client)
     .getReceipt(client);

Thread.sleep(2500);
```

* If you have successfully followed the steps in this tutorial, you should see the following print to your console 🤩 :

`2021-05-12T21:43:45.639584Z received topic message: hello, HCS!`

**NOTE**: It may take 10-15 seconds before the message appears on your console from the mirror node.

Having trouble or have any comments, suggestions, or feedback?  
Connect with us on [Discord](https://discordapp.com/invite/FFb9YFX)🤓!

