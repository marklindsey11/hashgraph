# Key

A Key can be a public key from one of the three supported systems \(ed25519, RSA-3072, ECDSA with p384\). Or, it can be the ID of a smart contract instance, which is authorized to act as if it had a key. If an account has an ed25519 key associated with it, then the corresponding private key must sign any transaction to transfer cryptocurrency out of it. And similarly for RSA and ECDSA.

| Field | Type | Description | ​ |
| :--- | :--- | :--- | :--- |
| key | oneof | ​ | ​ |
| ​ | contractID | ​[ContractID](contractid.md)​ | smart contract instance that is authorized as if it had signed with a key |
| ​ | ed25519 | ​ | ed25519 public key bytes |
| ​ | RSA\_3072 | ​ | RSA-3072 public key bytes |
| ​ | ECDSA\_384 | ​ | ECDSA with the p-384 curve public key bytes |
| ​ | thresholdKey | ​[ThresholdKey](thresholdkey.md)​ | a threshold N followed by a list of M keys, any N of which are required to form a valid signature |
| ​ | keyList | ​[KeyList](https://docs.hedera.com/hedera-api/basic-types-1/untitled-5)​ | A list of Keys of the Key type. |

  


