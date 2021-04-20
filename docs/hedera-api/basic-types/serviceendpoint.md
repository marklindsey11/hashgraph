# ServiceEndpoint

Contains the IP address and the port representing a service endpoint of a Node in a network. Used to reach the Hedera API and submit transactions to the network. Added in Hedera services v0.13.0 release.

| Field | Type | Description |
| :--- | :--- | :--- |
| `ipAddressV4` | bytes | The 32-bit IPv4 address of the node encoded in left to right order \(e.g. 127.0.0.1 has 127 as its first byte\) |
| `port` | int32 | The port of the node |



