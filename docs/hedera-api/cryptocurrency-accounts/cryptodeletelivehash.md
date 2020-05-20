# CryptoDeleteLiveHash

{% hint style="info" %}
Renamed from CryptoDeleteClaim to CryptoDeleteLiveHash \(Hedera Services v0.5.0\).
{% endhint %}

At consensus, deletes a livehash associated to the given account. The transaction must be signed by either the key of the owning account, or at least one of the keys associated to the livehash.

## CryptoDeleteLiveHashTransactionBody

| Field | Type | Description |
| :--- | :--- | :--- |
| accountOfLiveHash | [AccountID](../basic-types/accountid.md) | The account owning the livehash |
| liveHashToDelete |  | The SHA-384 livehash to delete from the account \(48 bytes\) |

