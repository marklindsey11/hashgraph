# Hedera Service Solidity Libraries

## Hedera Token Service&#x20;

Hedera Token Service integration allows you to write token transactions natively in Solidity smart contracts. There are three **Solidity source files** available to developers.

* [HederaTokenService.sol](https://github.com/hashgraph/hedera-smart-contracts/blob/main/hts-precompile/HederaTokenService.sol)
* [HederaResponseCodes.sol](https://github.com/hashgraph/hedera-smart-contracts/blob/main/hts-precompile/HederaResponseCodes.sol)
* [IHederaTokenService.sol ](https://github.com/hashgraph/hedera-smart-contracts/blob/main/hts-precompile/IHederaTokenService.sol)

The Hedera Token Service Solidity file provides the transactions to interact with tokens created on Hedera. The Hedera Response Codes contract provides the response codes associated with network errors. The IHedera Token Service is a supporting library for the Hedera Token Service Solidity file. You can grab these libraries [here](https://github.com/hashgraph/hedera-smart-contracts/tree/main/hts-precompile) to add to your project and import them to your Solidity contract. Please see the example file below.

{% code title="ContractExample.sol" %}
```solidity
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;

import "./HederaTokenService.sol";
import "./HederaResponseCodes.sol";

contract contractExample is HederaTokenService {
...
int response = HederaTokenService.transferToken(tokenAddress, msg.sender, address(this), amount);
...
}
```
{% endcode %}

{% hint style="info" %}
**Note:** Although the [IHederaTokenService.sol ](https://github.com/hashgraph/hedera-smart-contracts/blob/main/hts-precompile/IHederaTokenService.sol)file is not imported in the contract, you will need it in your project directory for the supporting libraries to reference.
{% endhint %}

### Transfer Tokens

### <mark style="color:purple;">`cryptoTransfer(tokenTransfers)`</mark>

A transaction that transfers the provided list of tokens.

ABI Version: 2

| **Param**        | **Type**                                                                                                                                                     | **Description**             |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------- |
| `tokenTransfers` | [IHederaTokenService.TokenTransferList\[\] ](https://github.com/hashgraph/hedera-smart-contracts/blob/main/hts-precompile/IHederaTokenService.sol#L39)memory | The list of token transfers |

### <mark style="color:purple;">`transferToken(token, sender, receiver, amount)`</mark>

Transfers tokens where the calling account/contract is implicitly the first entry in the token transfer list, <mark style="color:purple;"></mark> where the amount is the value needed to zero balance the transfers. The account address sending the token is required to sign the transaction.

ABI Version: 1

| **Param**  | **Type**                                                               | **Description**                                                                                                                     |
| ---------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `token`    | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address) | The token ID to transfer to/from. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address.         |
| `sender`   | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address) | The address sending the token. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address.            |
| `receiver` | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address) | The address of the receiver of the token. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address. |
| `amount`   | int64                                                                  | Non-negative value of the token to send. A negative value will result in a failure.                                                 |

### <mark style="color:purple;">`transferTokens(token, accountIds, amount)`</mark>

Initiates a fungible token transfer. Not applicable to non-fungible tokens.

ABI Version: 1

| **Param**    | **Type**                                                                                                   | **Description**                                                                                                                     |
| ------------ | ---------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `token`      | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address)                                     | The token ID to transfer. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address.                 |
| `accountIds` | [address](https://docs.soliditylang.org/en/v0.6.2/types.html?highlight=address%20%5B%5D#address)\[] memory | Hedera accounts to do a transfer to/from. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address. |
| `amounts`    | int64\[] memory                                                                                            | Non-negative value to send. A negative value will result in a failure.                                                              |

### <mark style="color:purple;">`transferNFT(token, sender, receiver, serialNum)`</mark>

Transfers tokens where the calling account/contract is implicitly the first entry in the token transfer list, <mark style="color:purple;"></mark> where the amount is the value needed to zero balance the transfers. The address sending the token is required to sign the transaction.

ABI Version: 1

| **Param**   | **Type**                                                               | **Description**                                                                                                                     |
| ----------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `token`     | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address) | The token to transfer to/from.                                                                                                      |
| `sender`    | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address) | The address sending the token. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address.            |
| `receiver`  | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address) | The address of the receiver of the token. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address. |
| `serialNum` | int64                                                                  | The serial number of the NFT to transfer.                                                                                           |

### <mark style="color:purple;">`transferNFTs(token, sender, receiver, serialNumber)`</mark>

Initiates a non-fungible token transfer

ABI Version: 1

| **Param**      | **Type**                                                                         | **Description**                                                                                                                     |
| -------------- | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `token`        | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address)           | The ID of the token to transfer. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address.          |
| `sender`       | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address)\[] memory | The address sending the token. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address.            |
| `receiver`     | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address)\[] memory | The address of the receiver of the token. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address. |
| `serialNumber` | int64                                                                            | The serial number of the nft sent by the same index at sender.                                                                      |

