# ContractDelete

## **ContractDeleteTransactionBody**

Modify a smart contract instance to have the given parameter values. Any null field is ignored \(left unchanged\). If only the contractInstanceExpirationTime is being modified, then no signature is needed on this transaction other than for the account paying for the transaction itself. But if any of the other fields are being modified, then it must be signed by the adminKey. The use of adminKey is not currently supported in this API, but in the future will be implemented to allow these fields to be modified, and also to make modifications to the state of the instance. If the contract is created with no admin key, then none of the fields can be changed that need an admin signature, and therefore no admin key can ever be added. So if there is no admin key, then things like the bytecode are immutable. But if there is an admin key, then they can be changed. For example, the admin key might be a threshold key, which requires 3 of 5 binding arbitration judges to agree before the bytecode can be changed. This can be used to add flexibility to the mangement of smart contract behavior. But this is optional. If the smart contract is created without an admin key, then such a key can never be added, and its bytecode will be immutable.

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| contractID | [ContractID](../basic-types/contractid.md) | The Contract ID instance to delete \(this can't be changed\) |  |
| obtainers | oneof |  |  |
|  | transferAccountID | [AccountID](../basic-types/accountid.md) | The account ID which will receive all remaining hbars |
|  | transferContractID | [ContractID](../basic-types/contractid.md) | The contract ID which will receive all remaining hbars |

