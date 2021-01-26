---
description: Hedera Services release information
---

# Hedera Services

| Network | Current Version | Upcoming |
| :--- | :--- | :--- |
| **Mainnet** | 0.10.0 | 0.11.0 |
| **Testnet** | 0.11.0 | 0.12.0 |
| **Previewnet** | 0.11.0 | 0.12.0 |

## Upcoming Releases

## [v0.11.0](https://github.com/hashgraph/hedera-services/releases/tag/v0.11.0)

{% hint style="info" %}
**MAINNET UPDATE SCHEDULED: FEBRUARY 4, 2021**
{% endhint %}

{% hint style="success" %}
**TESTNET UPDATE COMPLETED: JANUARY 26, 2021**
{% endhint %}

In Hedera Services v0.11.0, we upgraded record stream from v2 to v5 and event stream from v3 to v5. The changes are described in [Record and Event Stream File Formats Document](https://docs.hedera.com/guides/docs/record-and-event-stream-file-formats). In [\#784](https://github.com/hashgraph/hedera-services/issues/784), we also made other production and pre-production networks to be similar to mainnet, namely accounts from 900 to 1000 are created if they don't exist.

## Latest Releases

## [v0.10.0](https://github.com/hashgraph/hedera-services/releases/tag/v0.10.0)

{% hint style="success" %}
**MAINNET UPDATE COMPLETED: JANUARY 7, 2021**
{% endhint %}

{% hint style="success" %}
**TESTNET UPDATE COMPLETED: DECEMBER 17, 2020** 
{% endhint %}

In Hedera Services v0.10.0, we improved the usability of the Hedera Token Service \(HTS\) with a `newTotalSupply` field in the receipts of `TokenMint` and `TokenBurn` transactions. Without this field, a client must follow the entire record stream of a token's supply changes to be certain of its supply at the consensus timestamp in the receipt. \(Note that HTS operations are now enabled on Previewnet and Testnet, but remain disabled on Mainnet at this time. Please consult the [SDK documentation](https://docs.hedera.com/452354233115445331/token-service) for HTS semantics.\)

Also for HTS, we added a property `fees.tokenTransferUsageMultiplier` that scales the resource usage assigned to a `CryptoTransfer` that changes token balances. This scaling factor is expected to be set so that the cost of a `CryptoTransfer` that changes two token balances is roughly 10x the cost of a `CryptoTransfer` that changes only two hbar balances.

Apart from HTS, this release drops a restriction on what payer accounts can be used for `CryptoUpdate` transactions that target system accounts. \(That is, accounts with number not greater than `hedera.numReservedSystemEntities`.\) In earlier versions, only three payers were accepted: The target account itself, the system admin account, or the treasury account. Other payers resulted in a status of `AUTHORIZATION_FAILED`. This entire restriction is removed, with one exception---the treasury must pay for a `CryptoUpdate` targeting the treasury.

Apart from these functional changes, we fixed an unintentional change in the naming of the crypto balances CSV file, and improved the usefulness of clients under _test-clients/_ for testing reconnect scenarios.

## [v0.9.0](https://github.com/hashgraph/hedera-services/releases/tag/v0.9.0-rc.1)

{% hint style="success" %}
**MAINNET UPDATE COMPLETED: DECEMBER 3, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPDATE COMPLETED: NOVEMBER 19, 2020**
{% endhint %}

In Hedera Services v0.9.0, we finished the alpha implementation of the Hedera Token Service \(HTS\). Note that all HTS operations are enabled on Previewnet, but remain disabled on Testnet and Mainnet. Please consult the [SDK documentation](https://docs.hedera.com/452354233115445331/token-service) for HTS semantics.

We made several changes to the HAPI protobuf. First, we removed the deprecated `SignatureList` message type. Second, we added a top-level `signedTransactionBytes` field to the `Transaction` message to ensure deterministic transaction hashes across different client libraries; the top-level `bodyBytes` and `sigMap` fields are now deprecated and the already-deprecated `body` field is removed. Third, we deprecated all fields related to non-payer records, include account send and receive thresholds. This followed from the effective removal of non-payer records in v0.8.1.

For the same reason, the semantics of the `CryptoGetRecords` and `ContractGetRecords` queries have also changed. The only queryable records are now those granted to the effective payer of a transaction that was handled while the network property `ledger.keepRecordsInState=true`. Such records have an expiry of 180 seconds. It is important to note that because a contract account can never be the effective payer for a transaction, any `ContractGetRecords` query will always return an empty record list, and we have deprecated the query.

## [v0.8.1](https://github.com/hashgraph/hedera-services/releases/tag/v0.8.1-rc1)

{% hint style="success" %}
**MAINNET UPDATE COMPLETED: OCTOBER 22, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPDATE COMPLETED: OCTOBER 7, 2020**
{% endhint %}

The mainnet release includes the 0.8.0 version updates. 

## [v0.8.0](https://github.com/hashgraph/hedera-services/releases/tag/v0.8.0-rc1)

{% hint style="success" %}
**TESTNET UPDATE COMPLETED: SEPTEMBER 17, 2020**
{% endhint %}

In Hedera Services v0.8.0, we made several minor fixes and improvements. This tag also includes pre-release implementations of several operations for an incipient Hedera Token Service \(HTS\).

**NOTE:** HTS operations will remain disabled in non-development environments for some time. These operations are under active development; please consult `master` for up-to-date semantics.

#### Enhancements

* Deprecated fields related to threshold records in HAPI protobuf  [\#506](https://github.com/hashgraph/hedera-services/issues/506)
* Update Receipt proto to pair each Status with NodeID - Receipt is deleted only when the latest \(duplicate\) transaction expires. `getTxRecord` API will continue to return ALL records with the transaction ID.
* First drafts of `tokenCreate`, `tokenUpdate`, `tokenDelete`, `tokenTransfer`, `tokenFreeze`, `tokenUnfreeze`, `tokenGrantKyc`, `tokenRevokeYc`, `tokenWipe`, and `getTokenInfo` HAPI operations. [\#505](https://github.com/hashgraph/hedera-services/pull/505) and [\#522](https://github.com/hashgraph/hedera-services/pull/522) 

## [v0.7.0](https://github.com/hashgraph/hedera-services/releases/tag/v0.7.0-alpha1)

{% hint style="success" %}
**MAINNET UPDATE COMPLETED: SEPTEMBER 8, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPDATE COMPLETED: AUGUST 20, 2020**
{% endhint %}

In Hedera Services v0.7.0, we’ve moved to Swirlds SDK release `0.7.3` which enables zero-stake nodes to be part of a network without affecting consensus. Hedera Services v0.7.0 migrated to new interfaces and methods provided in this version of the Swirlds SDK. HCS topic running hashes are now calculated including the payer account id. The release includes other minor fixes and improvements.

**Enhancements**

* Migrate to Swirlds SDK release `0.7.3` with appropriate settings and logging configurations [\#347](https://github.com/hashgraph/hedera-services/issues/347), [\#427](https://github.com/hashgraph/hedera-services/issues/427)
* Update HCS topic running hash to include the payer account id [\#88](https://github.com/hashgraph/hedera-services/issues/88)
* Add zero-stake node functionality [\#274](https://github.com/hashgraph/hedera-services/issues/274)
* Add new stats for the average size of HCS submit message transactions that got handled and for counting the number of platform transactions not created per second [\#316](https://github.com/hashgraph/hedera-services/issues/316), [\#334](https://github.com/hashgraph/hedera-services/issues/334)
* Change gRPC CipherSuite to be CNSA compliant [\#215](https://github.com/hashgraph/hedera-services/issues/215)
* Make recordLogPeriod dynamic with a default of 2 seconds [\#315](https://github.com/hashgraph/hedera-services/issues/315)
* Add record with 3-min expiry to effective payer account after handling transaction [\#348](https://github.com/hashgraph/hedera-services/issues/348)
* Enhancements for going open source [\#378](https://github.com/hashgraph/hedera-services/issues/378), [\#379](https://github.com/hashgraph/hedera-services/issues/379)

**Documentation changes**

* Clarify interpretation of response codes `UNKNOWN` and `PLATFORM_TRANSACTION_NOT_CREATED` [\#314](https://github.com/hashgraph/hedera-services/issues/314), [\#394](https://github.com/hashgraph/hedera-services/issues/394)

**Bug fixes**

* Prevent `CryptoCreate` and `CryptoUpdate` transactions from giving an account an empty key [\#58](https://github.com/hashgraph/hedera-services/issues/58), [\#60](https://github.com/hashgraph/hedera-services/issues/60)
* Fix incorrect submitted smart contract transactions count [\#371](https://github.com/hashgraph/hedera-services/issues/371)
* Validate total ledger balance before starting up Services [\#258](https://github.com/hashgraph/hedera-services/issues/258)
* Add a new rolling file to log all queries with controlled maximum rate [\#59](https://github.com/hashgraph/hedera-services/issues/59)
* Other minor bugs [\#373](https://github.com/hashgraph/hedera-services/issues/373)

## [v0.6.0](https://github.com/hashgraph/hedera-services/releases/tag/v0.6.0)

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: AUGUST 6, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: JULY 16, 2020**
{% endhint %}

In Hedera Services v0.6.0, we’ve enhanced the Hedera Consensus Service by supporting [HCS Topic Fragmentation](https://github.com/hashgraph/hedera-services/issues/53). We added, into the `ConsensusSubmitMessageTransactionBody`, an optional field for the current chunk information. For every chunk, the payer account that is part of the `initialTransactionID` must match the Payer Account of this transaction. The entire `initialTransactionID` should match the `transactionID` of the first chunk, but this is not checked or enforced by Hedera except when the chunk number is 1.

**Enhancements**

* Add support for HCS Topic Fragmentation

**Documentation changes**

* Protobuf v0.6.0 with HAPI doc update to support HCS Topic Fragmentation 

## \*\*\*\*[**v0.5.8**](https://github.com/hashgraph/hedera-services/releases/tag/oa-release-r5-rc8)\*\*\*\*

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: JUNE 18, 2020**  
  
v0.5.8 includes all of the updates found in [v0.5.0](services.md#v-0-5-0)
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: JUNE 8, 2020**
{% endhint %}

Version 0.5.8 includes a patch which addresses the resilience of peer-to-peer networking in the hashgraph consensus platform.

## **v0.5.0**

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: MAY 5, 2020**
{% endhint %}

In Hedera Services v0.5.0, we’ve added TLS for trusted communication with nodes on the Hedera network. For better security, only TLS v1.2 and v1.3 with TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384 and TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 cipher suites are allowed.   
  
We’ve added new metadata in the Hedera NodeAddressBook, accessible in system file 0.0.101. The versions of the node software and gRPC Hedera API \(HAPI\) are now queryable via GetVersionInfo under the new NetworkService for node and network-scoped operations.   
  
For Hedera Consensus Service, we’ve updated the topic running hash calculation to use the SHA-384 hash of the submitted message, rather than the message itself. This reduces the storage requirements needed to validate the hash of a topic. The record of a ConsensusSubmitMessage transaction that uses the new hashing scheme will have a new topicRunningHashVersion field in its receipt. The value of the field will be 2.   
  
Hedera File Service also has several fixes of note. First, we enabled immutable files. Second, we relaxed the signing requirements for a FileDelete transaction to match the semantics of a revocation service. Third, we fixed a fee calculation bug that overcharged certain FileUpdate transactions.   
  
For Hedera Smart Contract Service, we’ve improved visibility into transactions that create child contracts using the new keyword by putting created ids in the record of the transaction; and we now propagate parent contract metadata to created children.   
  
Finally, if you use the throttle properties in system file 0.0.121 to estimate network performance limits, you will also be interested in a new standardized format of those properties. The lists below contain these and other minor updates, bug fixes, and documentation changes. 

**Enhancements** 

* Add support for TLS
* Expand address book metadata
* Return all created contract ids 
* Propagate creator contract metadata
* Introduce GetVersionInfo query 
* Standardize throttle configuration 
* Enforce file.encoding=utf-8 on startup 
* Make duration properties inclusive for readability

**Bug fixes** 

* Use message SHA-384 hash in running hash 
* Enable immutable files  
* Relax FileDelete signing requirements 
* Fix sbh calculation in FileUpdate 
* Return metadata for deleted files
* Enforce receiver signing requirements during contract execution 
* Reject invalid CryptoGetInfo
* Reject CryptoCreate with empty key
* Return NOT\_SUPPORTED for state proof queries 
* Waive fees for 0.0.57 updating 0.0.111
* Waive signing requirements for 0.0.55 updating 0.0.121/0.0.122
* Waive all fees for 0.0.2
* Do not throttle system accounts 

**Documentation changes** 

* Replace “claim” with “livehash” as appropriate
* Standardize and clarify HAPI doc

## v0.4.1

* Software update includes the ability for Hedera to dynamically set throttles on network transaction types. 
* The following throttles would be updated to: 1000 submit messages per second and 5 topic creates per second. 
* Reassigning of new Council Member nodes 

## v0.4.0

* Say hello to the Hedera Consensus Service! This release is the first to include HCS, allowing verifiable timestamping and ordering of application messages.  
* Network pricing has been updated to include HCS transactions and queries 
* Network throttle for HCS set to 1000 tps for submitting messages, and 100 tps for each of the other HCS operations. 
* Improved end to end testing.
* General code clean up and refactoring.
* ContractCall - TransactionReceipt response to ContractCall no longer includes the contractID called
* CryptoUpdate - TransactionReceipt response to CryptoUpdate no longer includes the accountID updated
* CryptoTransfer – CryptoTransfer transactions resulting in INSUFFICIENT\_ACCOUNT\_BALANCE error no longer list Transfers in the TransactionRecord transferList that were not applied

#### Miscellaneous 

#### SDKs 

* Java SDK has been updated to support the Hedera Consensus Service
* JavaScript/Typescript SDK has reached version 1.0.0, supporting all four mainnet services
* JavaScript/Typescript SDK supports both running in the browser \(with Envoy Proxy\) and in Node.
* Go SDK now supports all four mainnet services.

**Fees**

* Transfer list within transaction records now shows only a single net amount in or out for each account, reflecting both transfers and any fees paid.
* Fixed bug in fee schedule that had resulted in fees for ContractCallLocal, ContractGetBytecode, and getVersion queries being undercharged by ~33%
* You may get more information regarding transaction record fees [here](https://docs.hedera.com/guides/mainnet/fees/transaction-records).

#### SDK Extension Components

* The Hedera SDK Extension Components \(SXC\) is an open sourced set of pre-built components that aim to provide additional functionality over and above HCS to make it easier and quicker to develop applications, particularly if they require secure communications between participants.
* Components use the Hedera Java SDK to communicate with the Hedera Consensus Service.
* Learn more about Hedera SXC [here](https://github.com/hashgraph/hedera-hcs-sxc).

