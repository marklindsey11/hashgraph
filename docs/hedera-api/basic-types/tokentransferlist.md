# TokenTransferList

A list of token IDs and amounts representing the transferred out \(negative\) or into \(positive\) amounts, represented in the lowest denomination of the token

| Field | Type | Description |
| :--- | :--- | :--- |
| token | [TokenID](https://github.com/hashgraph/hedera-protobuf/tree/hedera-protobuf-java-api-0.9.0-alpha5#TokenID) | The ID of the token |
| transfers | [AccountAmount](https://github.com/hashgraph/hedera-protobuf/tree/hedera-protobuf-java-api-0.9.0-alpha5#AccountAmount) | Multiple list of AccountAmounts, each of which has an account and amount |

