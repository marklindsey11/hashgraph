# Smart Contracts

## Hyperleder Besu

The EthereumJ virtual machine was replaced with the [Hyperledger Besu](https://besu.hyperledger.org/en/stable/) virtual machine in the Hedera Services release [0.19](https://github.com/hashgraph/hedera-services/releases/tag/v0.19.4). This migration enables Hedera to maintain parity with Ethereum Mainnet evolutions such as the EVM container formats and new opcodes and precompiled contracts. The Besu integration is configured to use the “London” hard fork of Ethereum Mainnet. The smart cont

### London Hard Fork

The smart contract platform will be upgraded to support the EVM visible changes for the “London” hard fork. This includes changes introduced in the “Istanbul” and “Berlin” hard forks. Changes relating to block production, data serialization, and the fee market will not be implemented because they are not relevant to Hedera’s architecture.

Starting in the Hedera Services 0.22 release, we will start charging for the **Intrinsic Gas Cost** (21,000 Gas) per transaction and for the input data (16 gas per non-zero byte, 4 gas per zero byte). The intrinsic gas cost is a constant that is charged before any code is executed.

#### Opcode and Solidity variable mapping to Hedera

| Solidity                                  | Hedera                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `address`                                 | The address is a mapping of shard.realm.number into a 20 byte Solidity address.                                                                                                                                                                                                                                                                                                                                |
| `block.basefee`                           | The BASEFEE opcode will return zero. Hedera does not use the Fee Market mechanism this is designed to support                                                                                                                                                                                                                                                                                                  |
| `block.chainid`                           | The CHAINIDopcode will return 290(hex 0x0127) for mainnet, 291( hex 0x0128) for testnet, and 292( hex 0x0129) for previewnet                                                                                                                                                                                                                                                                                   |
| `block.coinbase`                          | The COINBASEoperation will return the funding account (Hedera transaction fee collecting account 0.0.98).                                                                                                                                                                                                                                                                                                      |
| `block.number`                            | The index of the record file (not recommended use block.timestamp)                                                                                                                                                                                                                                                                                                                                             |
| `block.timestamp`                         | The transaction consensus timestamp                                                                                                                                                                                                                                                                                                                                                                            |
| `block.difficulty`                        | Always zero                                                                                                                                                                                                                                                                                                                                                                                                    |
| `block.gaslimit`                          | The GASLIMIT operation will return the gasLimitof the transaction. The transaction gasLimit will be the lowest of the gas limit requested in the transaction or a global upper gas limit configured for all smart contracts.                                                                                                                                                                                   |
| `msg.sender`                              | The address of the solidity contract ID or account ID that called this contract.  For the root level or for delegate chains that go to root it is the account ID paying for the transaction.                                                                                                                                                                                                                   |
| `msg.value`                               | The value associated to the transaction associated in tinybar                                                                                                                                                                                                                                                                                                                                                  |
| `tx.origin`                               | The account ID paying for the transaction, regardless of depth.                                                                                                                                                                                                                                                                                                                                                |
| `tx.gasprice`                             | Fixed (varies with the global fee schedule and exchange rate)                                                                                                                                                                                                                                                                                                                                                  |
| `selfdestruct(address payable recipient)` | Address will not be reusable due to Hedera’s account numbering policies                                                                                                                                                                                                                                                                                                                                        |
| `<address>.code`                          | Precompile contract addresses will report no code, including HTS System contract                                                                                                                                                                                                                                                                                                                               |
| `<address>.codehash`                      | Precompile contract addresses will report the empty code hash                                                                                                                                                                                                                                                                                                                                                  |
| `SELFBALANCE`                             | This opcode will operate as expected with no change from Ethereum Mainnet.                                                                                                                                                                                                                                                                                                                                     |
| `CREATE2`                                 | The CREATE2operation (including new Contract{salt:value}()}() style contract creations) is currently not supported and returns an illegal opcode failure. The implementation in hedera of CREATEand CREATE2are identical, and this creates a usability problem with contracts that expect CREATE2to operate in a specified manner. This stems from the differences in Hedera’s and Ethereum’s account mapping. |

### Gas Schedule

The Hedera Smart Contract Service will use the Gas Schedule from the "London" hard fork. Notable changes include warm/cold account access and refund reductions.

#### **Warm and Cold Account and Slot Access**

Berlin introduced the notion of warm and cold accounts and storage slots. The first access to an account or storage slot in a transaction will need to pay the "cold" costs and all subsequent calls will pay the lower "warm" access costs. [EIP-2929](https://eips.ethereum.org/EIPS/eip-2929) contains the full details of the new cost scheduling.

Hedera does not at this time allow for "pre-warming" addresses and storage slots as part of the transaction as seen in [EIP-2930](https://eips.ethereum.org/EIPS/eip-2929). Future HIPs may support this scheme.

#### **Gas Refund Reductions and Eliminations**

In the London gas schedule, the amount of gas that can be returned from storage access usage patterns has been significantly reduced. Account refunds from `SELFDESTRUCT` have been completely removed.

[Hedera vs. London Gas Costs](https://www.notion.so/c6585e88dda64db880773537a7e5769c)

The terms 'warm' and 'cold' in the above table correspond with whether the account or storage slot has been read or written to within the current smart contract transaction, even if within a child call frame.

'CALL _et al._' includes with limitation CALL, CALLCODE, DELEGATECALL, and STATICCALL

Reference [HIP-206](https://hips.hedera.com/hip/hip-26)

Starting in 0.22 we will start charging for the **Intrinsic Gas Cost** (21,000 Gas per transaction) per transaction and for the input data (16 gas per non-zero byte, 4 gas per zero byte). The intrinsic gas cost is a constant that is charged before any code is executed. The total gas cost for a given transaction will include the intrinsic gas cost, the input data, the gas for the transaction and EVM operation cost.

**Token Burn Precompile Gas Fee from USD**

```
$0.001 USD * ( 1 GAS/ $0.0000000569 USD )*1.2 = Gas/ precompile tx
```

**Total Gas**

precompile transaction to execute

```
```

Intrinsic cost = `21,000 gas + [(16*count of non-zero bytes in functionParameters) gas + (4*count of non-zero bytes in functionParameters) gas ]`

EVM execution cost = `EVM opcode gas (opcode gas from London table) (links to tools)`

Hedera Services precompile cost = `(cost of base Hedera Service in USD * ( 1 GAS/ $0.0000000569 ))*1.2`

Total cost gas = Intrinsic cost + EVM execution cost + Hedera Services precompile cost

USD/gas conversation rate

Total cost in USD = total cost gas X $0.000\_000\_0569/1 gas

Paid in hbar

update Hedera calculator

**For non-precompiles gas cost in USD**

Use London gas table and multiply by the USD/Gas conversion ($0.000\_000\_0569/1 Gas)

Example:

EXTCODESIZE opcode - gas cost 2600

Gas and USD price would be

```
2600 Gas*($0.000_000_0569/1 Gas)
```
