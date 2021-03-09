# TokenRelationship

Token's information related to the given Account.

| Field | Type | Description |
| :--- | :--- | :--- |
| `tokenId` | [TokenID](tokenid.md) | A unique token id |
| `symbol` | string | The Symbol of the token |
| `balance` | uint64 | The balance that the Account holds in the smallest denomination |
| `kycStatus` | TokenKycStatus | The KYC status of the account \(KycNotApplicable, Granted or Revoked\). If the token does not have KYC key, KycNotApplicable is returned |
| `freezeStatus` | TokenFreezeStatus | The Freeze status of the account \(FreezeNotApplicable, Frozen or Unfrozen\). If the token does not have Freeze key, FreezeNotApplicable is returned |
| `decimals` | uint32 | Tokens divide into 10 decimal pieces |



