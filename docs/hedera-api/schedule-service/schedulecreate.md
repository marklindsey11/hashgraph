# ScheduleCreate

Create a new Scheduled Transaction. After the Scheduled Transaction is created, the Schedule ID for it is set in the receipt.

Users are able to create the Scheduled Transactions without the need for them to sign the scheduled underlying transaction \(f.e Account A creates Scheduled Transaction for Account B, C and D to sign\).

Creating immutable scheduled transaction: Scheduled Transaction can be created as immutable if the adminKey is omitted. In this case no one is able to execute ScheduleDelete operation and the Scheduled Transaction will either execute or expire.

Defining the Payer of the Transactions: By default, the payer of the Scheduled Transaction is the Account that creates it in the first place. However, users have the option to create Scheduled Transactions with Payer set to any account. If a Payer is provided, its signature will be required in order for the scheduled transaction to reach execution.

Providing Signatures as part of the creation: Users are able to provide signatures for the Scheduled Transaction as part of the creation itself.

Idempotent Creation: Creating Scheduled Transactions is an idempotent operation in the sense that if multiple parties perform ScheduleCreate operation specifying identical transactions, only the first one will create the transaction and the other operations will append the provided signatures.

The criteria for identical transactions is the following: If there is a previously created Scheduled Transaction, that hasn't yet been executed and all of the properties are exactly the same except for the sigMap \(transactionBody, adminKey, payerAccountID and memo\).

In that sense, ScheduleCreate transaction referring to an already created Scheduled Transaction and providing the rest of the required signature\(s\) will cause the underlying encoded transaction to be executed!

Note: Even though only the first ScheduleCreate Transaction will create new Scheduled Entity and the rest of them will have their signatures from the sigMap witnessed, the ScheduleID property in the TransactionReceipt will be set on all of them.

INVALID\_ACCOUNT\_ID is returned if the specified payerAccountID does not exist.

UNRESOLVABLE\_REQUIRED\_SIGNERS is returned if the transactionBody defines required Signers that cannot be resolved \(f.e signature from non-existing account is requested\)

UNPARSEABLE\_SCHEDULED\_TRANSACTION is returned if the transactionBody cannot be parsed into normal Transaction.

UNSCHEDULABLE\_TRANSACTION is returned if the transactionBody is representing a transaction that is not allowed to be scheduled \(f.e scheduling a ScheduleCreate transaction\).

SOME\_SIGNATURES\_WERE\_INVALID is returned if one of the signatures provided does not represent a valid signature for any required signer.

## ScheduleCreateTransactionBody

| Field | Type | Description | Signature Required |
| :--- | :--- | :--- | :--- |
| `transactionBody` | bytes | The transaction serialized into bytes that must be signed | Required |
| `adminKey` | [Key](../basic-types/key.md) | The Key which is able to delete the Scheduled Transaction \(if tx is not already executed\) | Optional |
| `payerAccountId` | [AccountID](../basic-types/accountid.md) | The account which is going to pay for the execution of the Scheduled TX. If not populated, the scheduling account is charged | Optional |
| `sigMap` | [SignatureMap](../basic-types/signaturemap.md) | Signatures that could be provided \(similarly to how signatures are provided in ScheduleSign operation\) on Scheduled Transaction creation | Optional |
| `memo` | string | Publicly visible information about the Scheduled entity, up to 100 bytes. No guarantee of uniqueness | Optional |

