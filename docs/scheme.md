# <center> zk-NFT implemented with move contract

In this project, we plan to implement a simple zk-NFT and deploy and test it on the Sui blockchain.

The original project was written using the Hardhat framework and tested on Ethereum. The zkSNARK was implemented using circom and snarkjs, and the verification key was exported as a Solidity contract. Currently, the snarkjs tool does not support exporting to Move contracts, which is also a feature that we hope to expand in this project.

The following are links to the original project and related tools:

* [zk-NFT](https://github.com/kevinz917/zk-NFT)
* [circom](https://github.com/iden3/circom)
* [circomlib](https://github.com/iden3/circomlib)
* [snarkjs](https://github.com/iden3/snarkjs)


## zk-NFT

Here I present zk-NFT, a NFT powered by zkSNARKs that flips the concept of an NFT upside down. Normally, NFTs contain metadata that are fully revealed. Here, zk-NFT allows users to create and prove ownership of NFTs as well as their characteristics without revealing the full underlying metadata.

This would allow interesting universes to be built on top of the NFTs. For example, two pets, represented by NFTs and their hidden attributes, can engage in battle, but through ZK, can be orchestrated in a way such that the attributes are not fully revealed, but only the battle results are. In addition, this creates unseen dynamics in trading through a fog-of-war type interaction.

zkSNARKs written in Circom and Solidity.

## Example scenario

Here I propose a hypothetical game play involving fog-of-war type bids.

Suppose Alice plays a video game (powered by zk-NFT). First, the game asks Alice to create her character (mint the NFT). The character has three attributes: speed, agility, and endurance, and the total of these attributes cannot exceed 10.

Alice then creates her character and keeps these attributes private (off-chain) to herself and submits a hash of it onchain (committing the zk proof). After a few hours, many other players such as Bob also create their own unique characters.

As the game progressed, many have realize that characters with high speed and endurance values are currently useful, and Alice happens to have a character like that. However, because the information is hidden, others don't know. Seeing that her character is desirable, Alice decides to sell it.

In order to create speculation and movement in the market, Alice partially reveals (using SNARKs) that her character indeed has a speed attribute above 7, but doesn't reveal exactly the stat (realistically she should be able to reveal a combination of any proofs). This garners interest from buyers, and Bob decides to place a bid of 1 ETH. At the same time, Alice, without revealing the entire NFT, retains some leverage and information asymmetry.

Alice, seeing that Bob's bid is fair, accepts the bid and sells her character. When she accepts the bid, she hands over the right of the character, and is also bounded to simultaneously reveals all three attributes of her character. Bob is very happy - he knew that the speed attribute is higher than 7, and is pleased to find out that it's actually a 9, thinking he got a good deal. Alice, also thinks she got a decent deal, since the other attributes of her character, agility and endurance are low (but she didn't have to reveal them to Bob), and she suspects that in the future, the game will value characters with high agility stats, so she was happy to sell it off. She continues the buy cycle by trying to buy other unrevealed characters ...

## Basic functions

1. Minting. User first select attributes for their NFT in private with some constraint. In this prototype, it means selecting three attributes for your character, and the sum of the attributes has to be less than a max value. These attributes are then stored off-chain in a browser cache. To mint the NFT, the proof for minting is submitted which contains hidden values of attributes.

2. Revealing and Speculating. Trading is an integral part of any NFT ecosystem, but how would people trade if the information is hidden? Here, we use a partial reveal schema that allows users to first reveal a portion of their NFT's metadata without revealing the entire scheme, proven by zkSNARKs. For example, seller A wants to prove to buyer B that his NFT has an attribute of "speed" greater than 5 to encourage a purchase, but not specifying what that value is to retain leverage. This partial reveal schema provides the necessary speculation to engage buyers and sellers in a fog-of-war type interaction we haven't seen anywhere else in the NFT world.

3. Trading. In this version of the game, when a seller accepts a bid, they must reveal the full attributes of their NFT, effectively broadcasting it on-chain. It's possible to also swap the hidden attributes in off-chain ways. I'm currently exploring more trading variations!


