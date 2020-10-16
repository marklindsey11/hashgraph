# Transaction Contents

## SignedTransaction

| Field | Type | Description |
| :--- | :--- | :--- |
| bodyBytes |  | TransactionBody serialized into bytes, which needs to be signed |
| sigMap | [SignatureMap](https://github.com/hashgraph/hedera-protobuf/tree/hedera-protobuf-java-api-0.9.0-alpha5#SignatureMap) | The signatures on the body with the new format, to authorize the transaction |

