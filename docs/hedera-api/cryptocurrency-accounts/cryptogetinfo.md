# CryptoGetInfo

## CryptoGetInfoQuery

Get all the information about an account, including the balance. This does not get the list of account records.

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [QueryHeader](../miscellaneous/queryheader.md) | Standard info sent from client to node, including the signed payment, and what kind of response is requested \(cost, state proof, both, or neither\). |
| accountID | [AccountID](../basic-types/accountid.md) | The account ID for which information is requested |

## CryptoGetInfoResponse

Response when the client sends the node CryptoGetInfoQuery

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [ResponseHeader](../miscellaneous/responseheader.md#responseheader) | Standard response from node to client, including the requested fields: cost, or state proof, or both, or neither |
| accountInfo | [CryptoGetInfoResponse.AccountInfo](cryptogetinfo.md#cryptogetinforesponse-accountinfo) | Info about the account \(a state proof can be generated for this\) |

## CryptoGetInfoResponse.AccountInfo

Response when the client sends the node CryptoGetInfoQuery

| Field | Type | Description |
| :--- | :--- | :--- |
| accountID | [AccountID](../basic-types/accountid.md) | The account ID for which this information applies |
| contractAccountID |  | The Contract Account ID comprising of both the contract instance and the cryptocurrency account owned by the contract instance, in the format used by Solidity |
| deleted |  | If true, then this account has been deleted, it will disappear when it expires, and all transactions for it will fail except the transaction to extend its expiration date |
| proxyAccountID | [AccountID](../basic-types/accountid.md) | The Account ID of the account to which this is proxy staked. If proxyAccountID is null, or is an invalid account, or is an account that isn't a node, then this account is automatically proxy staked to a node chosen by the network, but without earning payments. If the proxyAccountID account refuses to accept proxy staking , or if it is not currently running a node, then it will behave as if proxyAccountID was null. |
| proxyReceived |  | The total number of tinybars proxy staked to this account |
| key | [Key](../basic-types/key.md) | The key for the account, which must sign in order to transfer out, or to modify the account in any way other than extending its expiration date. |
| balance |  | The current balance of account in tinybars |
| generateSendRecordThreshold |  | The threshold amount \(in tinybars\) for which an account record is created \(and this account charged for them\) for any send/withdraw transaction. |
| generateReceiveRecordThreshold |  | The threshold amount \(in tinybars\) for which an account record is created \(and this account charged for them\) for any transaction above this amount. |
| receiverSigRequired |  | If true, no transaction can transfer to this account unless signed by this account's key |
| expirationTime | [Timestamp](../miscellaneous/timestamp.md#timestamp) | The TimeStamp time at which this account is set to expire |
| autoRenewPeriod | [Duration](../miscellaneous/duration.md) | The duration for expiration time will extend every this many seconds. If there are insufficient funds, then it extends as long as possible. If it is empty when it expires, then it is deleted. |
| liveHashes | [Claim](cryptoaddclaim.md#claim) | All of the livehashes attached to the account \(each of which is a hash along with the keys that authorized it and can delete it \) |

