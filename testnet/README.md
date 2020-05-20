---
description: Join a Hedera Testnet
---

# Testnet

## Overview

Hedera testnets provides developers with access to a free testing environment for Hedera network services. Testnets simulate the exact same devlopment environment as you would expect for mainnet. This includes transaction fees, throttles, available services, etc. Once your application has been built and tested in this test enviornment you can expect to migrate your decentralized application to mainnet without any changes. Testnets are likely to change and data may be deleted

{% hint style="warning" %}
**Limited Support**  
Transactions are currently throttled for mainnet and testnet. You will receive a "BUSY" response if the number of transactions submitted to the network exceeds the threshold value.
{% endhint %}

| Network Service | Availability  |
| :--- | :--- |
| Cryptocurrency | Limited |
| Smart Contracts | Limited |
| File Service | Limited |
| Consensus Service | Limited  |

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
        <p>MessageSubmit transactions: 1,000 tps
          <br />createTopic: 5tps</p>
        <p>getTopicInfo/updateTopic/deleteTopic: 100 tps</p>
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
</table>