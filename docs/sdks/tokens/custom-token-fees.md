# Custom token fees

When you create a token, you have the ability to set one or many custom fees \(up to 10\). Custom fees are fees that are distributed to the specified accounts each time the token is transferred programmatically. These custom fees can be either a fixed fee or a fractional fee. 

* A **fixed fee** transfers a specified amount of the token each time a token transfer is initiated to the account that was specified to collect the custom fee \(fee collector account\). The custom token fee does not depend on the amount of the token that is being transferred. 
* A **fractional fee** transfers the specified fraction of the total value of the tokens that are being transferred to the specified fee collecting account. Along with setting a custom fractional fee, you can impose minimum and maximum fee limits per transfer transaction. 

A custom fee schedule can include both types of fees. You can optionally set a token's fee schedule during the [creation of a token](define-a-token.md).

**Token Custom Fee Payment**

The account sending the token that has a custom fee schedule associated with it is responsible to pay for the custom fees. If the sending account does not have enough tokens to pay for the custom token fees plus transfer amount, the transaction will fail. A token's treasury account and any fee collecting accounts defined in the custom fee schedule for that token are exempt from paying any custom transaction fees when the token is transferred. 

**Limits**

* You can add up to 10 custom fees for a given token
* At most, two "levels" of custom token fees are allowed. In other words, a token being transferred may have a custom fee schedule \(first layer\) which requires you to pay fees in another token that has its own fee schedule \(second layer\). If that’s the case, a token paid as a fee within the second layer cannot have its own fee schedule, otherwise that would create a third layer.
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
//Create a custom token fixed fee schedule
new CustomFixedFee()
    .setAmount(1) //1 token is transferred to the fee collecting account each time this token is transferred
    .setFeeCollectorAccountId(AccountId.fromString("0.0.10")); // 1 token is sent to this account everytime it is transferred

//Version: 2.0.9
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create a custom token fixed fee schedule
new CustomFixedFee()
    .setAmount(1) //1 token is transferred to the fee collecting account each time this token is transferred
    .setFeeCollectorAccountId(AccountId.fromString("0.0.10")); // 1 token is sent to this account everytime it is transferred

//Version: 2.0.26
```
{% endcode %}

{% code title="Go" %}
```go
//Create a custom token fixed fee schedule
hedera.CustomFee{
			Fee: hedera.CustomFixedFee{
				Amount: 1}, // 1 token is transferred to the fee collecting account each time this token is transferred
			FeeCollectorAccountID: &feeCollectorAccountId,
		}

//Version: 2.1.11
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

{% code title="Java" %}
```java
//Create a custom token fractional fee schedule
new CustomFractionalFee()
    .setNumerator(1) // The numerator of the fraction
    .setDenominator(10) // The denominator of the fraction
    .setFeeCollectorAccountId(AccountId.fromString("0.0.10")); // The account collecting the 10% custom fee each time the token is transferred

//Version: 2.0.9
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Create a custom token fractional fee schedule
new CustomFractionalFee()
    .setNumerator(1) // The numerator of the fraction
    .setDenominator(10) // The denominator of the fraction
    .setFeeCollectorAccountId(AccountId.fromString("0.0.10")); // The account collecting the 10% custom fee each time the token is transferred

//Version: 2.0.26    
```
{% endcode %}

{% code title="Go" %}
```go
//Create a custom token fractional fee schedule (10% custom token fee)
hedera.CustomFee{
			Fee: hedera.CustomFractionalFee{
				Numerator: 1,
				Denominator: 10,},
			FeeCollectorAccountID: &accountId,
		}

//Version: 2.1.11
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

