# Custom token fees

When you create a token, you have the ability to set one or many custom fees \(up to 10\). Custom fees are fees that are distributed to the specified accounts each time the token is transferred programmatically. These custom fees can be either a fixed fee, fractional fee, or royalty fee. 

* A **fixed fee** transfers a specified amount of the token each time a token transfer is initiated to the account that was specified to collect the custom fee \(fee collector account\). The custom token fee does not depend on the amount of the token that is being transferred. Applicable to both fungible and non-fungible tokens. 
* A **fractional fee** transfers the specified fraction of the total value of the tokens that are being transferred to the specified fee collecting account. Along with setting a custom fractional fee, you can impose minimum and maximum fee limits per transfer transaction. Applicable to fungible tokens only.
* A **royalty fee** is a fractional fee that is assessed each time the ownership of an NFT is transferred from person A to person B. The fee collector account ID defined in the royalty fee schedule will receive the royalty fee each time. The royalty fee charged is a fraction of the value exchanged for the NFT. If there is no value exchanged for the NFT, a fallback fee can be used to charge the receiving account. Applicable to non-fungible tokens only.

A custom fee schedule can include both types of fees. You can optionally set a token's fee schedule during the [creation of a token](define-a-token.md).

**Token Custom Fee Payment**

* Fractional fees are by default charged to the token transfer receiver. This means the receiving account of the fungible token will receive less than the transfer amount \(transfer amount - custom fees\). If the `net_of_transfers` field is set to true, the fractional fees are then charged to the sending account. In this case, the receiving account will receive the full amount of the token transfer value.
* Fixed fees are paid by the sending account in the fungible or non-fungible token transfer transaction.
* Royalty fees are paid by the sending account in a non-fungible token transfer transaction. When the NFT sender does not receive any fungible value, the fallback fee is charged to the NFT receiver
* The accounts transferring the token to the receiving accounts are responsible for paying the transfer transaction fee in hbar.

In addition to the custom token fee payment, the sender account is required to pay for the token transfer transaction fee in hbar.

**Limits**

* You can add up to 10 custom fees for a given token
* A token's treasury account and any fee collecting accounts defined in the custom fee schedule for a token are exempt from paying any custom transaction fees when the token is transferred. 
* At most, two "levels" of custom token fees are allowed. In other words, a token being transferred may have a custom fee schedule \(first layer\) which requires you to pay fees in another token that has its own fee schedule \(second layer\). If that’s the case, a token paid as a fee within the second layer cannot have its own fee schedule, otherwise, that would create a third layer.
* Fees cannot be a negative value

## Custom Fee 

### Fixed Fee

* The fee collector account collects the defined fee amount
* The amount is the amount of the token the fee collecting account will collect each time the token with the custom fee schedule is transferred
* The denominating token is the token to charge the custom fee in
  * To use the ID of the token generated in the transaction, enter "0.0.0" for the token ID
  * If this field is left blank, the default token is hbar

| Constructor | Description |
| :--- | :--- |
| `new CustomFixedFee()` | Initializes the CustomFixedFee object |

```java
new CustomFixedFee()
```

#### Methods

