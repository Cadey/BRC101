
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
**Working Draft!**
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*


# Hashed NFTS - BRC101

**BRC101: The Bitcoin NFT Standard Proposal We Need**

Imagine the possibility of bringing Non-Fungible Tokens (NFTs) to Bitcoin - a revolution in its own right that is loved by some, and questioned by others. As this concept has already taken flight, we aim to create a system that caters to every stakeholder's interest.

## What should an NFT be?

NFTs are essentially digital certificates of ownership. They can be linked to anything, or nothing at all. What's crucial is the data they carry, which should be able to answer basic questions such as:

 - Who issued the NFT
 - What is the NFT's content?
 - Where is the content located?
 - How do we verify the issuer and trustworthiness of the NFT?
 - How do we validate the content of the NFT?

## What is the problem with NFTs on BitCoin today?

Currently, as of 6th July 2023, NFTs on Bitcoin have a fundamental issue. They are being engraved directly onto the blockchain, which is far from optimal. Yes, recording the NFT content directly into the blockchain ensures its permanency, but it also sets us up for future complications.

Bitcoin is designed to be efficient, dealing in small amounts of data. This design ensures that even the most basic hardware can run a node. But storing full NFT content on Bitcoin is like trying to fit a square peg into a round hole; it just doesn't work. It increases the requirements for every node, which, in turn, may result in fewer nodes due to the elevated costs. Although miners might welcome this, the potential trade-off is a less robust network.

## Why not inscribe NFT contents directly?

Many people ask: why not inscribe NFT contents directly? The answer is that while a blockchain is reliable and immutable, it's not a database. It is essentially a record of transactions.

Most NFTs use off-chain storage, like IPFS, for their content. Although it's a decent solution, it's not perfect. IPFS is so decentralized that you can mirror (or "pin") all the content, but as this data grows, the costs start escalating. This leads to only a fraction of the data being pinned.

In conclusion, while NFTs on Bitcoin represent a promising concept, the implementation needs careful consideration. Optimizing storage, keeping costs low, and maintaining the integrity of the network are challenges that need to be addressed for a harmonious incorporation of NFTs into Bitcoin's landscape.


## BRC101 - Hashed NFTS
Given the all-encompassing nature of NFTs - their ability to represent any conceivable thing - we require a standard that expands beyond the confines of art. BRC101 addresses this need through an innovative two-step minting process: Collection Creation and Asset Creation.


### Collection creation: The first step
In the journey of minting NFTs, the initial step is to establish a collection. This is where we define what our suite of NFTs will represent. The concept of a 'collection' is flexible and unique, shaped by the relationship and agreement between the issuer and the buyer.

```
{
	"p": "nftHashCol",
	"v": 1,
	"n" : "Super dooper collection",
	"d" : "superDooper.com",
	"v" : "dns"
}
```
| Property	| Description | type |
| :--- | :--- | :--- |
| p | Ordinal protocol | string|
| v | Protocol version | number |
| n | Collection name | string |
| d | Issuer domain | string |
| v | Issuer validation type | "dns" \| "http" |

> When using DNS validation and TXT record with the ordinal ID as a value should be returned.
> When using HTTP a .well-known/Ordinal/Collection.[OrdinalCollectionId].ord should return a 200.

### NFT creation

Each NFT minted in a collection refers back to the nftHashCol by leveraging an ordinal ID. This structure not only enhances the system's efficiency but also solidifies the element of trust.

As such, the data incorporated within the NFT on-chain only contains the necessary information to maintain the record of the NFT and its original content. It is a method that values both trust and efficiency.

> Under BRC101, there's a clear delineation between 'Content' and 'Metadata'. While the inclusion of metadata is optional, it plays a vital role when included. If metadata is part of an NFT, the content hash and content type should accurately represent the content to which the metadata is pointing. The type of metadata, in this scenario, is always interpreted as text. It’s a framework that values precision and clarity, ensuring that NFTs are accurately represented and recorded.

``` 
{
	"p": "nftHashItem",
	"v": 1,
	"cH": "98a2...",
	"mH": "45c4...",
	"n": "Super dooper cool NFT",
	"l": "aaaaYwv...",
	"lT" : "ipfs"
	"t": "image/jpeg",
	"cId" : 3423432432
}
```
| Property	| Description | type |
| :--- | :--- | :--- |
| p | Ordinal protocol | string|
| v | Protocol version | number |
| cH | Hash of the NFTs content | Sha512 Hash |
| mH | Hash of the NFTs metadata | Sha512 Hash |
| n | Name of the NFT | string |
| l| location of the content | string |
| lT | location type | "ipfs" \| "http" |
| t | Content type | string |
| cId | Collection ordinal ID | string |



#### Authenticating NFTs: The Trust Quandary and BRC101's Solution

One of the most pressing challenges with NFTs is determining their authenticity – who created them, and how can we verify this?

In reality, the verification process may differ for each collection, and it can't be fully executed on-chain. Take for instance, you buy an NFT linked to a cat image. How can you ascertain its authenticity?

- Is it the **trust** you place in the marketplace you purchased it from?
- Is it **trust** in a corresponding Twitter profile?
- Or is it something else entirely that you **trust**?

In essence, let's circle back to fundamentals. If you own an NFT, it's likely you have some information about its issuer – be it a company, an individual, or a charity. These entities have a presence, an identity, and they should be the ones validating the NFT's authenticity.

That's why under BRC101, the On-Chain NFT references an Off-Chain method for authentication. If a company goes under or an individual passes away, there are still means to validate the NFT's authenticity. Humanity excels in preserving and retrieving information - be it through TheWayBackMachine, official records, or other means. Issuers can create numerous ways to sustain the trust relationship!

Some may argue that other blockchains use oracles to verify truth. However, the question remains, what happens when that blockchain ceases to exist? BRC101 offers a robust, flexible solution that doesn't rely solely on one system for verification, making it a resilient choice in the dynamic world of NFTs.