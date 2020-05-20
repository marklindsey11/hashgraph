# ResponseCode

## ResponseCodeEnum

| Enum Name | Description |
| :--- | :--- |
| OK | The transaction passed the precheck validations. |
| INVALID\_TRANSACTION | For any error not handled by specific error codes listed below. |
| PAYER\_ACCOUNT\_NOT\_FOUND | Payer account does not exist. |
| INVALID\_NODE\_ACCOUNT | Node Account provided does not match the node account of the node the transaction was submitted to. |
| TRANSACTION\_EXPIRED | Pre-Check error when TransactionValidStart + transactionValidDuration is less than current consensus time. |
| INVALID\_TRANSACTION\_START | Transaction start time is greater than current consensus time |
| INVALID\_TRANSACTION\_DURATION | valid transaction duration is a positive non zero number that does not exceed 120 seconds |
| INVALID\_SIGNATURE | The transaction signature is not valid |
| MEMO\_TOO\_LONG | Transaction memo size exceeded 100 bytes |
| INSUFFICIENT\_TX\_FEE | The fee provided in the transaction is insufficient for this type of transaction |
| INSUFFICIENT\_PAYER\_BALANCE | The payer account has insufficient cryptocurrency to pay the transaction fee |
| DUPLICATE\_TRANSACTION | This transaction ID is a duplicate of one that was submitted to this node or reached consensus in the last 180 seconds \(receipt period\) |
| BUSY | If API is throttled out |
| NOT\_SUPPORTED | The API is not currently supported |
| INVALID\_FILE\_ID | The file id is invalid or does not exist |
| INVALID\_ACCOUNT\_ID | The account id is invalid or does not exist |
| INVALID\_CONTRACT\_ID | The contract id is invalid or does not exist |
| INVALID\_TRANSACTION\_ID | Transaction id is not valid |
| RECEIPT\_NOT\_FOUND | Receipt for given transaction id does not exist |
| RECORD\_NOT\_FOUND | Record for given transaction id does not exist |
| INVALID\_SOLIDITY\_ID | The solidity id is invalid or entity with this solidity id does not exist |
| UNKNOWN | Transaction hasn't yet reached consensus, or has already expired |
| SUCCESS | The transaction succeeded |
| FAIL\_INVALID | There was a system error and the transaction failed because of invalid request parameters. |
| FAIL\_FEE | There was a system error while performing fee calculation, reserved for future. |
| FAIL\_BALANCE | There was a system error while performing balance checks, reserved for future. |
| KEY\_REQUIRED | Key not provided in the transaction body |
| BAD\_ENCODING | Unsupported algorithm/encoding used for keys in the transaction |
| INSUFFICIENT\_ACCOUNT\_BALANCE | When the account balance is not sufficient for the transfer |
| INVALID\_SOLIDITY\_ADDRESS | During an update transaction when the system is not able to find the Users Solidity address |
| INSUFFICIENT\_GAS | Not enough gas was supplied to execute transaction |
| CONTRACT\_SIZE\_LIMIT\_EXCEEDED | contract byte code size is over the limit |
| LOCAL\_CALL\_MODIFICATION\_EXCEPTION | local execution \(query\) is requested for a function which changes state |
| CONTRACT\_REVERT\_EXECUTED | Contract REVERT OPCODE executed |
| CONTRACT\_EXECUTION\_EXCEPTION | For any contract execution related error not handled by specific error codes listed above. |
| INVALID\_RECEIVING\_NODE\_ACCOUNT | In Query validation, account with +ve\(amount\) value should be Receiving node account, the receiver account should be only one account in the list |
| MISSING\_QUERY\_HEADER | Header is missing in Query request |
| ACCOUNT\_UPDATE\_FAILED | The update of the account failed |
| INVALID\_KEY\_ENCODING | Provided key encoding was not supported by the system |
| NULL\_SOLIDITY\_ADDRESS | null solidity address |
| CONTRACT\_UPDATE\_FAILED | update of the contract failed |
| INVALID\_QUERY\_HEADER | the query header is invalid |
| INVALID\_FEE\_SUBMITTED | Invalid fee submitted |
| INVALID\_PAYER\_SIGNATURE | Payer signature is invalid |
| KEY\_NOT\_PROVIDED | The keys were not provided in the request. |
| INVALID\_EXPIRATION\_TIME | Expiration time provided in the transaction was invalid. |
| NO\_WACL\_KEY | WriteAccess Control Keys are not provided for the file |
| FILE\_CONTENT\_EMPTY | The contents of file are provided as empty. |
| INVALID\_ACCOUNT\_AMOUNTS | The crypto transfer credit and debit do not sum equal to 0 |
| EMPTY\_TRANSACTION\_BODY | Transaction body provided is empty |
| INVALID\_TRANSACTION\_BODY | Invalid transaction body provided |
| INVALID\_SIGNATURE\_TYPE\_MISMATCHING\_KEY | the type of key \(base ed25519 key, KeyList, or ThresholdKey\) does not match the type of signature \(base ed25519 signature, SignatureList, or ThresholdKeySignature\) |
| INVALID\_SIGNATURE\_COUNT\_MISMATCHING\_KEY | the number of key \(KeyList, or ThresholdKey\) does not match that of signature \(SignatureList, or ThresholdKeySignature\). e.g. if a keyList has 3 base keys, then the corresponding signatureList should also have 3 base signatures. |
| EMPTY\_LIVEHASH\_BODY | the claim body is empty |
| EMPTY\_LIVE\_HASH | the hash for the claim is empty |
| EMPTY\_LIVEHASH\_KEYS | the key list is empty |
| INVALID\_LIVE\_HASH\_SIZE | the size of the claim hash is not 48 bytes |
| EMPTY\_QUERY\_BODY | the query body is empty |
| EMPTY\_LIVE\_QUERY | the crypto claim query is empty |
| LIVEHASH\_NOT\_FOUND | the crypto claim doesn't exists in the file system. It expired or was never persisted. |
| ACCOUNT\_ID\_DOES\_NOT\_EXIST | the account id passed has not yet been created. |
| LIVEHASH\_ALREADY\_EXISTS | the claim hash already exists |
| INVALID\_FILE\_WACL | File WACL keys are invalid |
| SERIALIZATION\_FAILED | Serialization failure |
| TRANSACTION\_OVERSIZE | The size of the Transaction is greater than transactionMaxBytes |
| TRANSACTION\_TOO\_MANY\_LAYERS | The Transaction has more than 50 levels |
| CONTRACT\_DELETED | Contract is marked as deleted |
| PLATFORM\_NOT\_ACTIVE | the platform node is either disconnected or lagging behind. |
| KEY\_PREFIX\_MISMATCH | one public key matches more than one prefixes on the signature map |
| PLATFORM\_TRANSACTION\_NOT\_CREATED | transaction not created by platform due to either large backlog or message size exceeded transactionMaxBytes |
| INVALID\_RENEWAL\_PERIOD | auto renewal period is not a positive number of seconds |
| INVALID\_PAYER\_ACCOUNT\_ID | the response code when a smart contract id is passed for a crypto API request |
| ACCOUNT\_DELETED | the account has been marked as deleted |
| FILE\_DELETED | the file has been marked as deleted |
| ACCOUNT\_REPEATED\_IN\_ACCOUNT\_AMOUNTS | same accounts repeated in the transfer account list |
| SETTING\_NEGATIVE\_ACCOUNT\_BALANCE | attempting to set negative balance value for crypto account |
| OBTAINER\_REQUIRED | when deleting smart contract that has crypto balance either transfer account or transfer smart contract is required |
| OBTAINER\_SAME\_CONTRACT\_ID | when deleting smart contract that has crypto balance you can not use the same contract id as transferContractId as the one being deleted |
| OBTAINER\_DOES\_NOT\_EXIST | transferAccountId or transferContractId specified for contract delete does not exist |
| MODIFYING\_IMMUTABLE\_CONTRACT | attempting to modify \(update or delete a immutable smart contract, i.e. one created without a admin key\) |
| FILE\_SYSTEM\_EXCEPTION | Unexpected exception thrown by file system functions |
| AUTORENEW\_DURATION\_NOT\_IN\_RANGE | the duration is not a subset of \[MINIMUM\_AUTORENEW\_DURATION,MAXIMUM\_AUTORENEW\_DURATION\] |
| ERROR\_DECODING\_BYTESTRING | Decoding the smart contract binary to a byte array failed. Check that the input is a valid hex string. |
| CONTRACT\_FILE\_EMPTY | File to create a smart contract was of length zero |
| CONTRACT\_BYTECODE\_EMPTY | Bytecode for smart contract is of length zero |
| INVALID\_INITIAL\_BALANCE | Attempt to set negative initial balance |
| INVALID\_RECEIVE\_RECORD\_THRESHOLD | attempt to set negative receive record threshold |
| INVALID\_SEND\_RECORD\_THRESHOLD | attempt to set negative send record threshold |
| ACCOUNT\_IS\_NOT\_GENESIS\_ACCOUNT | Special Account Operations should be performed by only Genesis account, return this code if it is not Genesis Account |
| PAYER\_ACCOUNT\_UNAUTHORIZED | The fee payer account doesn't have permission to submit such Transaction |
| INVALID\_FREEZE\_TRANSACTION\_BODY | FreezeTransactionBody is invalid |
| FREEZE\_TRANSACTION\_BODY\_NOT\_FOUND | FreezeTransactionBody does not exist |
| TRANSFER\_LIST\_SIZE\_LIMIT\_EXCEEDED | Exceeded the number of accounts \(both from and to\) allowed for crypto transfer list |
| RESULT\_SIZE\_LIMIT\_EXCEEDED | Smart contract result size greater than specified maxResultSize |
| NOT\_SPECIAL\_ACCOUNT | The payer account is not a special account\(account 0.0.55\) |
| CONTRACT\_NEGATIVE\_GAS | Negative gas was offered in smart contract call |
| CONTRACT\_NEGATIVE\_VALUE | Negative value / initial balance was specified in a smart contract call / create |
| INVALID\_FEE\_FILE | Failed to update fee file |
| INVALID\_EXCHANGE\_RATE\_FILE | Failed to update exchange rate file |
| INSUFFICIENT\_LOCAL\_CALL\_GAS | Payment tendered for contract local call cannot cover both the fee and the gas |
| ENTITY\_NOT\_ALLOWED\_TO\_DELETE | Entities with Entity ID below 1000 are not allowed to be deleted |
| AUTHORIZATION\_FAILED | Violating one of these rules: 1\) treasury account can update all entities below 0.0.1000, 2\) account 0.0.50 can update all entities from 0.0.51 - 0.0.80, 3\) Network Function Master Account A/c 0.0.50 - Update all Network Function accounts & perform all the Network Functions listed below, 4\) Network Function Accounts: i\) A/c 0.0.55 - Update Address Book files \(0.0.101/102\), ii\) A/c 0.0.56 - Update Fee schedule \(0.0.111\), iii\) A/c 0.0.57 - Update Exchange Rate \(0.0.112\). |
| FILE\_UPLOADED\_PROTO\_INVALID | Fee Schedule Proto uploaded but not valid \(append or update is required\) |
| FILE\_UPLOADED\_PROTO\_NOT\_SAVED\_TO\_DISK | Fee Schedule Proto uploaded but not valid \(append or update is required\) |
| FEE\_SCHEDULE\_FILE\_PART\_UPLOADED | Fee Schedule Proto File Part uploaded |
| EXCHANGE\_RATE\_CHANGE\_LIMIT\_EXCEEDED | The change on Exchange Rate exceeds Exchange\_Rate\_Allowed\_Percentage |
| MAX\_CONTRACT\_STORAGE\_EXCEEDED | Contract permanent storage exceeded the currently allowable limit |
| MAX\_GAS\_LIMIT\_EXCEEDED | Gas exceeded currently allowable gas limit per transaction |
| MAX\_FILE\_SIZE\_EXCEEDED | File size exceeded the currently allowable limit |
| INVALID\_TOPIC\_ID | The Topic ID specified is not in the system. |
| INVALID\_ADMIN\_KEY |  |
| INVALID\_SUBMIT\_KEY |  |
| UNAUTHORIZED | An attempted operation was not authorized \(ie - a deleteTopic for a topic with no adminKey\). |
| INVALID\_TOPIC\_MESSAGE | A ConsensusService message is empty. |
| INVALID\_AUTORENEW\_ACCOUNT | The autoRenewAccount specified is not a valid, active account. |
| AUTORENEW\_ACCOUNT\_NOT\_ALLOWED | An adminKey was not specified on the topic, so there must not be an autoRenewAccount. |
| TOPIC\_EXPIRED | The topic has expired, was not automatically renewed, and is in a 7 day grace period before the topic will be deleted unrecoverably. This error response code will not be returned until autoRenew functionality is supported by HAPI. |

