# Get NFT info

A query that returns information about a non-fungible token \(NFT\). You request the info for an NFT by specifying the NFT ID.

{% hint style="warning" %}
Requesting NFT info by Token ID or Account ID is currently disabled in the[ 0.17 release](https://github.com/hashgraph/hedera-services/releases/tag/v0.17.2).
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
| `setNftId(<nftId>)` | [NftId](nft-id.md) | Applicable only to tokens of type `NON_FUNGIBLE_UNIQUE`. Gets info on a NFT for a given TokenID \(of type `NON_FUNGIBLE_UNIQUE`\) and serial number. | Optional |

{% code title="Java" %}
```java
//Returns the info for the specified NFT ID
List<TokenNftInfo> nftInfos = new TokenNftInfoQuery()
     .setNftId(nftId)
     .execute(client);

//v2.0.14
```
{% endcode %}

{% code title="JavaScript" %}
```javascript
//Returns the info for the specified NFT ID
const nftInfos = await new TokenNftInfoQuery()
     .setNftId(nftId)
     .execute(client);

//v2.0.28
```
{% endcode %}

{% code title="Go" %}
```go
//Returns the info for the specified NFT ID
nftInfo, err := NewTokenNftInfoQuery().
   SetNftID(nftID).
	 Execute(client)

//v2.1.16
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



