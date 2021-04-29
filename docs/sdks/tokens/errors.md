# Network Response Messages

Network response messages and their descriptions.

| Network Response | Description |
| :--- | :--- |
| `ACCOUNT_FROZEN_FOR_TOKEN` | Account is frozen and cannot transact with the token |
| `TOKENS_PER_ACCOUNT_LIMIT_EXCEEDED` | Maximum number of token relations for a given account is exceeded |
| `INVALID_TOKEN_ID` | The token is invalid or does not exist |
| `INVALID_TOKEN_DECIMALS` | Invalid token decimals |
| `INVALID_TOKEN_INITIAL_SUPPLY` | Invalid token initial supply |
| `INVALID_TREASURY_ACCOUNT_FOR_TOKEN` | Invalid token initial supply |
| `INVALID_TOKEN_SYMBOL` | Token Symbol is not UTF-8 capitalized alphabetical string |
| `TOKEN_HAS_NO_FREEZE_KEY` | Freeze key is not set on token |
| `TRANSFERS_NOT_ZERO_SUM_FOR_TOKEN` | Amounts in transfer list are not net zero |
| `MISSING_TOKEN_SYMBOL` | Token Symbol is not provided |
| `TOKEN_SYMBOL_TOO_LONG` | Token Symbol is too long |
| `ACCOUNT_KYC_NOT_GRANTED_FOR_TOKEN` | KYC must be granted and account does not have KYC granted |
| `TOKEN_HAS_NO_KYC_KEY` | KYC key is not set on token |
| `INSUFFICIENT_TOKEN_BALANCE` | Token balance is not sufficient for the transaction |
| `TOKEN_WAS_DELETED` | Token transactions cannot be executed on deleted token |
| `TOKEN_HAS_NO_SUPPLY_KEY` | Supply key is not set on token |
| `TOKEN_HAS_NO_WIPE_KEY` | Wipe key is not set on token |
| `INVALID_TOKEN_MINT_AMOUNT` | Invalid mint amount |
| `INVALID_TOKEN_BURN_AMOUNT` | Invalid burn amount |
| `TOKEN_NOT_ASSOCIATED_TO_ACCOUNT` | Account has not been associated to an account |
| `CANNOT_WIPE_TOKEN_TREASURY_ACCOUNT` | Cannot execute wipe operation on treasury account |
| `INVALID_KYC_KEY` | Invalid kyc key |
| `INVALID_WIPE_KEY` | Invalid wipe key |
| `INVALID_FREEZE_KEY` | Invalid freeze key |
| `INVALID_SUPPLY_KEY` | Invalid supply key |
| `MISSING_TOKEN_NAME` | Token Name is not provided |
| `TOKEN_NAME_TOO_LONG` | Token Name is too long |
| `INVALID_WIPING_AMOUNT` | The provided wipe amount must not be negative, zero or bigger than the token holder balance |
| `TOKEN_IS_IMMUTABLE` | Token does not have Admin key set, thus update/delete transactions cannot be performed |
| `TOKEN_ALREADY_ASSOCIATED_TO_ACCOUNT` | An associateToken operation specified a token already associated to the account |
| `TRANSACTION_REQUIRES_ZERO_TOKEN_BALANCES` | An attempted operation is invalid until all token balances for the target account are zero |
| `ACCOUNT_IS_TREASURY` | An attempted operation is invalid because the account is a treasury |
| `TOKEN_ID_REPEATED_IN_TOKEN_LIST` | Same TokenIDs present in the token list |
| `TOKEN_TRANSFER_LIST_SIZE_LIMIT_EXCEEDED` | Exceeded the number of token transfers \(both from and to\) allowed for token transfer list |
| `EMPTY_TOKEN_TRANSFER_BODY` | TokenTransfersTransactionBody has no TokenTransferList |
| `EMPTY_TOKEN_TRANSFER_ACCOUNT_AMOUNTS` | TokenTransfersTransactionBody has a TokenTransferList with no AccountAmounts |

