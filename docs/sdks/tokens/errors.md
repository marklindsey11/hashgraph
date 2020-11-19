# Errors

Network errors and their descriptions.

| Errors | Description |
| :--- | :--- |
| ACCOUNT\_FROZEN\_FOR\_TOKEN | Account is frozen and cannot transact with the token |
| TOKENS\_PER\_ACCOUNT\_LIMIT\_EXCEEDED | Maximum number of token relations for agiven account is exceeded |
| INVALID\_TOKEN\_ID | The token is invalid or does not exist |
| INVALID\_TOKEN\_DECIMALS | Invalid token decimals |
| INVALID\_TOKEN\_INITIAL\_SUPPLY | Invalid token initial supply |
| INVALID\_TREASURY\_ACCOUNT\_FOR\_TOKEN | Invalid token initial supply |
| INVALID\_TOKEN\_SYMBOL | Token Symbol is not UTF-8 capitalized alphabetical string |
| TOKEN\_HAS\_NO\_FREEZE\_KEY | Freeze key is not set on token |
| TRANSFERS\_NOT\_ZERO\_SUM\_FOR\_TOKEN | Amounts in transfer list are not net zero |
| MISSING\_TOKEN\_SYMBOL | Token Symbol is not provided |
| TOKEN\_SYMBOL\_TOO\_LONG | Token Symbol is too long |
| ACCOUNT\_KYC\_NOT\_GRANTED\_FOR\_TOKEN | KYC must be granted and account does not have KYC granted |
| TOKEN\_HAS\_NO\_KYC\_KEY | KYC key is not set on token |
| INSUFFICIENT\_TOKEN\_BALANCE | Token balance is not sufficient for the transaction |
| TOKEN\_WAS\_DELETED | Token transactions cannot be executed on deleted token |
| TOKEN\_HAS\_NO\_SUPPLY\_KEY | Supply key is not set on token |
| TOKEN\_HAS\_NO\_WIPE\_KEY | Wipe key is not set on token |
| INVALID\_TOKEN\_MINT\_AMOUNT | Invalid mint amount |
| INVALID\_TOKEN\_BURN\_AMOUNT | Invalid burn amount |
| TOKEN\_NOT\_ASSOCIATED\_TO\_ACCOUNT | Account has not been associated to an account |
| CANNOT\_WIPE\_TOKEN\_TREASURY\_ACCOUNT | Cannot execute wipe operation on treasury account |
| INVALID\_KYC\_KEY | Invalid kyc key |
| INVALID\_WIPE\_KEY | Invalid wipe key |
| INVALID\_FREEZE\_KEY | Invalid freeze key |
| INVALID\_SUPPLY\_KEY | Invalid supply key |
| MISSING\_TOKEN\_NAME | Token Name is not provided |
| TOKEN\_NAME\_TOO\_LONG | Token Name is too long |
| INVALID\_WIPING\_AMOUNT | The provided wipe amount must not be negative, zero or bigger than the token holder balance |
| TOKEN\_IS\_IMMUTABLE | Token does not have Admin key set, thus update/delete transactions cannot be performed |
| TOKEN\_ALREADY\_ASSOCIATED\_TO\_ACCOUNT | An associateToken operation specified a token already associated to the account |
| TRANSACTION\_REQUIRES\_ZERO\_TOKEN\_BALANCES | An attempted operation is invalid until all token balances for the target account are zero |
| ACCOUNT\_IS\_TREASURY | An attempted operation is invalid because the account is a treasury |
| TOKEN\_ID\_REPEATED\_IN\_TOKEN\_LIST | Same TokenIDs present in the token list |
| TOKEN\_TRANSFER\_LIST\_SIZE\_LIMIT\_EXCEEDED | Exceeded the number of token transfers \(both from and to\) allowed for token transfer list |
| EMPTY\_TOKEN\_TRANSFER\_BODY | TokenTransfersTransactionBody has no TokenTransferList |
| EMPTY\_TOKEN\_TRANSFER\_ACCOUNT\_AMOUNTS | TokenTransfersTransactionBody has a TokenTransferList with no AccountAmounts |

