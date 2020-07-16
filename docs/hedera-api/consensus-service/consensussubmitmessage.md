# ConsensusSubmitMessage

## ConsensusMessageChunkInfo

| Field | Type | Description |
| :--- | :--- | :--- |
| initialTransactionID | TransactionID | TransactionID of the first chunk, gets copied to every subsequent chunk in a fragmented message. |
| total |  | The total number of chunks in the message. |
| number |  | The sequence number \(from 1 to total\) of the current chunk in the message. |

## ConsensusSubmitMessageTransactionBody

| Field | Type | Description |
| :--- | :--- | :--- |
| `topicID` | [TopicID](../basic-types/topicid.md) | Topic to submit message to. |
| `message` |  | Message to be submitted. Max size of the Transaction \(including signatures\) is 6kB. |
| chunkInfo | ConsensusMessageChunkInfo | Optional information of the current chunk in a fragmented message. |



