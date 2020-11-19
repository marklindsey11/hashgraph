# Hbars

| Constructor | Type | Description |
| :--- | :--- | :--- |
| `new Hbar(<amount>)` | Hbar | Initializes the Hbar object |

```java
new Hbar(<amount>)
```

## Hbar from:

Construct hbars from different representations.

{% tabs %}
{% tab title="V2" %}
| Method | Type | Description |
| :--- | :--- | :--- |
| `Hbar.from(<hbars>)`  | long / BigDecimal | Returns an Hbar whose value is equal to the specified value |
| `Hbar.from(<hbars, unit>)` | long / BigDecimal , HbarUnit | Returns an Hbar representing the value in the given units |
| `Hbar.fromString(<text>)` | CharSequence  | Converts the provided string into an amount of hbars |
| `Hbar.fromString(<text, unit>)` | CharSequence, HbarUnit | Converts the provided string into an amount of hbars |
| `Hbar.fromTinybar(<tinybars>)` | long | Returns an Hbar converted from the specified number of tinybars |

{% code title="Java" %}
```java
//100 hbars
new Hbar(1000);

//100 hbars from hbar value
Hbar.from(100);

//100 tinybars from hbars convert to unit
Hbar.from(100, HbarUnit.TINYBAR);

// 100 hbars converted from string value
Hbar.fromString("100");

//100 tinybars from string value
Hbar.fromString("100", HbarUnit.TINYBAR);

//v2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```java
// 100 hbars
new Hbar(1000);

//100 hbars
Hbar.from(100);

//100 tinybars
Hbar.from(100, HbarUnit.TINYBAR);

// 100 hbars converted from string value
Hbar.fromString("100");

//100 tinybars from string value
Hbar.fromString("100", HbarUnit.TINYBAR); 
```
{% endcode %}

{% code title="Go" %}
```java
//100 hbars
hedera.NewHbar(100)

//100 tinybars
hedera.HbarFrom(100, hedera.HbarUnits.Tinybar)

//v2.0.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Method | Type | Description |
| :--- | :--- | :--- |
| `Hbar.from(<amount, unit>)` | HbarUnit | Hbars from the provided denomination |
| `Hbar.fromTinybar(<amount>)` | long | Hbars converted from tinybars |

{% code title="Java" %}
```java
//100 hbars converted to tinybars
Hbar.from(100, HbarUnit.Tinybar);

//Hbars from tinybars
Hbar.fromTinybar(100);

//v1.3.2
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//100 hbars converted to tinybars
Hbar.from(100, HbarUnit.Tinybar);

//Hbars from tinybars
Hbar.fromTinybar(100);

//v1.4.4
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Hbar to:

Convert hbars to a different unit/format.

{% tabs %}
{% tab title="V2" %}
| Method | Type | Description |
| :--- | :--- | :--- |
| `to(<unit>)` | HbarUnit | Specifiy the unit of hbar to convert to. Use `As` for Go. |
| `toString(<unit>)` | HbarUnit | String value of the hbar unit to convert to. Use `String()` for Go. |
| `toTinybar()` | Long | Hbar value converted to tinybars |

{% code title="Java" %}
```java
//100 hbars converted to tinybars
new Hbar(100).to(HbarUnit.TINYBAR);

//100 hbars converted to tinybars
new Hbar(100).toString(HbarUnit.TINYBAR);

//100 hbars converted to tinybars
new Hbar(100).toTinybars();

//v2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```java
//100 hbars converted to tinybars
new Hbar(100).to(HbarUnit.TINYBAR);

//100 hbars converted to tinybars
new Hbar(100).toString(HbarUnit.TINYBAR);

//100 hbars converted to tinybars
new Hbar(100).toTinybars();
```
{% endcode %}

{% code title="Go" %}
```java
//100 hbars converted to tinybars
hedera.NewHbar(100).As(hedera.HbarUnits.Tinybar)

//100 hbars to string format
hedera.NewHbar(100).String()

//100 hbars converted to tinybars
hedera.NewHbar(100).AsTinybar()
//v2.0.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Method | Type | Description |
| :--- | :--- | :--- |
| `as(<unit>)` | HbarUnit | Specifiy the unit of hbar to convert to. Use `As` for Go. |
| `toString()` | Long | Hbar value converted to tinybars |

{% code title="Java" %}
```java
//100 hbars converted to tinybars
new Hbar(100).as(HbarUnit.Tinybar);

//100 hbars converted to tinybars
new Hbar(100).toTinybars();

//v1.3.2
```
{% endcode %}

