# ContractCallLocal

## **ContractCallLocalQuery**

Call a function of the given smart contract instance, giving it functionParameters as its inputs. It will consume the entire given amount of gas.

| Field                | Type                                           | Description                                                                                                                                                                                                     |
| -------------------- | ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `header`             | [QueryHeader](../miscellaneous/queryheader.md) | Standard info sent from client to node, including the signed payment, and what kind of response is requested (cost, state proof, both, or neither). The payment must cover the fees and all of the gas offered. |
| `contractID`         | [ContractID](../basic-types/contractid.md)     | The contract instance to call, in the format used in transactions                                                                                                                                               |
| `gas`                | int64                                          | The amount of gas to use for the call. All of the gas offered will be charged for.                                                                                                                              |
| `functionParameters` | bytes                                          | Which function to call, and the parameters to pass to the function                                                                                                                                              |
| `maxResultSize`      | int64                                          | Max number of bytes that the result might include. The run will fail if it would have returned more than this number of bytes. **\[deprecated 0.20.0]**                                                         |

## ContractCallLocalResponse

Response when the client sends the node ContractCallLocalQuery

| Field            | Type                                                                | Description                                                                                                      |
| ---------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `header`         | [ResponseHeader](../miscellaneous/responseheader.md#responseheader) | standard response from node to client, including the requested fields: cost, or state proof, or both, or neither |
| `functionResult` | ContractFunctionResult                                              | the value returned by the function (if it completed and didn't fail)                                             |

## ContractFunctionResult

The result returned by a call to a smart contract function. This is part of the response to a ContractCallLocal query, and is in the record for a ContractCall or ContractCreateInstance transaction. The ContractCreateInstance transaction record has the results of the call to the constructor.

| Field                | Type                                       | Description                                                        |
| -------------------- | ------------------------------------------ | ------------------------------------------------------------------ |
| `contractID`         | [ContractID](../basic-types/contractid.md) | the smart contract instance whose function was called              |
| `contractCallResult` | bytes                                      | the result returned by the function                                |
| `errorMessage`       | string                                     | message In case there was an error during smart contract execution |
| `bloom`              | bytes                                      | bloom filter for record                                            |
| `gasUsed`            | uint64                                     | units of gas used to execute contract                              |
| `logInfo`            | ContractLoginfo                            | the log info for events returned by the function                   |

## ContractLoginfo

The log information for an event returned by a smart contract function call. One function call may return several such events.

| Field        | Type                                       | Description                                  |
| ------------ | ------------------------------------------ | -------------------------------------------- |
| `contractID` | [ContractID](../basic-types/contractid.md) | Address of a contract that emitted the event |
| `bloom`      | bytes                                      | Bloom filter for a particular log            |
| `topic`      | repeated bytes                             | Topics of a particular event                 |
| `data`       | bytes                                      | Event data                                   |
