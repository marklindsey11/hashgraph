---
description: Join Hedera mainnet
---

# Mainnet

## Overview

The Hedera mainnet, short for main network, is where applications are run in production with real transactions and associated costs. Transactions can be submitted to the Hedera mainnet by any application user and are timestamped and ordered automatically by the distributed ledger. Any data associated with Hedera services and stored on ledger can be accessed by any Hedera account. For each transaction, small **transaction fees** will be charged \(in tinybars\). You can find more information about transactions fees [here](https://www.hedera.com/fees). If you are looking to test your application or just to experiment, please check out [Testnet Access,](../testnet/testnet-access.md) which allows you to prototype and practice in a real Hedera network without incurring those fees.

{% hint style="warning" %}
**Limited Support**   
Transactions are currently throttled for mainnet and testnet. You will receive a "BUSY" response if the number of transactions submitted to the network exceeds the threshold value.
{% endhint %}

| Network Service | Availability  |
| :--- | :--- |
| Cryptocurrency | Limited |
| Smart Contract Service | Limited |
| File Service | Limited |
| Consensus Service | Limited |
| Token Service | Not available |

#### Network Throttles

<table>
  <thead>
    <tr>
      <th style="text-align:left">Network Request Type</th>
      <th style="text-align:left">Throttle (tps)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Cryptocurrency Transactions</td>
      <td style="text-align:left">8,000 tps (excludes CryptoCreate)</td>
    </tr>
    <tr>
      <td style="text-align:left">CryptoCreate Transactions</td>
      <td style="text-align:left">13 tps</td>
    </tr>
    <tr>
      <td style="text-align:left">Consensus Transactions</td>
      <td style="text-align:left">
        <p>3,000 tps</p>
        <p>CreateTopic: 5 tps</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">File Transactions</td>
      <td style="text-align:left">13 tps</td>
    </tr>
    <tr>
      <td style="text-align:left">Smart Contract Transactions</td>
      <td style="text-align:left">13 tps</td>
    </tr>
    <tr>
      <td style="text-align:left">Queries</td>
      <td style="text-align:left">8,000 tps</td>
    </tr>
    <tr>
      <td style="text-align:left">Receipts</td>
      <td style="text-align:left">unlimited (no throttle)</td>
    </tr>
  </tbody>
</table>

