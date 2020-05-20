---
title: Fees (Beta)
excerpt: Network fees for the Hedera mainnet and testnet
---

# Fees \(Beta\)

The Hedera testnet fees tables found below offers a low-end estimate of transaction and query fees for all network services. The tables below contain USD, HBAR, and Tinybar \(tℏ\) values per each API call. All operation fees on the Hedera testnet are paid in test HBAR, which is freely available and only useful for development purposes.

Fee estimates are based on assumptions about the details of a specific API call. For instance, the fee for an HBAR cryptocurrency transfer \(CryptoTransfer\) assumes a single signature on the transaction and the fee for storing a file assumes a 48 byte sized file stored for 30 days. Transactions which exceed these base assumptions will be more expensive; we recommend increasing your maximum allowable fee to accommodate for additional complexity. Hedera is in the process of creating tools which will make it simple to calculate the cost of running your application on the mainnet.

### Mainnet Fees

Mainnet transaction and query fees can be estimated using the [Hedera Fee Estimator](https://www.hedera.com/fees). The Fee Estimator allows you to determine fees \(in both USD and HBAR, using the current exchange rate live on the mainnet\) for individual transactions & queries based on their characteristics, as well as projected costs based on expected volume for those transactions. The estimations may not be 100% accurate and the underlying prices are subject to change without prior notice.

## Hbar Denominations and Abbreviations

| Denominations | Abbreviations | Amount of HBAR Cryptocurrency |
| :--- | :--- | :--- |
| gigabar | 1 Gℏ | = 1,000,000,000 ℏ |
| megabar | 1 Mℏ | = 1,000,000 ℏ |
| kilobar | 1 Kℏ | = 1,000 ℏ |
| hbar | 1 ℏ | = 1 ℏ |
| millibar | 1,000 mℏ | = 1 ℏ |
| microbar | 1,000,000 μℏ | = 1 ℏ |
| tinybar | 100,000,000 tℏ | = 1 ℏ |

## Transaction and Query Fees

All fees are subject to change.

### Cryptocurrency Accounts

| Operations | USD \($\) |
| :--- | :--- |
| CryptoCreate | $0.01 |
| CryptoAccountAutoRenew | $0.00022 |
| CryptoUpdate | $0.00022 |
| CryptoTransfer | $0.0001 |
| CryptoDelete | $0.005 |
| CryptoAddClaim | $0.1 |
| CryptoDeleteClaim | $0.005 |
| CryptoGetClaim | $0.0001 |
| CryptoGetAccountRecords | $0.0001 |
| CryptoGetAccountBalance | $0.00 |
| CryptoGetInfo | $0.0001 |
| CryptoGetStakers | $0.0001 |

### Consensus Service

| Operations | USD \($\) |
| :--- | :--- |
| ConsensusCreateTopic | $0.01 |
| ConsensusUpdateTopic | $0.00022 |
| ConsensusDeleteTopic | $0.005 |
| ConsensusSubmitMessage | $0.0001 |
| ConsensusGetInfo | $0.0001 |

### File Service

| Operations | USD \($\) |
| :--- | :--- |
| FileCreate | $0.05 |
| FileUpdate | $0.0005 |
| FileDelete | $0.007 |
| FileAppend | $0.05 |
| FileGetContents | $0.0001 |
| FileGetInfo | $0.0001 |



### Smart Contract

| Operations | USD \($\) |
| :--- | :--- |
| ContractCreate | $1.0 |
| ContractUpdated | $0.026 |
| ContractDelete | $0.007 |
| ContractCall | $0.05 |
| ContractCallLocal | $0.001 |
| ContractGetByteCode | $0.05 |
| GetBySolidityID | $0.0001 |
| ContractGetInfo | $0.0001 |
| ContractGetRecords | $0.0001 |
| ContractAutoRenew | $0.026 |

### Miscellaneous

| Operations | USD \($\) |
| :--- | :--- |
| GetVersion | $0.001 |
| GetByKey | $0.0001 |
| TransactionGetReceipt | $0.0000 |
| TransactionGetRecord | $0.0001 |

