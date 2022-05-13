# Wallet

{% hint style="info" %}
This feature is available in the Hedera JavaScript SDK only. (version >2.12.0).
{% endhint %}

The `Wallet` extends the `Signer`. The `Signer` is responsible for `Signing` requests while the `Provider` is responsible for communication between an application and a Hedera network, but is not required to communicate directly with a Hedera network. Note this means the `Provider` can for instance communicate with some third party service which finally communicates with a Hedera network.

## abstract class Wallet extends Signer

### **Methods**

<mark style="color:purple;">**`getProvider()`**</mark><mark style="color:purple;">**->**</mark>** `Provider`**

Returns the provider.

<mark style="color:purple;">**`getAccountKey()`**</mark><mark style="color:purple;">**->**</mark>** `Key`**

Returns the public key associated with this wallet.
