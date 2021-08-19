# Get NFT info

A query that returns information about a non-fungible token \(NFT\). There are three different ways you can get NFT information:

* NFT ID
* Token ID
* Account ID

{% hint style="warning" %}
Requesting NFT info by Token ID or Account ID is currently disabled in the[ 0.17.2 release](https://github.com/hashgraph/hedera-services/releases/tag/v0.17.2).
{% endhint %}

The request returns the following information:

| Item | Description |
| :--- | :--- |
| **NFT ID** | The ID of the non-fungible token in x.y.z format. |
| **Account ID** | The account ID of the current owner of the NFT |
| **Creation Time** | The effective consensus timestamp at which the NFT was minted |
| **Metadata**  | Represents the unique metadata of the NFT |

| Constructor | Description |
| :--- | :--- |
| `new TokenNftInfoQuery()` | Initializes the TokenNFTInfoQuery object |

```java
new TokenNftInfoQuery()
```

### Methods

{% tabs %}
{% tab title="V2" %}
| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `byAccountId(<accountId>)` | AccountId | Applicable only to tokens of type `NON_FUNGIBLE_UNIQUE`. Gets info on NFTs N through M owned by the specified accountId. Use `setStart()` and `setEnd()`. | Optional |
| `byNftId(<nftId>)` | [NftId](nft-id.md) | Applicable only to tokens of type `NON_FUNGIBLE_UNIQUE`. Gets info on a NFT for a given TokenID \(of type `NON_FUNGIBLE_UNIQUE`\) and serial number. | Optional |
| `byTokenId(<tokenId>)` | TokenId | Applicable only to tokens of type `NON_FUNGIBLE_UNIQUE`. Gets info on NFTs N through M on the list of NFTs associated with a given `NON_FUNGIBLE_UNIQUE` Token. Use `setStart()` and `setEnd()`. | Optional |
| `setStart(<start>)` | long | Specifies the start index \(inclusive\) of the range of NFTs to query for. Value must be in the range \[0; ownedNFTs-1\] | Optional  |
| `setEnd(<end>)` | long | Specifies the end index \(exclusive\) of the range of NFTs to query for. Value must be in the range \(start; ownedNFTs\] | Optional |

{% code title="Java" %}
```java
//Returns the info for the specified NFT ID
List<TokenNftInfo> nftInfos = new TokenNftInfoQuery()
     .byNftId(nftId)
     .execute(client);

//v2.0.11
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Returns the info for the specified NFT ID
const nftInfos = await new TokenNftInfoQuery()
     .byNftId(nftId)
     .execute(client);

//v2.0.28
```
{% endcode %}

{% code title="Go" %}
```go
//Returns the info for the specified NFT ID
nftInfo, err := NewTokenNftInfoQuery().
   ByNftID(nftID).
	 Execute(client)

//v2.1.14
```
{% endcode %}
{% endtab %}

{% tab title="V1" %}


| Method | Type | Description | Requirement |
| :--- | :--- | :--- | :--- |
| `byAccountId(<accountId, start, end>)` | [AccountId](../specialized-types.md#accountid), long, long | Applicable only to tokens of type `NON_FUNGIBLE_UNIQUE`. Gets info on NFTs N through M owned by the specified accountId. Use `setStart()` and `setEnd()`. | Optional |
| `byNftId(<nftId>)` | [NftId](nft-id.md) | Applicable only to tokens of type `NON_FUNGIBLE_UNIQUE`. Gets info on a NFT for a given TokenID \(of type `NON_FUNGIBLE_UNIQUE`\) and serial number. | Optional |
| `byTokenId(<tokenId, start, end>)` | [TokenId](token-id.md), long, long | Applicable only to tokens of type `NON_FUNGIBLE_UNIQUE`. Gets info on NFTs N through M on the list of NFTs associated with a given `NON_FUNGIBLE_UNIQUE Start` and `End` designates the index range to return the NFTs for. | Optional |

{% code title="Java" %}
```java
//Returns the info for the specified NFT ID
List<TokenNftInfo> nftInfos = new TokenNftInfoQuery()
     .byNftId(nftId)
     .execute(client);
     
//v1.5.0
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Returns the info for the specified NFT ID
const nftInfos = await new TokenNftInfoQuery()
     .byNftId(nftId)
     .execute(client);

//v1.4.10
```
{% endcode %}
{% endtab %}
{% endtabs %}



