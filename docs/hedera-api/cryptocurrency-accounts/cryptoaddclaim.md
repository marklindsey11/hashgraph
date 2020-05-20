# CryptoAddLiveHash

{% hint style="info" %}
Renamed from CryptoAddClaim to CryptoAddLiveHash \(Hedera Services v0.5.0\)
{% endhint %}

## LiveHash

A hash \(presumably of some kind of credential or certificate\), along with a list of keys \(each of which is either a primitive or a threshold key\). Each of them must reach its threshold when signing the transaction, to attach this livehash to this account. At least one of them must reach its threshold to delete this livehash from this account. This is intended to provide a revocation service: all the authorities agree to attach the livehash, to attest to the fact that the credential or certificate is valid. Any one of the authorities can later delete the livehash, to indicate that the credential has been revoked. In this way, any client can prove to a third party that any particular account has certain credentials, or to identity facts proved about it, and that none of them have been revoked yet.

| Field | Type | Description |
| :--- | :--- | :--- |
| accountID | [AccountID](../basic-types/accountid.md) | the account to which the livehash is attached |
| hash |  | The SHA-384 hash of a credential or certificate |
| keys | [KeyList](../basic-types/keylist.md) | list of keys: all must sign the transaction to attach the livehash, and any one of them can later delete it. Each "key" can actually be a threshold key containing multiple other keys \(including other threshold keys\). |
| claimDuration | [Duration](../miscellaneous/duration.md) | the duration for which the livehash will remain valid |

## CryptoAddLiveHashTransactionBody

At consensus, attaches the given livehash to the given account. The hash can be deleted by the key controlling the account, or by any of the keys associated to the livehash. Hence livehashes provide a revocation service for their implied credentials; for example, when an authority grants a credential to the account, the account owner will cosign with the authority \(or authorities\) to attach a hash of the credential to the account---hence proving the grant. If the credential is revoked, then any of the authorities may delete it \(or the account owner\). In this way, the livehash mechanism acts as a revocation service. An account cannot have two identical livehashes associated. To modify the list of keys in a livehash, the livehash should first be deleted, then recreated with a new list of keys.

| Field | Type | Description |
| :--- | :--- | :--- |
| liveHash | [LiveHash](cryptoaddclaim.md#livehash) | A hash of some credential/certificate, along with the keys that authorized it and are allowed to delete it |

