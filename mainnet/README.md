---
description: Join Hedera mainnet
---

# Mainnet

## Overview

The Hedera mainnet, short for main network, is where applications are run in production with real transactions and associated costs. Transactions can be submitted to the Hedera mainnet by any application user and are timestamped and ordered automatically by the distributed ledger. Any data associated with Hedera services and stored on ledger can be accessed by any Hedera account. For each transaction, small **transaction fees** will be charged (in tinybars). You can find more information about transaction fees [here](https://www.hedera.com/fees). If you are looking to test your application or just to experiment, please check out [Testnet Access,](../testnet/testnet-access.md) which allows you to prototype and practice in a real Hedera network without incurring those fees.

{% hint style="warning" %}
**Limited Support **\
Transactions are currently throttled for mainnet. You will receive a "BUSY" response if the number of transactions submitted to the network exceeds the threshold value.
{% endhint %}

| Network Service        | Availability  |
| ---------------------- | ------------- |
| Cryptocurrency         | Limited       |
| Smart Contract Service | Limited       |
| File Service           | Limited       |
| Consensus Service      | Limited       |
| Token Service          | Limited       |

#### Network Throttles

| Network Request Type        | Throttle (tps)                                                                                             |
| --------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Cryptocurrency Transactions | <p>AccountCreateTransaction: 2 tps</p><p>Other: 6,000 tps (excludes CryptoCreate)</p>                      |
| Consensus Transactions      | <p>TopicCreateTransaction: 5 tps</p><p>TopicMessageSubmitTransaction: 8,000 tps</p><p>Other: 3,000 tps</p> |
| Token Transactions          | <p>TokenCreateTransaction: 100 tps</p><p>TokenAssociateTransaction: 100 tps</p><p>Other: 3,000 tps</p>     |
| File Transactions           | 13 tps                                                                                                     |
| Smart Contract Transactions | 13 tps                                                                                                     |
| Queries                     | 8,000 tps                                                                                                  |
| Receipts                    | unlimited (no throttle)                                                                                    |