### Mint Tokens

### <mark style="color:purple;">`mintToken(token, amount, metadata)`</mark>

Mints an amount of the token to the defined treasury account.&#x20;

ABI Version: 2

| **Param**  | **Type**                                                               | **Description**                                                                                                                                                                                                                       |
| ---------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `token`    | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address) | The Hedera token to mint. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address.                                                                                                                   |
| `amount`   | <p><br>uint64</p>                                                      | <p>Applicable to FUNGIBLE TOKENS ONLY. <br><br>The amount to mint to the Treasury Account. Amount must be a positive non-zero number represented in the lowest denomination of the token. The new supply must be lower than 2^63.</p> |
| `metadata` | bytes\[] memory                                                        | <p>Applicable to NON-FUNGIBLE TOKENS ONLY. <br>Maximum allowed size of each metadata is 100 bytes</p>                                                                                                                                 |

### Burn Tokens

### <mark style="color:purple;">`burnToken(token, amount, serialNumbers)`</mark>

Burns an amount of the token from the defined treasury account<mark style="color:purple;">.</mark>

ABI Version: 2

| **Param**       | **Type**                                                               | **Description**                                                                                                                                                                                                                                                                                 |
| --------------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `token`         | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address) | The token to burn. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address.                                                                                                                                                                                    |
| `amount`        | uint64                                                                 | <p>Applicable to FUNGIBLE TOKENS ONLY. <br><br>The amount to burn from the Treasury Account. <mark style="color:purple;"></mark> Amount must be a positive non-zero number, not bigger than the token balance of the treasury account (0; balance], represented in the lowest denomination.</p> |
| `serialNumbers` | int64\[]                                                               | <p>Applicable to NON-FUNGIBLE TOKENS ONLY.<br></p><p>The list of serial numbers to be burned.</p>                                                                                                                                                                                               |

### Associate Tokens

### <mark style="color:purple;">`associateToken(account, tokens)`</mark>

Associates the provided account with the provided tokens. Must be signed by the account that is being associated with the token.

ABI Version: 2

| **Param** | **Type**                                                                                                   | **Description**                                                                                                                                                                                                                                                                                                                     |
| --------- | ---------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `account` | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address)                                     | The account to be associated with the provided tokens. The address is a mapping of `shard.realm.number` (0.0.x) into a 20 byte Solidity address.                                                                                                                                                                                    |
| `token`   | [address](https://docs.soliditylang.org/en/v0.6.2/types.html?highlight=address%20%5B%5D#address)\[] memory | <p>The list of tokens to be associated with the provided account. </p><p><br>In the case of non-fungible tokens, once an account is associated, it can hold any number of NFTs (serial numbers) of that token type.<br><br>The address is a mapping of <code>shard.realm.number</code> (0.0.x) into a 20 byte Solidity address.</p> |

### Dissociate Tokens

### <mark style="color:purple;">`dissociateToken(account, token)`</mark>

Dissociates the provided account with the provided token. Must be signed by the provided Account's key.

ABI Version: 2

| **Param** | **Type**                                                               | **Description**                                                                                                                                                                   |
| --------- | ---------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `account` | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address) | <p>The Hedera account to be dissociated from the provided token. <br><br>The address is a mapping of <code>shard.realm.number</code> (0.0.x) into a 20 byte Solidity address.</p> |
| `token`   | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address) | <p>The token to be dissociated from the provided account.<br><br>The address is a mapping of <code>shard.realm.number</code> (0.0.x) into a 20 byte Solidity address.</p>         |

### <mark style="color:purple;">`dissociateTokens(account, tokens)`</mark>

Dissociates the provided account with the provided token. Must be signed by the account the token is being dissociated from.

ABI Version: 2

| **Param** | **Type**                                                                                                   | **Description**                                                                                                                                                                    |
| --------- | ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `account` | [address](https://docs.soliditylang.org/en/v0.8.10/types.html#address)                                     | The account to be dissociated from the provided tokens                                                                                                                             |
| `tokens`  | [address](https://docs.soliditylang.org/en/v0.6.2/types.html?highlight=address%20%5B%5D#address)\[] memory | <p>The list of tokens to be dissociated from the provided account.<br><br>The address is a mapping of <code>shard.realm.number</code> (0.0.x) into a 20 byte Solidity address.</p> |

### Gas Cost

{% content-ref url="../../../core-concepts/smart-contracts/gas-and-fees.md" %}
[gas-and-fees.md](../../../core-concepts/smart-contracts/gas-and-fees.md)
{% endcontent-ref %}

