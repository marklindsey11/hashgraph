# Transaction

A single signed transaction, including all its signatures. The SignatureList will have a Signature for each Key in the transaction, either explicit or implicit, in the order that they appear in the transaction. For example, a CryptoTransfer will first have a Signature corresponding to the Key for the paying account, followed by a Signature corresponding to the Key for each account that is sending or receiving cryptocurrency in the transfer. Each Transaction should not have more than 50 levels.  
The SignatureList field is deprecated and succeeded by SignatureMap.

## Transaction

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| signedTransactionBytes |  | SignedTransaction serialized into bytes |  |
| bodyBytes |  | TransactionBody serialized into bytes, which needs to be signed |  |
| sigMap | [SignatureMap](https://github.com/hashgraph/hedera-protobuf/tree/hedera-protobuf-java-api-0.9.0-alpha5#SignatureMap) | The signatures on the body with the new format, to authorize the transaction |  |

[Top](https://github.com/hashgraph/hedera-protobuf/tree/hedera-protobuf-java-api-0.9.0-alpha5#top)

## TransactionBody.proto

A single transaction. All transaction types are possible here.

#### TransactionBody

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| transactionID | TransactionID | The ID for this transaction, which includes the payer's account \(the account paying the transaction fee\). If two transactions have the same transactionID, they won't both have an effect |  |
| nodeAccountID | AccountID | The account of the node that submits the client's transaction to the network |  |
| transactionFee |  | The maximum transaction fee the client is willing to pay |  |
| transactionValidDuration | Duration | The transaction is invalid if consensusTimestamp &gt; transactionID.transactionValidStart + transactionValidDuration |  |
| generateRecord |  | Should a record of this transaction be generated? \(A receipt is always generated, but the record is optional\) |  |
| memo |  | Any notes or descriptions that should be put into the record \(max length 100\) |  |
| data | oneof |  |  |
|  | contractCall | ContractCallTransactionBody | Calls a function of a contract instance |
|  | contractCreateInstance | ContractCreateTransactionBody | Creates a contract instance |
|  | contractUpdateInstance | ContractUpdateTransactionBody | Updates a contract |
|  | contractDeleteInstance | ContractDeleteTransactionBody | Delete contract and transfer remaining balance into specified account |
|  | cryptoAddLiveHash | CryptoAddLiveHashTransactionBody | Attach a new livehash to an account |
|  | cryptoCreateAccount | CryptoCreateTransactionBody | Create a new cryptocurrency account |
|  | cryptoDelete | CryptoDeleteTransactionBody | Delete a cryptocurrency account \(mark as deleted, and transfer hbars out\) |
|  | cryptoDeleteLiveHash | CryptoDeleteLiveHashTransactionBody | Remove a livehash from an account |
|  | cryptoTransfer | CryptoTransferTransactionBody | Transfer amount between accounts |
|  | cryptoUpdateAccount | CryptoUpdateTransactionBody | Modify information such as the expiration date for an account |
|  | fileAppend | FileAppendTransactionBody | Add bytes to the end of the contents of a file |
|  | fileCreate | FileCreateTransactionBody | Create a new file |
|  | fileDelete | FileDeleteTransactionBody | Delete a file \(remove contents and mark as deleted until it expires\) |
|  | fileUpdate | FileUpdateTransactionBody | Modify information such as the expiration date for a file |
|  | systemDelete | SystemDeleteTransactionBody | Hedera administrative deletion of a file or smart contract |
|  | systemUndelete | SystemUndeleteTransactionBody | To undelete an entity deleted by SystemDelete |
|  | freeze | FreezeTransactionBody | Freeze the nodes |
|  | consensusCreateTopic | ConsensusCreateTopicTransactionBody | Creates a topic |
|  | consensusUpdateTopic | ConsensusUpdateTopicTransactionBody | Updates a topic |
|  | consensusDeleteTopic | ConsensusDeleteTopicTransactionBody | Deletes a topic |
|  | consensusSubmitMessage | ConsensusSubmitMessageTransactionBody | Submits message to a topic |
|  | uncheckedSubmit | UncheckedSubmitBody |  |
|  | tokenCreation | TokenCreateTransactionBody | Creates a token instance |
|  | tokenTransfers | TokenTransfersTransactionBody | Transfers tokens between accounts |
|  | tokenFreeze | TokenFreezeAccountTransactionBody | Freezes account not to be able to transact with a token |
|  | tokenUnfreeze | TokenUnfreezeAccountTransactionBody | Unfreezes account for a token |
|  | tokenGrantKyc | TokenGrantKycTransactionBody | Grants KYC to an account for a token |
|  | tokenRevokeKyc | TokenRevokeKycTransactionBody | Revokes KYC of an account for a token |
|  | tokenDeletion | TokenDeleteTransactionBody | Deletes a token instance |
|  | tokenUpdate | TokenUpdateTransactionBody | Updates a token instance |
|  | tokenMint | TokenMintTransactionBody | Mints new tokens to a token's treasury account |
|  | tokenBurn | TokenBurnTransactionBody | Burns tokens from a token's treasury account |
|  | tokenWipe | TokenWipeAccountTransactionBody | Wipes amount of tokens from an account |
|  | tokenAssociate | TokenAssociateTransactionBody | Associate tokens to an account |
|  | tokenDissociate | TokenDissociateTransactionBody | Dissociate tokens from an account |

