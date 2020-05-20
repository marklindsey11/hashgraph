# SmartContractService

| RPC | Request | Response | Comments |
| :--- | :--- | :--- | :--- |
| `createContract` | Transaction | TransactionResponse | Creates a contract |
| `updateContract` | Transaction | TransactionResponse | Updates a contract with the content |
| `contractCallMethod` | Transaction | TransactionResponse | Calls a contract |
| `getContractInfo` | Query | Response | Retrieves the contract information |
| `contractCallLocalMethod` | Query | Response | Calls a smart contract to be run on a single node |
| `ContractGetBytecode` | Query | Response | Retrieves the byte code of a contract |
| `getBySolidityID` | Query | Response | Retrieves a contract by its Solidity address |
| `getTxRecordByContractID` | Query | Response | Retrieves the 25-hour records stored for a contract |
| `deleteContract` | Transaction | TransactionResponse | Deletes a contract instance and transfers any remaining hbars to a specified receiver |
| `systemDelete` | Transaction | TransactionResponse | Deletes a contract if the submitting account has network admin privileges |
| `systemUndelete` | Transaction | TransactionResponse | Undeletes a contract if the submitting account has network admin privileges |

