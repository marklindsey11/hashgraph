---
description: Join a Hedera Testnet
---

# Testnets

## Overview

Hedera testnets provide developers with access to a free testing environment for Hedera network services. Testnets simulate the exact same development environment as you would expect for mainnet. This includes transaction fees, throttles, available services, etc. Once your application has been built and tested in this test environment you can expect to migrate your decentralized application to mainnet without any changes. Testnets are likely to change and data may be deleted

**Test Networks:**

| **Name**                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Test Network**         | Runs the same code as the Hedera mainnet, designed to provide a pre-production environment for developers about to move to mainnet. You can find compatible SDKs [here](../docs/sdks/#hedera-supported-sdks).                                                                                                                                                                                                                                                                |
| **Preview Test Network** | <p>Code that is under development by the Hedera team, and likely to be used in an upcoming release, designed to give developers early exposure to features coming down the pipe. Updates to the network are made frequently. There is no guarantee an SDK will readily support the up-and-coming features.</p><p><strong>Note:</strong> Updates to this network are triggered by a new release and are frequent. These updates will not be reflected on the status page.</p> |

{% hint style="warning" %}
**Limited Support**\
Transactions are currently throttled for testnets. You will receive a "BUSY" response if the number of transactions submitted to the network exceeds the threshold value.
{% endhint %}

| Network Service        | Availability |
| ---------------------- | ------------ |
| Cryptocurrency         | Limited      |
| Consensus Service      | Limited      |
| File Service           | Limited      |
| Smart Contract Service | Limited      |
| Token Service          | Limited      |

### Test Network Throttles

| Network Request Type        | Throttle (tps)                                                                                       |
| --------------------------- | ---------------------------------------------------------------------------------------------------- |
| Cryptocurrency Transactions | <p>AccountCreateTransaction: 2 tps</p><p>AccountBalanceQuery: unlimited</p><p>Other: 10,000 tps </p> |
| Consensus Transactions      | <p>TopicCreateTransaction: 5 tps</p><p>Other: 10,000 tps</p>                                         |
| Token Transactions          | <p>TokenMint (NFT): 1200 tps</p><p>TokenAssociateTransaction: 100 tps</p><p>Other: 3,000 tps</p>     |
| Schedule Transactions       | 100 tps                                                                                              |
| File Transactions           | 10 tps                                                                                               |
| Smart Contract Transactions | 350 tps                                                                                              |
| Queries                     | 10,000 tps                                                                                           |
| Receipts                    | unlimited (no throttle)                                                                              |