{% code title="JavaScript" %}
```java
//100 hbars converted to tinybars
new Hbar(100).as(HbarUnit.Tinybar);

//100 hbars converted to tinybars
new Hbar(100).toTinybars();

//v1.4.4
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Hbar constants:

Provided constant values of hbars.

{% tabs %}
{% tab title="V2" %}
| Method | Type | Description |
| :--- | :--- | :--- |
| `Hbar.MAX` | Hbar | A constant value of the maximum number of hbars \(50\_000\_000\_000 hbars\) |
| `Hbar.MIN` | Hbar | A constant value of the minimum number of hbars \(-50\_000\_000\_000 hbars\) |
| `Hbar.ZERO` | Hbar | A constant value of zero hbars |

{% code title="Java" %}
```java
//The maximum number of hbars
Hbar hbarMax = Hbar.MAX; 

//The minimum number of hbars
Hbar hbarMin = Hbar.MIN;

//A constant value of zero hbars
Hbar hbarZero = Hbar.ZERO; 

//v2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```java
//The maximum number of hbars
const hbarMax = Hbar.MAX; 

//The minimum number of hbars
const hbarMin = Hbar.MIN;

//A constant value of zero hbars
const hbarZero = Hbar.ZERO; 
```
{% endcode %}

{% code title="Go" %}
```java
//The maximum number of hbars
hbarMax := hedera.MaxHbar

//The minimum number of hbars
hbarMin := hedera.MinHbar

//A constant value of zero hbars
hbarZero := hedera.ZeroHbar

//v2.0.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Method | Type | Description |
| :--- | :--- | :--- |
| `Hbar.MAX` | Hbar | A constant value of the maximum number of hbars \(50\_000\_000\_000 hbars\) |
| `Hbar.MIN` | Hbar | A constant value of the minimum number of hbars \(-50\_000\_000\_000 hbars\) |
| `Hbar.ZERO` | Hbar | A constant value of zero hbars |

{% code title="Java" %}
```java
//The maximum number of hbars
Hbar hbarMax = Hbar.MAX; 

//The minimum number of hbars
Hbar hbarMin = Hbar.MIN;

//Zero hbars
Hbar hbarZero = Hbar.ZERO; 

//v1.3.2
```
{% endcode %}

{% code title="JavaScript" %}
```java
//The maximum number of hbars
const hbarMax = Hbar.MAX; 

//The minimum number of hbars
const hbarMin = Hbar.MIN;

//Zero hbars
const hbarZero = Hbar.ZERO; 

//v1.4.4
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Hbar units

Define the unit of hbar to represent.

{% tabs %}
{% tab title="V2" %}
| Function | Description |
| :--- | :--- |
| `HbarUnit.TINYBAR` | The atomic \(smallest\) unit of hbar, used natively by the Hedera network |
| `HbarUnit.MICROBAR` | Equivalent to 100 tinybar or 1⁄1,000,000 hbar. |
| `HbarUnit.MILIBAR` | Equivalent to 100,000 tinybar or 1⁄1,000 hbar |
| `HbarUnit.HBAR` | The base unit of hbar, equivalent to 100 million tinybar. |
| `HbarUnit.KILOBAR` | Equivalent to 1 thousand hbar or 100 billion tinybar.HbarUnit.Megbar |
| `HbarUnit.MEGABAR` | Equivalent to 1 million hbar or 100 trillion tinybar. |
| `HbarUnit.GIGABAR` | Equivalent to 1 billion hbar or 100 quadillion tinybar. |

{% code title="Java" %}
```java
//100 tinybars
Hbar.from(100, HbarUnit.TINYBAR);

//v2.0.0
```
{% endcode %}

{% code title="JavaScript" %}
```java
//100 tinybars
Hbar.from(100, HbarUnit.TINYBAR);

//v2.0.0
```
{% endcode %}

{% code title="Go" %}
```java
//100 tinybars
hedera.HbarFrom(100, hedera.HbarUnits.Tinybar)

//v2.0.0
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}
| Function | Description |
| :--- | :--- |
| `HbarUnit.Tinybar` | The atomic \(smallest\) unit of hbar, used natively by the Hedera network |
| `HbarUnit.Microbar` | Equivalent to 100 tinybar or 1⁄1,000,000 hbar. |
| `HbarUnit.Milibar` | Equivalent to 100,000 tinybar or 1⁄1,000 hbar |
| `HbarUnit.Hbar` | The base unit of hbar, equivalent to 100 million tinybar. |
| `HbarUnit.Kilobar` | Equivalent to 1 thousand hbar or 100 billion tinybar.HbarUnit.Megbar |
| `HbarUnit.Megabar` | Equivalent to 1 million hbar or 100 trillion tinybar. |
| `HbarUnit.Gigabar` | Equivalent to 1 billion hbar or 100 quadillion tinybar. |

{% code title="Java" %}
```java
Hbar.from(100, HbarUnit.Tinybar);

//v1.3.2
```
{% endcode %}

{% code title="JavaScript" %}
```java
Hbar.from(100, HbarUnit.Tinybar);

//v1.4.4
```
{% endcode %}
{% endtab %}
{% endtabs %}



