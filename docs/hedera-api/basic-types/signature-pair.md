# SignaturePair

The client may use any number of bytes from 0 to the whole length of the public key for pubKeyPrefix.

| Field | Type | Description | ​ |
| :--- | :--- | :--- | :--- |
| pubKeyPrefix | ​ | First few bytes of the public key | ​ |
| signature | oneof | ​ | ​ |
| ​ | contract | ​ | smart contract virtual signature \(always length zero\) |
| ​ | ed25519 | ​ | ed25519 signature |
| ​ | RSA\_3072 | ​ | RSA-3072 signature |
| ​ | ECDSA\_384 | ​ | ECDSA p-384 signature |

  
  


