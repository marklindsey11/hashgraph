# NodeAddress

The metadata for a Node – including IP Address, and the crypto account associated with the Node.

| Field | Type | Description |
| :--- | :--- | :--- |
| `ipAddress` | bytes | The ip address of the Node with separator & octets |
| `portno` | int32 | The port number of the grpc server for the node |
| `memo` | bytes | The memo field of the node |
| `RSA_PubKey` | string | The RSA public key of the node. |
| `nodeId` | int64 | A non-sequential identifier for the node |
| `nodeAccountId` | [AccountId](accountid.md) | The account to be paid for queries and transactions sent to this node |
| `nodeCertHash` | bytes | A hash of the X509 cert used for gRPC traffic to this node |

####   <a id="undefined"></a>

