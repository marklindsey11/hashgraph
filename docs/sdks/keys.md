# Keys

Hedera accounts require a cryptographically secure key pair in order to be generated and used. It’s these keys that define ownership, granting access to files, or allowing hbar transfers. 

Hedera conveniently supplies support for different key types without the use of a smart contract. This is powerful and allows you to easily model how you want your users to make decisions directly in the code. 

* **Simple Key**: Only one key pair has the authority to modify the account 
* **Key List**: A list of keys that are all required to sign transactions to modify the account
* **Threshold Keys**: Requires a minimum of x number of signatures from a total of y signatures to modify the account.



The SDK currently suppports Ed25519 key system. 

| **Method** | Type | Description |
| :--- | :---: | :--- |
| `Ed25519PrivateKey.generate()` | [Ed25519PrivateKey](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/crypto/ed25519/Ed25519PrivateKey.java) | Generates a Ed25519 private key |
| `<newKey>.PublicKey()` | [Ed25519PublicKey](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/crypto/ed25519/Ed25519PublicKey.java) | Gets the corresponding public key to the previously generated private key |

### Example

{% tabs %}
{% tab title="Java" %}
```java
// Generate a Ed25519 private, public key pair
Ed25519PrivateKey newKey = Ed25519PrivateKey.generate();
Ed25519PublicKey newPublicKey = newKey.publicKey;

System.out.println("private key = " + newKey);
System.out.println("public key = " + newPublicKey);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const {Ed25519PrivateKey}= require('@hashgraph/sdk');

async function main() {

    const privateKey = await Ed25519PrivateKey.generate();
    const key = privateKey.publicKey;
    
    console.log(`private = ${privateKey.toString()}`);
    console.log(`public = ${key.toString()}`);
    }
    
main();
```
{% endtab %}
{% endtabs %}

## Key List

Create a key list where each key in the list is required to sign the transaction.

| Constructor | Description |
| :--- | :--- |
| `new KeyList()` | Initializes a KeyList object |

```java
new KeyList()
```

| **Method** | Type | Description |
| :--- | :---: | :--- |
| `add(<key>)` | [Ed25519PublicKey](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/crypto/ed25519/Ed25519PublicKey.java) | Add one public key to the key list |
| `addAll(<keys>)` | [Ed25519PublicKey](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/crypto/ed25519/Ed25519PublicKey.java) | Add all keys to the key list |

### Example

{% tabs %}
{% tab title="Java" %}
```java
//Generate 3 keys
Ed25519PrivateKey key1 = Ed25519PrivateKey.generate();
Ed25519PublicKey publicKey1 = key1.publicKey;

Ed25519PrivateKey key2 = Ed25519PrivateKey.generate();
Ed25519PublicKey publicKey2 = key2.publicKey;

Ed25519PrivateKey key3 = Ed25519PrivateKey.generate();
Ed25519PublicKey publicKey3 = key3.publicKey;

//Add they keys to a key list
KeyList keyList = new KeyList().add(publicKey1).add(publicKey2).add(publicKey3);
 
//Create an account with a key list       
AccountCreateTransaction transaction = new AccountCreateTransaction()
    // require 3 of the 3 keys we generated to sign on anything modifying this account
    .setKey(keyList)
    .setInitialBalance(new Hbar(10));

//Submit the transaction to a Hedera network
TransactionId txId = transaction.execute(client);

//v1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Generate 3 keys
const key1 = await Ed25519PrivateKey.generate();
const publicKey1 = key1.publicKey;

const key2 = await Ed25519PrivateKey.generate();
const publicKey2 = key2.publicKey;

const key3 = await Ed25519PrivateKey.generate();
const publicKey3 = key3.publicKey;

//Add they keys to a key list
const keyList = new KeyList().add(publicKey1).add(publicKey2).add(publicKey3);
 
//Create an account with a key list       
const transaction = new AccountCreateTransaction()
    // require 3 of the 3 keys we generated to sign on anything modifying this account
    .setKey(keyList)
    .setInitialBalance(new Hbar(10));

//Submit the transaction to a Hedera network
const txId = await transaction.execute(client);

//v1.4.2
```
{% endtab %}
{% endtabs %}

## Threshold Keys

Create a key list where each key in the list is required to sign the transaction.

| Constructor | Type | Description |
| :--- | :--- | :--- |
| `new ThresholdKey(<threshold>)` | int | Initializes a KeyList object |

```java
new ThresholdKey(<threshold>)
```

| **Method** | Type | Description |
| :--- | :---: | :--- |
| `add(<key>)` | [Ed25519PublicKey](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/crypto/ed25519/Ed25519PublicKey.java) | Add one public key to the key list |
| `addAll(<keys>)` | [Ed25519PublicKey](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/crypto/ed25519/Ed25519PublicKey.java) | Add all keys to the key list |

### Example

{% tabs %}
{% tab title="Java" %}
```java
//Generate 3 keys
Ed25519PrivateKey key1 = Ed25519PrivateKey.generate();
Ed25519PublicKey publicKey1 = key1.publicKey;

Ed25519PrivateKey key2 = Ed25519PrivateKey.generate();
Ed25519PublicKey publicKey2 = key2.publicKey;

Ed25519PrivateKey key3 = Ed25519PrivateKey.generate();
Ed25519PublicKey publicKey3 = key3.publicKey;

// require 2 of the 3 keys we generated to sign on anything modifying this account
ThresholdKey thresholdKeys = new ThresholdKey(2).add(publicKey1).add(publicKey2).add(publicKe

//Create an account with a key list       
AccountCreateTransaction transaction = new AccountCreateTransaction()
    // require 2 of the 3 keys we generated to sign on anything modifying this account
    .setKey(thresholdKeys)
    .setInitialBalance(new Hbar(10));

//Submit the transaction to a Hedera network
TransactionId txId = transaction.execute(client);

//v1.2.2
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
//Generate 3 keys
const key1 = await Ed25519PrivateKey.generate();
const publicKey1 = key1.publicKey;

const key2 = await Ed25519PrivateKey.generate();
const publicKey2 = key2.publicKey;

const key3 = await Ed25519PrivateKey.generate();
const publicKey3 = key3.publicKey;

//Create a threshold key of 2/3
const thresholdKeys = new ThresholdKey(2).add(publicKey1).add(publicKey2).add(publicKey3);
    
const transaction = new AccountCreateTransaction()
    // require 2 of the 3 keys we generated to sign on anything modifying this account
    .setKey(thresholdKeys)
    .setInitialBalance(new Hbar(10));

//Submit the transaction to a Hedera network
const txId = await transaction.execute(client);


//v1.4.2
```
{% endtab %}
{% endtabs %}

## 

