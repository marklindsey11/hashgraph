# FileService

| RPC | Request | Response | Comments |
| :--- | :--- | :--- | :--- |
| `createFile` | Transaction | TransactionResponse | Creates a file  |
| `updateFile` | Transaction | TransactionResponse | Updates a file  |
| `deleteFile` | Transaction | TransactionResponse | Deletes a file |
| `appendContent` | Transaction | TransactionResponse | Appends the file  |
| `getFileContent` | Query | Response | Retrieves the file content  |
| `getFileInfo` | Query | Response | Retrieves the file information  |
| `systemDelete` | Transaction | TransactionResponse | Deletes a file if the submitting account has network admin privileges |
| `systemUndelete` | Transaction | TransactionResponse | Undeletes a file if the submitting account has network admin privileges |

