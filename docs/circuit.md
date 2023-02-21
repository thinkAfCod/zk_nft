# Circuit Design

Circuit file: [zkNFT.circom](https://github.com/kevinz917/zk-NFT/blob/main/circuits/zkNFT.circom)

This project's circom circuit implements the creation and trading of non-fungible tokens (NFTs) based on zero-knowledge proofs on a blockchain.

The entire circuit is divided into three templates: `mint`, `revealAttribute`, `and revealNFT`.

The `mint` template is used to create an NFT. It uses the LessEqThan comparator to check whether the sum of the inputted three attribute values is less than or equal to a given maximum value. If this condition is met, the attribute values are inputted into the `hashCharacter` template to calculate the hash value, and finally the hash value is outputted.

The `revealAttribute` template is used to reveal some attribute of a certain NFT, such as whether the first inputted attribute value is greater than or equal to a given minimum value. If this condition is met, the attribute values are inputted into the `hashCharacter` template to calculate the hash value, and finally the hash value is outputted.

The `revealNFT` template is used to reveal all attribute values of a certain NFT. The inputted three attribute values are inputted into the `hashCharacter` template to calculate the hash value, and finally the hash value is outputted.

In this circuit, the `hashCharacter` template uses `MiMCSponge` to calculate the hash value of the attribute values. In addition, the `LessEqThan` and `GreaterEqThan` comparators are used to check whether the attribute values meet the conditions.

Finally, use `component main = revealNFT()`to specify the template used. In constructing the mint and revealAttribute, you need to switch to the corresponding template, for example, `component main = mint(10)`, `component main = revealAttribute(3)`, etc.