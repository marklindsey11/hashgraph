# Import an existing key

Construct keys in another format to a key representation or import keys from a file.

{% tabs %}
{% tab title="V1" %}
| **Method**                                     | **Type**          | **Description**                                                                                                       |
| ---------------------------------------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------- |
| `PrivateKey.fromString(<privateKey>)`          | String            | Converts a private key string to PrivateKey                                                                           |
| `PublicKey.fromString(<publicKey>)`            | String            | Converts a public key string to PublicKey                                                                             |
| `PrivateKey.fromBytes(<privateKey>)`           | byte \[]          | Converts a private key from bytes to PrivateKey                                                                       |
| `PublicKey.fromBytes(<publicKey>)`             | byte \[ ]         | Converts a public key from bytes to PublicKey                                                                         |
| `PrivateKey.fromKeystore(<bytes, passphrase>)` | byte \[ ], String | Private key from keystore and passphrase                                                                              |
| `PrivateKey.fromPem(<pemEncoded>)`             | String            | Private key from pem encoded String                                                                                   |
| `PrivateKey.fromPem(<pem, passphrase>)`        | String, String    | Parse a private key from a PEM encoded string. The private key may be encrypted, e.g. if it was generated by OpenSSL. |

{% code title="Java" %}
```java
//Converts a private key string to PrivateKey
Ed25519PrivateKey privateKey = Ed25519PrivateKey.fromString("302e020100300506032b6570042204201d5b7516488d7010e3730ab7432f7115a7588ad76553153f6e108c62cbd1ff25");

//The public key associated with the private key
Ed25519PublicKey publicKey = Ed25519PublicKey.fromString("302a300506032b6570032100d292412f1c86507224c1db656050c2162c91983540d608f6a31e9b43359bc5e");

//v1.3.2
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Converts a private key string to PrivateKey
const privateKey = Ed25519PrivateKey.fromString("302e020100300506032b6570042204201d5b7516488d7010e3730ab7432f7115a7588ad76553153f6e108c62cbd1ff25");

//The public key associated with the private key
const publicKey = Ed25519PublicKey.fromString("302a300506032b6570032100d292412f1c86507224c1db656050c2162c91983540d608f6a31e9b43359bc5e");

//v1.4.4
```
{% endcode %}
{% endtab %}
{% endtabs %}

####
