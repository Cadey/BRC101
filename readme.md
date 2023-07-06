\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
**Working Draft!**
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*


# Hashed NFTS - BRC101

**BRC101 - A BitCoin Ordinal NFT standard proposal**

Many of you reading this will love the idea of NFTs on BitCoin, many others will disagree. The fact is however, the genie is out of the bottle, so lets make a solution that all parties can be OK with.

## What should an NFT be?
At there core, NFTs are proofs of ownership, of something, **anything**, nothing more. 

The data within an NFT needs to include only the information to answer some basic questions ***Who***, ***What***, ***Where***, ***How***

 - Who issued the NFT
 - What is the content of the NFT
 - Where can the content be located
 - How can we verify the issuer and establish trust
 - How can the content be validated

## What is the problem with NFTs on BitCoin today?
As of today (6th July 2023) NFTs are being inscribed directly onto the blockchain, this however isnt the best way to do it. When you inscribe the NFT content directly into the blockchain you are creating problems down the road, problems which might not seem important today, but they will be.

BitCoin is supposed to be optimal, with small amounts of data. This allows for nodes to have the smallest hardware requirements possible. Inscriptions with full NFT content on, unfortunately, breaks this.

This could make the miners happy, but think about the added cost to every other node on the network. Who pays for that additional space to run a node? The logical conclusion is, BitCoin has **less** nodes!

## So why are NFTs contents being inscribed?
While its true, the best way to ensure the entire content of an NFT is never changed or lost is to put it into a blockchain, the blockchain isnt a database. Its a history of transactions.

Other implementations of NFTs use off-chain storage for the content, usually using IPFS. While this solution is OK, its not as perfect as people would like to think. IPFS is decentralized, to the point that you can mirror (pin) all the content if you wish, but as this content grows (which is is) the costs start to ramp up. Now only "some" of the data will be pinned....


## BRC101 - Hashed NFTS
Since an NFT can be ***anything***, we need a standard which can represent more than just art. To do this, BRC101 uses a two step minting process. Collection creation, Asset creation.


### Collection creation
To create a collection, we need to inscribe what our collection of NFTs are. What defines what a collection is can be unique and is relevant only to the issuer and buyer relationship.

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

### NFT creation
Each NFT created in a collection references back to the **nftHashCol** by means of ordinal Id, this helps to keep the trust intact.

The NFT data then only contains enough information On-Chain to keep record of the NFT and its original content.

> BRC101 makes a distinction between "Content" and "MetaData". Metadata is optional, however if metadata is included, the content hash and content type should be represent the content the metadata is pointing to. The metadata type will always be interpreted as a text

``` 
{
	"p": "nftHashItem",
	"v": 1,
	"cH": "98a2141d88e0a940e9ca21aa8290273998f066d9f4a845c1518d1d276735829eddfd87c13b77495cdcd5baaee8427936df2f7c5f17506656e844b3a082b8a89c",
	"mH": "98a2141d88e0a940e9ca21aa8290273998f066d9f4a845c1518d1d276735829eddfd87c13b77495cdcd5baaee8427936df2f7c5f17506656e844b3a082b8a89c",
	"n": "Super dooper cool NFT",
	"l": "aaaaYwvVtjNFKRqHEWPChdkfM24Z1i34FmmC4uAjDdnJ7NF/338.json",
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



#### Establishing trust!
The most important problem to solve with an NFT is establishing its authenticity, who created it, how can we verify this to be true?

This, realistically is different for each collection, and i cant be done "on-chain". Lets take an example, when you buy an NFT of a cat image, how do you know its the genuine cat image?  

- Do you **trust** the marketplace you purchased it from?
- Do you **trust** a twitter profile?
- What do you **trust**??

So lets go back to the basics, when you have an NFT, chances are you know somthing about the issuer. They could be a company, a person, a charity... The point is, they are **something** and they should be the ones telling you its genuine. 

For this reason, the On-Chain NFT needs to reference an Off-Chain means to authenticate it. If that company goes bust, or the person dies. There will be other ways to recover this authenticity, humans are actually quite good at this. TheWayBackMachine, good old official records, etc etc. Issuers can establish any number of ways to keep the trust relationship alive!

> Some people will of course you could point to some other blockchains which use oracles to confirm a truth, but what happens when that chain no longer exists....