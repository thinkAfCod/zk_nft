# Contracts Design

This project includes the following contract files:

1. [NFT.sol](https://github.com/kevinz917/zk-NFT/blob/main/contracts/NFT.sol)

2. [mintProof.sol](https://github.com/kevinz917/zk-NFT/blob/main/contracts/mintProof.sol)

3. [partialRevealProof.sol](https://github.com/kevinz917/zk-NFT/blob/main/contracts/partialRevealProof.sol)

4. [revealProof.sol](https://github.com/kevinz917/zk-NFT/blob/main/contracts/revealProof.sol)

The last three contracts, `mintProof.sol`, `partialRevealProof.sol`, and `revealProof.sol`, were exported using the snarkjs tool and correspond to the verification of `mint proof`, `revealAttribute proof`, and `revealNFT proof`, respectively.

The core contract file is `NFT.sol`. This is a Solidity smart contract that implements ERC721 and includes the OpenZeppelin ERC721Enumerable and Ownable contracts, as well as the three verification contracts mentioned above: `partialRevealProof`, `mintProof`, and `revealProof`.

The contract creates a contract named `ZKNFT`. It implements `ERC721Enumerable` and `Ownable` contracts and therefore has the same functionality and behavior as those contracts provide. In addition, the contract defines a structure named character, which represents the attributes and other state data of the NFT.

The contract also defines the following functions:

* `mint` - creates a new NFT, for which the user needs to provide some private inputs to prove that they satisfy certain conditions. When these inputs are verified, a new NFT is created for the user and ownership is transferred to the user.
* `reveal` - reveals all the attributes of an NFT. This can only be done by the owner of the NFT. Once executed, the NFT will be marked as exposed and all its attributes will be recorded in the contract state.

* `partialReveal1` - partially reveals attributes. This allows the owner to selectively reveal some of the attributes of their NFT (e.g., attribute1 > 3). The attributes that are partially revealed will be recorded in the contract state, but the unrevealed attributes will remain private.
createBid - bids on an NFT.

* `acceptBid` - accepts a bid. If the owner of the NFT is the initial owner, they must reveal both the NFT and the bid. Otherwise, only the ownership of the NFT needs to be transferred to the buyer.

* `withdraw` - withdraws all funds from the contract.

**Note that functions such as `mint`, `reveal`, and `partialReveal1` require proof verification before executing the corresponding logic.**

Finally, the contract also defines several mappings and events for tracking state and triggering events.