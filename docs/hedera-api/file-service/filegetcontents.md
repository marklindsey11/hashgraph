# FileGetContents

## FileGetContentsQuery

Get the contents of a file. The content field is empty \(no bytes\) if the file is empty.

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [QueryHeader](../miscellaneous/queryheader.md) | Standard info sent from client to node, including the signed payment, and what kind of response is requested \(cost, state proof, both, or neither\). |
| fileID | [FileID](../basic-types/fileid.md) | The file ID of the file whose contents are requested |

## FileGetContentsResponse

Response when the client sends the node FileGetContentsQuery

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [ResponseHeader](../miscellaneous/responseheader.md#responseheader) | Standard response from node to client, including the requested fields: cost, or state proof, or both, or neither |
| fileContents | [FileGetContentsResponse.FileContents](filegetcontents.md#filegetcontentsresponse-filecontents) | the file ID and contents \(a state proof can be generated for this\) |

## FileGetContentsResponse.FileContents

Response when the client sends the node FileGetContentsQuery

| Field | Type | Description |
| :--- | :--- | :--- |
| fileID | [FileID](../basic-types/fileid.md) | The file ID of the file whose contents are being returned |
| contents |  | The bytes contained in the file |



