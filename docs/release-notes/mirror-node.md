# Mirror Node

| Network | Version |
| :--- | :--- |
| **Mainnet** | Mirror Node v0.9.1 |
| **Testnet** | Mirror Node v0.10.1 |
| **Previewnet** | Coming soon... |

## Upcoming Releases

## [v0.11.0](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.11.0)

This release was mainly focused on refactoring code and properties as a necessary step for future enhancements. We also continued making improvements to our Kubernetes support. To that end, we added Prometheus REST metrics, Helm tests and Mirror Node can now run in GKE.

We added a new parameter to all of the topic related REST APIs to return a topic message in plaintext instead of binary. Messages submitted to HAPI are submitted as binary and stored in the Mirror Node that way as well. If you know the messages are actually strings encoded in UTF-8, then you can set `encoding=utf-8`and the REST API will make a best effort conversion to string. By default or if you pass a query parameter of `encoding=base64`, it will return the message as base64 encoded binary.

**Breaking Changes**

Please note when upgrading that we made major breaking changes to the naming of our configuration properties. We've renamed all `hedera.mirror.api` properties to `hedera.mirror.rest`. We also renamed the properties `apiUsername` to `restUsername` and `apiPassword` to `restPassword` to reflect that as well. Any properties that were used by the importer module were renamed to be nested under `hedera.mirror.importer`. We apologize for any inconvenience.

We've removed the `hedera.mirror.addressBookPath` property in favor of a `hedera.mirror.importer.initialAddressBook` property. The former was overloaded to be both the initial bootstrap address book and the live address book being updated by file transactions for `0.0.102`. The live address book is now hardcoded to `${hedera.mirror.importer.dataPath}/addressbook.bin` and cannot be changed.

The REST API to retrieve a topic message by its consensus timestamp now supports both a plural \(`/topics/messages/:consensusTimestamp`\) and singular \(`/topic/message/:consensusTimestamp`\) URI path. The singular format is deprecated and will be going away in the near future, so please update to the plural format soon.

We removed the singular form of a few alpha topic REST APIs. The `/topic/:id/message` API was removed in favor of the plural form `/topics/:id/messages`. Similarly, the `/topic/:id/message/:sequencenumber`API was removed in favor of its plural form `/topics/:id/messages/:sequencenumber`. Please update accordingly.  
  


## Latest Releases

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

