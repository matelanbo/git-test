Overview
Zkshuffle provides easy access for Ethereum developers to create "mental poker" games utilizing zero-knowledge proofs. The concept of "mental poker" refers to the implementation of a fair gaming protocol over a communication system that doesn't require the involvement of any trusted third-party. The term was initially proposed in 1979 by Adi Shamir, Ron Rivest, and Leonard Adleman in a paper where they discussed the idea of creating a fair poker game in which players could not see each other's cards or shuffle and deal the cards themselves. The challenge of building a “mental poker” game is to ensure that no one can cheat while maintaining the communications reliable, efficient and low-cost.  As an implementation of Poseidon ZKP, zkshuffle emphasizes the reduction of gas cost on Ethereum. A more detailed description of the mechanism underlying  zkshuffle can be found via zkShuffle: Mental Poker on SNARK for Ethereum - HackMD. “Mental poker” protocols can be applied beyond poker to many different types of games where secure, fair exchange of information is required without a trusted third party.

Main components 
Circuits 
Poseidon-ZKP/packages/circuits at main · Poseidon-ZKP/Poseidon-ZKP · GitHub
This folder contains circom code to implement encryption and decryption of the zk poker shuffle. It also contains the corresponding verifier contracts generated with snarkjs
Shuffle Contracts
Poseidon-ZKP/packages/contracts/contracts/shuffle at main · Poseidon-ZKP/Poseidon-ZKP · GitHub
This folder contains contracts that implement poker shuffle.
ShuffleManager.sol
(source code Poseidon-ZKP/ShuffleManager.sol at main · Poseidon-ZKP/Poseidon-ZKP · GitHub)
This contract is designed to manage zk shuffle games. It's responsible for creating new games, registering players, checking game states, and performing various operations required for game management.

List of other contracts?
