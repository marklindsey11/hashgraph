# TokenUpdate

Updates an already created Token.

If no value is given for a field, that field is left unchanged. For an immutable tokens \(that is, a token created without an adminKey\), only the expiry may be updated. Setting any other field in that case will cause the transaction status to resolve to TOKEN\_IS\_IMMUTABlE.

## TokenUpdateTransactionBody

| Field | Type | Description | Signature Required |
| :--- | :--- | :--- | :--- |
| token | [TokenID](../basic-types/tokenid.md) | The Token to be updated  | N/A |
| symbol | string | The new Symbol of the Token. Must be UTF-8 capitalized alphabetical string identifying the token.  | N/A |
| name | string | The new Name of the Token. Must be a string of ASCII characters.  | N/A |
| treasury | [AccountID](../basic-types/accountid.md) | The new Treasury account of the Token. If the provided treasury account is not existing or deleted, the response will be INVALID\_TREASURY\_ACCOUNT\_FOR\_TOKEN. If successful, the Token balance held in the previous Treasury Account is transferred to the new one.  | If updated, required |
| adminKey | [Key](../basic-types/key.md) | The new Admin key of the Token. If Token is immutable, transaction will resolve to TOKEN\_IS\_IMMUTABlE.  | If updated, required |
| kycKey | [Key](../basic-types/key.md) | The new KYC key of the Token. If Token does not have currently a KYC key, transaction will resolve to TOKEN\_HAS\_NO\_KYC\_KEY.  | If updated, required |
| freezeKey | [Key](../basic-types/key.md) | The new Freeze key of the Token. If the Token does not have currently a Freeze key, transaction will resolve to TOKEN\_HAS\_NO\_FREEZE\_KEY.  | If updated, required |
| wipeKey | [Key](../basic-types/key.md) | The new Wipe key of the Token. If the Token does not have currently a Wipe key, transaction will resolve to TOKEN\_HAS\_NO\_WIPE\_KEY.  | If updated, required |
| supplyKey | [Key](../basic-types/key.md) | The new Supply key of the Token. If the Token does not have currently a Supply key, transaction will resolve to TOKEN\_HAS\_NO\_SUPPLY\_KEY.  | If updated, required |
| autoRenewAccount | [AccountID](../basic-types/accountid.md) | The new account which will be automatically charged to renew the token's expiration, at autoRenewPeriod interval.  | N/A |
| autoRenewPeriod | uint64 | The new interval at which the auto-renew account will be charged to extend the token's expiry.  | N/A |
| expiry | uint64 | The new expiry time of the token. Expiry can be updated even if admin key is not set. If the provided expiry is earlier than the current token expiry, transaction wil resolve to INVALID\_EXPIRATION\_TIME  | N/A |

