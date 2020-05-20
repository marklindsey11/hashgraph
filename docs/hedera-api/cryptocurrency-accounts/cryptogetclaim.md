# CryptoGetLiveHash

{% hint style="info" %}
Renamed from CryptoDeleteClaim to CryptoDeleteLiveHash \(Hedera Services v0.5.0\).
{% endhint %}

## CryptoGetLiveHashQuery

Get a single livehash attached to an account, or return null if it does not exist.

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [QueryHeader](../miscellaneous/queryheader.md) | Standard info sent from client to node, including the signed payment, and what kind of response is requested \(cost, state proof, both, or neither\). |
| accountID | [AccountID](../basic-types/accountid.md) | The account ID to which the livehash was attached |
| hash |  | The SHA-384 data in the livehash |

## CryptoGetLiveHashResponse

Returns the full livehash associated to an account, if it is present. Note that the only way to obtain a state proof exhibiting the absence of a livehash from an account is to retrieve a state proof of the entire account with its list of livehashes.

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [ResponseHeader](../miscellaneous/responseheader.md) | Standard response from node to client, including the requested fields: cost, or state proof, or both, or neither |
| livehash | LiveHash | The livehash, if present |

