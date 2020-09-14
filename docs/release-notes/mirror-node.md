---
description: Hedera mirror node release notes
---

# Mirror Node

| Network | Current Version | Upcoming Version |
| :--- | :--- | :--- |
| **Mainnet** | 0.17.3 | 0.18.0 |
| **Testnet** | 0.17.3 | 0.18.0 |

## Upcoming Releases

## [v0.18.1](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.18.1)

Contains a small change to the State Proof Alpha REST API to only return the current address book for now.

## [v0.18.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.18.0)

Building upon the availability of the [State Proof Alpha REST API](https://github.com/hashgraph/hedera-mirror-node/blob/v0.18.0/docs/design/stateproofalpha.md) in the last release, we've added [sample code](https://github.com/hashgraph/hedera-mirror-node/blob/v0.18.0/hedera-mirror-rest/state-proof-demo) in JavaScript to retrieve the state proof from a mirror node and locally verify it. This allows users to obtain cryptographic proof that a particular transaction took place on Hedera. The validity of the proof can be checked independently to ensure that the supermajority of Hedera mainnet stake had reached consensus on that transaction. Similar to the promise of the ultimate state proofs, the user can trust this state proof alpha served by the mirror nodes, even when the user does not trust the mirror nodes.

Importer can now be configured to connect to Amazon S3 using temporary security credentials via [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html). With this, a user that does not have permission to access an AWS resource can request a temporary role that will grant them that permission. See the [configuration documentation](https://github.com/hashgraph/hedera-mirror-node/blob/v0.18.0/docs/configuration.md#connect-to-s3-with-assumerole) for more information.

Importer also added two new properties to control the subset of data it should download and validate. The `hedera.mirror.importer.startDate` property can be used to exclude data from before this date and "fast-forward" to the point in time of interest. By default, the `startDate` will be set to the current time so mirror node operators can get up and running quicker with the latest data and reduce cloud storage retrieval costs. Note that this property only applies on the importer's first startup and can't be changed after that. The `hedera.mirror.importer.endDate` property can be used to exclude data after this date and halt the importer. By default it is set to a date far in the future so it will effectively never stop.

### Breaking Changes

The aforementioned `startDate` property does change how the mirror node operators on initial start from previous releases. By defaulting to now, users standing up a new mirror node will no longer retrieve all historical data and will instead only retrieve the latest data. Current users upgrading to this release will not be affected even if their data ingest is not fully caught up since this property only applies if the database is empty like it is on first start. To revert to the previous behavior, a date in the past can be specified like the Unix epoch `1970-01-01T00:00:00Z`.

## Latest Releases

## [v0.17.3](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.17.3)

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: SEPTEMBER 14. 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: SEPTEMBER 3, 2020** 
{% endhint %}

This release contains the port of a bug fix to better manage the `VertxException: Thread blocked` issue seen in [\#945](https://github.com/hashgraph/hedera-mirror-node/issues/945)

## [v0.17.2](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.17.2)

A small bug fix to better support resetting the mirror node when a stream reset is performed on the network environment

## [v0.17.1](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.17.1)

A small fix to correct a performance regression with not properly caching a heavily used query.

## [v0.17.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.17.0)

This release adds support for the storage of the network address books from file `0.0.101` and `0.0.102`in the mirror node database.  
The mirror node will now retrieve file address book contents which include node identifiers and their public keys from the database instead of the file system at startup.

This sets the stage for an additional feature which is the State Proof alpha REST API at `/transactions/${transactionId}/stateproof`.  
With this release it is possible to request the address book, record file and signature files that contain the contents of a transaction and allow for cryptographic verification of the transaction. Mirror node users can now actively verify submitted transactions for themselves.

Other changes include support for continuous deployment \(CD\) using [Github Actions](https://github.com/features/actions) that use [FluxCD](https://fluxcd.io/) to deploy master versions to a Kubernetes cluster. Additionally, this release includes fixes to the database copy operation optimization and improved handling of buffer size used when copying large topic messages.

## [v0.16.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.16.0)

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: AUGUST 18, 2020**
{% endhint %}

This release includes the foundation for some larger features to come. Notably, cloud bucket names are now set based on network specifications and users no longer need to explicitly state bucket names for demo, test and main networks. The `record_file` table contents are also expanded to include the start and end consensus timestamps of their containing transactions. The `record_file` table also saw a clean up to remove the path to the file.

Additionally, this release streamlines the helm chart architecture with a common chart for shared resources. It also adds dependabot to facilitate dependency update management. The parser was also update to handle signature files across multiple time bucket groups for greater parsing robustness.

Memory improvements were also made in the parser to improve ingestion performance. Due to performance pg notify was also removed in favor of direct psql notify to support faster streaming of incoming topic messages.

## [v0.15.3](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.15.3)

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: JULY 29, 2020**
{% endhint %}

Works around an issue sending large JSON payloads via pg\_notify by ignoring them for now. This occurs when a consensus message is sent with a message that exceeds 5824 bytes, which is also very close to the protobuf limit.

## [v0.15.2](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.15.2)

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: JULY 29, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: JULY 20, 2020**
{% endhint %}

This release improves the topic message ingest rate that regressed in the previous release. This is just a stop gap and future releases will increase this further.

## [v0.15.1](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.15.1)

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: JULY 29, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: JULY 15, 2020**
{% endhint %}

A hot fix release to address two high priority parsing errors with the new consensus message chunk header.

## [v0.15.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.15.0)

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: JULY 29, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: JULY 15, 2020**
{% endhint %}

This release adds support for HCS topic fragmentation that will soon be rolled out to main nodes in the 0.6.0 release. For larger consensus messages that don't fit in the max transaction size of 6144 bytes, a standard chunk info header can be supplied to indicate how that message should be split into smaller messages. The Mirror Node now understands this chunk information and stores it in the database. Additionally, it will return this [data](https://github.com/hashgraph/hedera-mirror-node/blob/a2f69ee1243fbbbfbc133549f9162bfc3a08f464/hedera-mirror-protobuf/src/main/proto/com/hedera/mirror/api/proto/ConsensusService.proto#L58) when subscribing to the topic via the gRPC API. The Java SDK is being updated to automatically split and reconstruct this message as appropriate.

Other changes include optimizations around end to end latency of the gRPC API. This was accomplished mainly by adding a new `NotifyingTopicListener` that uses PostgreSQL's LISTEN/NOTIFY functionality.

## [v0.14.1](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.14.1)

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: JULY 29, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: JULY 15, 2020**
{% endhint %}

This release further optimizes the ingestion rate. Initial tests indicate a 2x to 3x improvement.

## [v0.14.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.14.0)

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: JULY 29, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: JULY 15, 2020**
{% endhint %}

This release is all about performance optimizations. We reworked some of the foreign keys to improve the ingestion performance by a few thousand transactions per second. We also fixed an out of memory issue with the gRPC API and did some optimizations in that area.

Besides performance, we made some other small improvements. We now set `topicRunningHashV2AddedTimestamp` with a default value for mainnet, making it not fail on startup if a value is not provided. Containerized acceptance and performance tests were added, making it easier to test at scale.

#### Breaking Changes

We removed `hedera.mirror.grpc.listener.bufferInitial` and `hedera.mirror.grpc.listener.bufferSize` properties since we removed the shared poller's buffer.

We also renamed some tables and columns which would affect you if you directly use the database structure. We renamed `t_transactions` to `transaction`, `t_cryptotransferlists` to `crypto_transfer` and `non_fee_transfers` to `non_fee_transfer`.

## [v0.13.2](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.13.2)

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: JULY 2, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: JUNE 23, 2020**
{% endhint %}

Bug fix release to fix an out of memory issue with the gRPC API.

## [v0.13.1](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.13.1)

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: JULY 2, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: JUNE 23, 2020**
{% endhint %}

Small bug fix release to address grpc NETTY issue blocking acceptance tests

## [v0.13.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.13.0)

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: JULY 2, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: JUNE 23, 2020**
{% endhint %}

This release is a smaller release mainly focused on bug fixes with some minor enhancements. We added a new property `hedera.mirror.importer.downloader.endpointOverride` for testing. We also added `hedera.mirror.importer.downloader.gcpProjectId` to support specifying requester pays credentials with a personal account. Finally, we improved our Marketplace support getting us one closer to making it available.

## [v0.12.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.12.0)

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: MAY 29, 2020**
{% endhint %}

This feature release contains a few nice additions while fixing a few critical bugs. We made good progress on adding our application to [Google Cloud Platform Marketplace](https://console.cloud.google.com/marketplace). This should be wrapping up soon and enable a "one click to deploy" of the mirror node to Google's Cloud. Additionally, some extra fields were added to our APIs. We added `runningHashVersion` to the REST and GRPC APIs. Finally, we added `transactionHash` to the transaction REST API.

We improved the importer ingestion rate from 3400 to 5600 transactions per second in our performance test environment. There's still room for improvement and we plan on making additional performance optimizations in an upcoming release.

### Breaking Changes

We added an option to keep signature files after verification. By default, we no longer store signatures on the filesystem. If you'd like to restore the old behavior and keep the signatures, you can set `hedera.mirror.importer.downloader.record.keepSignatures=true` and `hedera.mirror.importer.downloader.balance.keepSignatures=true`.

We changed the bypass hash mismatch behavior in this release. Bypassing hash mismatch could be used in combination with other parameters to fast forward mirror node to newer data or to overcome stream resets. Previously you had to specify this via a database value in `t_application_status`. Since this data is not application state but considered more a user supplied value, we added a new property `hedera.mirror.importer.verfiyHashAfter=2020-06-05T17:16:00.384877454Z` for this purpose.  


## [v0.11.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.11.0) 

{% hint style="success" %}
**MAINNET UPGRADE COMPLETED: JUNE 10, 2020**
{% endhint %}

{% hint style="success" %}
**TESTNET UPGRADE COMPLETED: MAY 29, 2020**
{% endhint %}

This release was mainly focused on refactoring code and properties as a necessary step for future enhancements. We also continued making improvements to our Kubernetes support. To that end, we added Prometheus REST metrics, Helm tests and Mirror Node can now run in GKE.

We added a new parameter to all of the topic related REST APIs to return a topic message in plaintext instead of binary. Messages submitted to HAPI are submitted as binary and stored in the Mirror Node that way as well. If you know the messages are actually strings encoded in UTF-8, then you can set `encoding=utf-8`and the REST API will make a best effort conversion to string. By default or if you pass a query parameter of `encoding=base64`, it will return the message as base64 encoded binary.

**Breaking Changes**

Please note when upgrading that we made major breaking changes to the naming of our configuration properties. We've renamed all `hedera.mirror.api` properties to `hedera.mirror.rest`. We also renamed the properties `apiUsername` to `restUsername` and `apiPassword` to `restPassword` to reflect that as well. Any properties that were used by the importer module were renamed to be nested under `hedera.mirror.importer`. We apologize for any inconvenience.

We've removed the `hedera.mirror.addressBookPath` property in favor of a `hedera.mirror.importer.initialAddressBook` property. The former was overloaded to be both the initial bootstrap address book and the live address book being updated by file transactions for `0.0.102`. The live address book is now hardcoded to `${hedera.mirror.importer.dataPath}/addressbook.bin` and cannot be changed.

The REST API to retrieve a topic message by its consensus timestamp now supports both a plural \(`/topics/messages/:consensusTimestamp`\) and singular \(`/topic/message/:consensusTimestamp`\) URI path. The singular format is deprecated and will be going away in the near future, so please update to the plural format soon.

We removed the singular form of a few alpha topic REST APIs. The `/topic/:id/message` API was removed in favor of the plural form `/topics/:id/messages`. Similarly, the `/topic/:id/message/:sequencenumber`API was removed in favor of its plural form `/topics/:id/messages/:sequencenumber`. Please update accordingly.  
  


## [v0.10.1](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.10.1)

Small bug fix release to address a REST API packaging issue.

## [v0.10.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.10.0)

In preparation for Hedera Node release 0.5.0, we're releasing v0.10.0 to support the latest version of [HAPI](https://docs.hedera.com/guides/docs/hedera-api). The changes include renaming Claims to LiveHash and new response codes. One important HAPI change is the addition of a `topicRunningHashVersion` to the transaction record. This change was necessary as the way the topic running hash is changing with the release of 0.5.0. As a result, the Hedera Mirror Node added this new field to its database and a migration is ran to populate it with either the new or old version depending upon the release date of 0.5.0.

Unfortunately, this necessitated adding a required field `hedera.mirror.topicRunningHashV2AddedTimestamp` to control this behavior and will fail on startup if this is not populated. This is just a temporary measure. Once Hedera Node 0.5.0 is released to testnet and mainnet we will update this so it's automatically populated with the known date.

Other changes include adding Google PubSub support to publish JSON representing the `Transaction` and `TransactionRecord` protobuf to a message queue for external consumption. We've also added REST API metrics and added Traefik as an API gateway for our helm chart.

#### Breaking changes

We've had to remove our event stream support. This area of the code was never enabled and was untested and was incurring technical debt without providing any benefit. If it becomes necessary in the future, we can re-add it within our newly refactored framework.

The new `/api/v1/topics/:id` alpha REST API that was added in 0.9 has been changed to `/api/v1/topics/:id/messages`. This change was made to align the API with the other topic message APIs as it refers to the messages entity and not the topic entity.

## [v0.9.1](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.9.1)

Small bug fix release to address not being able to handle address book updates that span multiple transactions.

## [v0.9.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.9.0)

This release contains another new REST API for our [consensus service](https://www.hedera.com/consensus-service/). You can now retrieve all topic messages in a particular topic, with additional filtering by sequence number and consensus timestamp. Here's an example:

`GET /api/v1/topic/7?sequencenumber=gt:2&timestamp=lte:1234567890.000000006&limit=2`

```text
{
  "messages": [
    {
      "consensus_timestamp": "1234567890.000000003",
      "topic_id": "0.0.7",
      "message": "bWVzc2FnZQ==",
      "running_hash": "cnVubmluZ19oYXNo",
      "sequence_number": 3
    },
    {
      "consensus_timestamp": "1234567890.000000004",
      "topic_id": "0.0.7",
      "message": "bWVzc2FnZQ==",
      "running_hash": "cnVubmluZ19oYXNo",
      "sequence_number": 4
    }
  ],
  "links": {
     "next": "/api/v1/topic/7?sequencenumber=gt:2&timestamp=lte:1234567890.000000006&timestamp=gt:1234567890.000000004&limit=2"
  }
}
```

The other big feature of this release is [Kubernetes](https://kubernetes.io/) support. We've create a [Helm](https://helm.sh/) chart that can be used to deploy a highly available Mirror Node with a single command. This feature is still under heavy development as we work towards converting our current deployments to this new approach.

## [v0.8.1](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.8.1)

Small bug fix release to fix a packaging issue.

## [v0.8.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.8.0)

Mirror node v0.8.0 is here! We're made great strides in making the mirror node easier to run and manage. In particular, we added support for [requester pays](https://docs.aws.amazon.com/AmazonS3/latest/dev/RequesterPaysBuckets.html) buckets. This will allow anyone to run a mirror node as long as they are willing to pay for the cost to retrieve the data. Currently only Hedera and a few partners have access to the bucket, so enabling this will open up that data to our community. We are still working on a migration of the buckets to this model, so stay tuned.

We also added two new experimental REST APIs to retrieve HCS data. Firstly, we added `/api/v1/topic/message/${consensusTimestamp}` to retrieve a topic message by its consensus timestamp. Secondly, we added `/api/v1/topic/${topic}/message/${seqNum}` to retrieve a particular topic message by its sequence number from a topic. These APIs are considered alpha and may changed or be removed in the future. We also dramatically increased test coverage for the REST APIs and squashed some bugs in the process.

For our GRPC API, we had to switch from R2DBC to Hibernate to reach the scale and stability that we needed. In doing so, we can now support a lot more concurrent subscribers at a higher throughput. It should also finally put to rest any stability concerns with the GRPC component.

There are a few breaking changes that we had to make. We now no longer write and store record or balance files to the filesystem after they are inserted into the database. If you still need these files, you can set `hedera.mirror.parser.balance.keepFiles` and `hedera.mirror.parser.record.keepFiles` to true.

Also, we moved the persist properties to be grouped under a new path. That is we moved options like `hedera.mirror.parser.record.persistTransactionBytes` to `hedera.mirror.parser.record.persist.transactionBytes`. Please update your local configuration accordingly.

## [v0.7.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.7.0)

0.7.0 focuses on refactoring the record file parsing to decouple the parsing from the persisting of data. This refactoring is laying the groundwork for additional performance improvements and allowing additional downstream components to register for notification of the transactions.



## [v0.6.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.6.0)

* Release focused on stability and performance improvements. 
* End to end test coverage. 

This release was mainly focused on enhancing the stability and performance of the mirror node. We improved the transaction ingestion speed from 600 to about 4000 transactions per second. At the same time, we greatly improved the resiliency and performance of the GRPC module. We also added acceptance tests to test out HCS end to end.

**Breaking Change**

Please note that one potentially breaking change in this release is to reject subscriptions to topics that don't exist. This avoids the server having to poll repeatedly until it is created and taking up resources for a topic that may never exist. It is expected that clients or the [SDK](https://github.com/hashgraph/hedera-sdk-java/issues/367) will poll periodically after creating a topic until that topic makes its way to the mirror node. This functionality is hidden behind a feature flag but will slowly be rolled out over the next month.

## v0.5.3

* Now supports all HCS functionality including a streaming gRPC API for message topic subscription. 
* Changed how the mirror node verifies mainnet consensus. Mirror node now waits for at least third of node signatures rather than greater than two thirds to verify consensus.
*  Added new mainnet nodes to the mirror node address book.
* Access still restricted to a white listed set of IP addresses. Request access [here](https://learn.hedera.com/l/576593/2020-01-13/7z5jb).
* Please see the Mirror Node releases page for the full list of changes [here](https://github.com/hashgraph/hedera-mirror-node/releases).
* We occasionally may encounter a situation where an additional 15-20 second delay in message round trip time is experienced and subscriber connections are dropped. No messages are lost, and the consensus time is not affected. Clients are encouraged to reconnect. This issue will be fixed in a subsequent release of the Hedera mirror node. Some third-party mirror nodes should not be affected by this issue. We also don't expect it to impact the exchanges using the REST end point for the mirror node. 

