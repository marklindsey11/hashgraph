---
description: Join Hedera mainnet
---

# Mainnet

## Overview

The Hedera mainnet, short for main network, is where applications are run in production with real transactions and associated costs. is the public network used to deploy decentralized applications for use in production. Transactions can be submitted to the Hedera mainnet by any application user and are timestamped and ordered automatically by the distributed ledger. Any data associated with Hedera services and stored on ledger can be accessed by any Hedera account. For each transaction, small **transaction fees** will be charged \(in tinybars\). You can find more information about transactions fees [here](https://www.hedera.com/fees). If you are looking to test your application or just to experiment, please check out Testnet Access, which allows you to prototype and practice in a real Hedera network without incurring those fees.

{% hint style="warning" %}
**Limited Support**   
Transactions are currently throttled for mainnet and testnet. You will receive a "BUSY" response if the number of transactions submitted to the network exceeds the threshold value.
{% endhint %}

| Network Service | Availability  |
| :--- | :--- |
| Cryptocurrency | Limited |
| Smart Contracts | Limited |
| File Service | Limited |
| Consensus Service | Limited |

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
      <td style="text-align:left">
        <p>CryptoTransfer transactions: 10,000 tps</p>
        <p>All other cryptocurrency transactions<b>: </b>13 tps</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Consensus Transactions</td>
      <td style="text-align:left">
        <p>MessageSubmit transactions: 1,000 tps</p>
        <p>getTopicInfo/createTopic/updateTopic/deleteTopic: 100 tps</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">File Transactions</td>
      <td style="text-align:left">All transaction types: 13 tps</td>
    </tr>
    <tr>
      <td style="text-align:left">Smart Contract Transactions</td>
      <td style="text-align:left">All transaction types: 13 tps</td>
    </tr>
    <tr>
      <td style="text-align:left">Queries</td>
      <td style="text-align:left">6,500 tps</td>
    </tr>
    <tr>
      <td style="text-align:left">Receipts</td>
      <td style="text-align:left">unlimited (no throttle)</td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
**Hedera Consensus Service Mainnet Mirror Node Access**  
To gain access to the Hedera managed mirror node for mainnet, please complete this [form](https://learn.hedera.com/hcs-mirror-api-mainnet).
{% endhint %}