{% tabs %}
{% tab title="V2" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setFeeCollectorAccountId(<accountId>)` | [AccountId](../../hedera-api/basic-types/accountid.md) | Required |
| `setAmount(<amount>)` | long | Required |
| `setDenominatingTokenId(<tokenId>)` | [TokenId](../../hedera-api/basic-types/tokenid.md) | Required |

{% code title="Java" %}
```java
//Create a custom token fixed
new CustomFixedFee()
    .setAmount(1) // 1 token is transferred to the fee collecting account each time this token is transferred
    .setFeeCollectorAccountId(feeCollectorAccountId); // 1 token is sent to this account everytime it is transferred

//Version: 2.0.9
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create a custom token fixed
new CustomFixedFee()
    .setAmount(1) // 1 token is transferred to the fee collecting account each time this token is transferred
    .setFeeCollectorAccountId(feeCollectorAccountId); // 1 token is sent to this account everytime it is transferred

//Version: 2.0.26
```
{% endcode %}

{% code title="Go" %}
```go
//Create a custom token fixed
fractionalFee := []hedera.Fee{
		hedera.CustomFixedFee{
			CustomFee: hedera.CustomFee{
				FeeCollectorAccountID: &feeCollectorAccountId, // 1 token is sent to this account everytime it is transferred
			},
			Amount: 1, // 1 token is transferred to the fee collecting account each time this token is transferred
	},
}

//Version: 2.1.15
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setFeeCollectorAccountId(<accountId>)` | [AccountId](../specialized-types.md#accountid) | Required |
| `setAmount(<amount>)` | long | Required |
| `setDenominatingTokenId(<tokenId>)` | [TokenId](token-id.md) | Optional |

{% code title="Java" %}
```java
//Create a custom token fixed fee schedule
new CustomFixedFee()
    .setAmount(1) //1 token is transferred to the fee collecting account each time this token is transferred
    .setFeeCollectorAccountId(AccountId.fromString("0.0.10")); // 1 token is sent to this account everytime it is transferred

//Version: 1.5.0
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create a custom token fixed fee schedule
new CustomFixedFee()
    .setAmount(1) //1 token is transferred to the fee collecting account each time this token is transferred
    .setFeeCollectorAccountId(AccountId.fromString("0.0.10")); // 1 token is sent to this account everytime it is transferred

//Version: 1.4.10
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Fractional Fee

* The fee collector account is the account that will collect the specified fee amount
* The denominator of the fractional fee cannot be zero
* The fractional fee has to be less than or equal to 1
* You can apply a minimum or maximum fee to charge in cases the percentage of the transfer amount is too low or too high
* Cannot exceed the fractional range of a 64 bit signed integer
* If the assessment method field is set, the token's custom fee is charged to the sending account and the receiving account receives the full token transfer amount. If this field is set to false, the receiver pays for the token custom fees and gets the remaining token balance.

| Constructor | Description |
| :--- | :--- |
| `new CustomFractionalFee()` | Initializes the CustomFractionalFee object |

```java
new CustomFractionalFee()
```

#### Methods

{% tabs %}
{% tab title="V2" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setFeeCollectorAccountId(<accountId>)` | [AccountId](../specialized-types.md#accountid) | Required |
| `setNumerator(<numerator>)` | long | Required |
| `setDenominator(<amount>)` | long | Required |
| `setMax(<max>)` | long | Optional |
| `setMin(<min>)` | long | Optional |
| `setAssessmentMethod(<assessmentMethod>)` | FeeAssessmentMethod | Optional |

{% code title="Java" %}
```java
//Create a custom token fractional
new CustomFractionalFee()
    .setNumerator(1) // The numerator of the fraction
    .setDenominator(10) // The denominator of the fraction
    .setFeeCollectorAccountId(feeCollectorAccountId); // The account collecting the 10% custom fee each time the token is transferred

//Version: 2.0.9
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create a custom token fractional
new CustomFractionalFee()
    .setNumerator(1) // The numerator of the fraction
    .setDenominator(10) // The denominator of the fraction
    .setFeeCollectorAccountId(feeCollectorAccountId); // The account collecting the 10% custom fee each time the token is transferred

//Version: 2.0.26    
```
{% endcode %}

{% code title="Go" %}
```go
//Create a custom token fractional
fractionalFee := []hedera.Fee{
		hedera.CustomFractionalFee{
			CustomFee: hedera.CustomFee{
				FeeCollectorAccountID: &feeCollectorAccountId, // The account collecting the 10% custom fee each time the token is transferred
			},
			Numerator:   1, // The numerator of the fraction
			Denominator: 10, // The denominator of the fraction
		},
}

//Version: 2.1.15
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setFeeCollectorAccountId(<accountId>)` | [AccountId](../specialized-types.md#accountid) | Required |
| `setNumerator(<numerator>)` | long | Required |
| `setDenominator(<amount>)` | long | Required |
| `setMax(<max>)` | long | Optional |
| `setMin(<min>)` | long | Optional |
| `setAssessmentMethod(<assessmentMethod>)` | FeeAssessmentMethod | Optional |

{% code title="Java" %}
```java
//Create a custom token fractional fee schedule
new CustomFractionalFee()
    .setNumerator(1) // The numerator of the fraction
    .setDenominator(10) // The denominator of the fraction
    .setFeeCollectorAccountId(AccountId.fromString("0.0.10")); // The account collecting the 10% custom fee each time the token is transferred

//Version: 1.5.0
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create a custom token fractional fee schedule 
new CustomFractionalFee()
    .setNumerator(1) // The numerator of the fraction
    .setDenominator(10) // The denominator of the fraction
    .setFeeCollectorAccountId(AccountId.fromString("0.0.10")); // The account collecting the 10% custom fee each time the token is transferred
    
//Version: 1.4.10
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Royalty Fee

* Royalty fee charges a fraction of the value exchanged in a NFT transfer transaction. The fractional value is set by designating the numerator and denominator of the fraction.
* The fallback fee is a [fixed fee](custom-token-fees.md#fixed-fee) that is charged to the NFT receiver when there is no fungible value exchanged with the sender of the NFT

{% hint style="info" %}
Royalty fees are only applicable to non-fungible tokens \(NFTs\).
{% endhint %}

| Constructor | Description |
| :--- | :--- |
| `new CustomRoyaltyFee()` | Initializes the CustomRoyaltyFee object |

```java
new CustomRoyaltyFee()
```

#### Methods

{% tabs %}
{% tab title="V2" %}
| Method | Type | Requirement |
| :--- | :--- | :--- |
| `setNumerator(<numerator>)` | long | Required |
| `setDenominator(<denominator>)` | long | Required |
| `setFallbackFee(<fallbackFee>)` | [CustomFixedFee](custom-token-fees.md#fixed-fee) | Optional |
| `setFeeCollectorAccountId(<>)` | AccountId | Required |

{% code title="Java" %}
```java
//Create a royalty fee
new CustomRoyaltyFee()
     .setNumerator(1) // The numerator of the fraction
     .setDenominator(10) // The denominator of the fraction
     .setFallbackFee(new CustomFixedFee().setHbarAmount(new Hbar(1)) // The fallback fee
     .setFeeCollectorAccountId(feeCollectorAccountId))) // The account that will receive the royalty fee

// v2.0.12 
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create a royalty fee
new CustomRoyaltyFee()
     .setNumerator(1) // The numerator of the fraction
     .setDenominator(10) // The denominator of the fraction
     .setFallbackFee(new CustomFixedFee().setHbarAmount(new Hbar(1)) // The fallback fee
     .setFeeCollectorAccountId(feeCollectorAccountId))) // The account that will receive the royalty fee
     
 // v2.0.29 
```
{% endcode %}

{% code title="Go" %}
```go
//Create a royalty fee 
royaltyFee := []hedera.Fee{
		hedera.CustomRoyaltyFee{
			CustomFee: hedera.CustomFee{
				FeeCollectorAccountID: &feeCollectorAccountId, // The account that will receive the royalty fee
			},
			Numerator:   1, 
     .setNumerator(1) // The numerator of the fraction
			Denominator: 10, // The denominator of the fraction
			FallbackFee: &hedera.CustomFixedFee{
				CustomFee: hedera.CustomFee{
					FeeCollectorAccountID: &feeCollectorAccountId,
				},
				Amount: 1, // The fallback fee
			},
		}
	
// v2.1.15
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
Coming soon...
{% endtab %}
{% endtabs %}

## 



