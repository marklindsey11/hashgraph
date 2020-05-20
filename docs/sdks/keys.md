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

## Example

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

