# SignaturePair

The client may use any number of bytes from 0 to the whole length of the public key for pubKeyPrefix. If 0 bytes is used, then it is assumed that only one public key is used to sign. Only ed25519 keys and hence signatures are currently supported.

| Field | Type | Description | ​ |
| :--- | :--- | :--- | :--- |
| `pubKeyPrefix` | ​ | First few bytes of the public key | ​ |
| `signature` | oneof | ​ | ​ |
| ​ | contract | ​ | smart contract virtual signature \(always length zero\) |
| ​ | ed25519 | ​ | ed25519 signature |
| ​ | RSA\_3072 | ​ | RSA-3072 signature |
| ​ | ECDSA\_384 | ​ | ECDSA p-384 signature |

  
  


