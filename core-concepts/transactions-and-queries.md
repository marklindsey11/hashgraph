---
description: An overview of Hedera API transactions and queries
---

# Transactions and Queries

## Transactions

**Transactions** are requests sent by a client to a node with the expectation that they are submitted to the network for processing into consensus order and subsequent application to state. Each transaction \(e.g. `TokenCreateTransaction()`\) has an associated transaction fee that compensates the Hedera network for that processing and subsequent maintenance in consensus state.

**Transaction ID**

Each transaction has a unique transaction ID. The transaction ID is used for the following:

* Obtaining receipts, records, state proofs
* Internally by the network for detecting when duplicate transactions are submitted

The transaction ID is composed by using the transaction valid start time and the account ID of the account that paid for the transaction. The transaction valid start is the timestamp in seconds.nanoseconds format. A transaction ID looks something like `0.0.9401@1598924675.82525000`where `0.0.9401` is the transaction fee payer account ID and `1598924675.82525000` is the timestamp in seconds.nanoseconds.

A **transaction** generally includes the following:

* **Node Account**: the account of the node the transaction is being sent to \(e.g. `0.0.3`\)
* **Transaction ID**: the identifier for a transaction has two components, the account ID of the paying account plus the transaction’s valid start time
* **Transaction Fee**: the maximum fee the paying account is willing to pay for the transaction
* **Valid Duration**: the number of seconds that the client wishes the transaction to be deemed valid for, starting at the transaction valid start time
* **Memo**:  a string of text up to 100 bytes of data \(optional\)
* **Transaction**: type of request, for instance an HBAR transfer or a smart contract call
* **Signatures**: at minimum, the paying account will sign the transaction as authorization. Other signatures may be present as well.

The lifecycle of a transaction in the Hedera ecosystem begins when a client creates a transaction. Once the transaction is created it is cryptographically signed at minimum by the account paying for the fees associated with the transaction. Additional signatures may be required depending on the properties set for the account, topic, or token. The client is able to stipulate the maximum fee it is willing to pay for the processing of the transaction and, for a smart contract operation, the maximum amount of gas. Once the required signatures are applied to the transaction the client then submits the transaction to any node on the Hedera network.

The receiving node validates \(for instance, confirms the paying account has sufficient balance to pay the fee\) the transaction and, if validation is successful, submits the transaction to the Hedera network for consensus by adding the transaction to an event and gossiping that event to another node. Quickly, that event flows out to all the other nodes. The network receives this transaction exponentially fast via the [gossip about gossip protocol](https://docs.hedera.com/docs/gossip-about-gossip). The consensus timestamp for an event \(and so the transactions within\) is calculated by each node independently calculating the median of the times that the nodes of the network received that event. You may find more information on how the consensus timestamp is calculated [here](https://docs.hedera.com/docs/hashgraph-overview#section-fair-timestamps). The hashgraph algorithm delivers finality of consensus. Once assigned a consensus timestamp the transaction is then applied to the consensus state in the order determined by each transaction’s consensus timestamp. At that point the fees for the transaction are also processed. In this manner, every node in the network maintains a consensus state because they all apply the same transactions in the same order. Each node also creates and temporarily stores receipts/records in support of the client subsequently querying for the status of a transaction.

For more information about Hedera transaction fees, please visit Hedera API fees [overview](https://www.hedera.com/fees).

## Queries

**Queries** are processed only by the single node to which they are sent. Clients send queries to retrieve some aspect of the current consensus state like the balance of an account. Certain queries are free but generally queries are subject to fees. The full list of queries can be found [here](../docs/sdks/queries.md).

A query includes a header that includes a distinct HBAR transfer transaction that will serve as the means by which the client pays the node the appropriate fee. The node processing the query will submit that payment transaction to the network for processing into consensus statement in order to receive its fee.

A client can determine the appropriate fee for a query by first asking a node for the cost and not the actual data. Such a COST\_ANSWER query is free to the client.

For more information about query fees, please visit Hedera API fees [overview](https://www.hedera.com/fees).

### Recall:

{% hint style="info" %}
Recall

Hedera does not have **miners** or a special group of nodes that are responsible for adding transactions to the ledger like alternative distributed ledger solutions. The influence of each node to the determination of the consensus timestamp for an event is proportional to its stake in HBARs.
{% endhint %}

![](../.gitbook/assets/transaction-flow.png)

Once a transaction has been submitted to the network, clients may seek confirmation it was successfully processed. There are multiple confirmation methods - varying in the level of information provided, the duration for which the confirmation is available, the degree of trust, and the corresponding cost.

![](../.gitbook/assets/query-confirmation.png)

## Confirmations

* **Receipts:** Receipts provide minimal information - simply whether or not the transaction was successfully processed into consensus state. Receipts are generated by default and are persisted for 3 minutes. Receipts are free.
* **Records:** Records provide greater detail about the transaction than do receipts — such as the consensus timestamp it received or the results of a smart contract function call. Records are generated by default but are persisted for 3 minutes. Longer lived records \(24 hours\) are created if a crypto transfer transaction surpasses a threshold defined on the accounts involved.
* **State proofs \(coming soon\):** When querying for a record, a client can optionally indicate that it desires the network to return a state proof in addition to the record. A state proof documents network consensus on the contents of that record in the consensus state — this collective assertion includes signatures of most of the network nodes. Because state proofs are cryptographically signed by a super majority of the network, they are secure and potentially admissible in a court of law.

{% hint style="info" %}
An early version of a state proof, state proof alpha, is now available. Please check out the Mirror Node REST API section to get started.
{% endhint %}

{% page-ref page="../docs/mirror-node-api/cryptocurrency-api.md" %}

For a more detailed review of confirmation methods check out this [blog post](https://www.hedera.com/blog/transaction-confirmation-methods-in-hedera).

