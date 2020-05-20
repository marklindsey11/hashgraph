# TransactionBody

## TransactionBody

A single transaction. All transaction types are possible here.

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| transactionID | [TransactionID](../basic-types/transactionid.md) | The ID for this transaction, which includes the payer's account \(the account paying the transaction fee\). If two transactions have the same transactionID, they won't both have an effect |  |
| nodeAccountID | [AccountID](../basic-types/accountid.md) | The account of the node that submits the client's transaction to the network |  |
| transactionFee |  | The maximum transaction fee the client is willing to pay, which is split between the network and the node |  |
| transactionValidDuration | [Duration](duration.md) | The transaction is invalid if consensusTimestamp &gt; transactionID.transactionValidStart + transactionValidDuration |  |
| generateRecord |  | Should a record of this transaction be generated? \(A receipt is always generated, but the record is optional\) |  |
| memo |  | Any notes or descriptions that should be put into the record \(max length 100\) |  |
| data | oneof |  |  |
|  | contractCall | ContractCallTransactionBody | Contains the call a function of a contract instance |
|  | contractCreateInstance | [ContractCreateTransactionBody](../smart-contracts/contractcreate.md#contractcreatetransactionbody) | Contains the create data a contract instance |
|  | contractUpdateInstance | [ContractUpdateTransactionBody](../smart-contracts/contractupdate.md#contractupdatetransactionbody) | Contains contract modify info such as expiration date for a contract instance |
|  | contractDeleteInstance | [ContractDeleteTransactionBody](../smart-contracts/contractdelete.md#contractdeletetransactionbody) | Delete contract and transfer remaining balance into specified account |
|  | cryptoAddLiveHash | [CryptoAddClaimTransactionBody](../cryptocurrency-accounts/cryptoaddclaim.md#cryptoaddlivehashtransactionbody) | Attach a new claim to an account |
|  | cryptoCreateAccount | [CryptoCreateTransactionBody](../cryptocurrency-accounts/cryptocreate.md#cryptocreatetransactionbody) | Create a new cryptocurrency account |
|  | cryptoDelete | [CryptoDeleteTransactionBody](../cryptocurrency-accounts/cryptodelete.md#cryptodeletetransactionbody) | Delete a cryptocurrency account \(mark as deleted, and transfer hbars out\) |
|  | cryptoDeleteLiveHash | [CryptoDeleteClaimTransactionBody](../cryptocurrency-accounts/cryptodeletelivehash.md#cryptodeletelivehashtransactionbody) | Remove a claim from an account |
|  | cryptoTransfer | [CryptoTransferTransactionBody](../cryptocurrency-accounts/cryptotransfer.md#cryptotransfertransactionbody) | Transfer amount between accounts |
|  | cryptoUpdateAccount | [CryptoUpdateTransactionBody](../cryptocurrency-accounts/cryptoupdate.md#cryptoupdatetransactionbody) | Modify information such as the expiration date for an account |
|  | fileAppend | [FileAppendTransactionBody](../file-service/filecreate.md#filecreatetransactionbody) | Add bytes to the end of the contents of a file |
|  | fileCreate | [FileCreateTransactionBody](../file-service/filecreate.md#filecreatetransactionbody) | Create a new file |
|  | fileDelete | [FileDeleteTransactionBody](../file-service/filedelete.md#filedeletetransactionbody) | Delete a file \(remove contents and mark as deleted until it expires\) |
|  | fileUpdate | [FileUpdateTransactionBody](../file-service/fileupdate.md#fileupdatetransactionbody) | Modify information such as the expiration date for a file |
|  | systemDelete | [SystemDeleteTransactionBody](systemdelete.md#systemdeletetransactionbody) | Hedera multisig system deletes a file or smart contract |
|  | systemUndelete | [SystemUndeleteTransactionBody](systemundelete.md#systemundeletetransactionbody) | To undelete an entity deleted by SystemDelete |
|  | freeze | [FreezeTransactionBody](freeze.md#freezetransactionbody) | Freeze the nodes |
|  | consensusCreateTopic | [ConsensusCreateTopicTransactionBody](../consensus-service/consensuscreatetopic.md#consensuscreatetopictransactionbody) | Create a topic |
|  | consensusUpdateTopic | [ConsensusUpdateTopicTransactionBody](../consensus-service/consensusupdatetopic.md#consensusupdatetopictransactionbody) | Update a topic |
|  | consensusDeleteTopic | [ConsensusDeleteTopicTransactionBody](../consensus-service/consensusdeletetopic.md#consensusdeletetopictransactionbody) | Delete a topic |
|  | consensusSubmitMessage | [ConsensusSubmitMessageTransactionBody](../consensus-service/consensussubmitmessage.md#consensussubmitmessagetransactionbody) | Submit a message to a topic |

