# Hedera Services

| Network | Version | vNext |
| :--- | :--- | :--- |
| **Mainnet** | 0.4.1  | 0.5.8 |
| **Testnet** | 0.5.0 | 0.5.8 |
| **Previewnet** | Coming soon... |  |

## Upcoming Releases

## **v0.5.8**

{% hint style="info" %}
**TESTNET SCHEDULED: TBD**
{% endhint %}

{% hint style="info" %}
**MAINNET SCHEDULED: TBD**  
  
v0.5.8 includes all of the updates found in [v0.5.0](services.md#v-0-5-0)
{% endhint %}

Version 0.5.8 includes a patch which addresses the resilience of peer-to-peer networking in the hashgraph consensus platform.

## Latest Releases

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

