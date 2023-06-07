# Overview 
Zkshuffle provides easy access for Ethereum developers to create "mental poker" games utilizing zero-knowledge proofs. The concept of "mental poker" refers to the implementation of a fair gaming protocol over a communication system that doesn't require the involvement of any trusted third-party. The term was initially proposed in 1979 by Adi Shamir, Ron Rivest, and Leonard Adleman in a paper where they discussed the idea of creating a fair poker game in which players could not see each other's cards or shuffle and deal the cards themselves. The challenge of building a “mental poker” game is to ensure that no one can cheat while maintaining the communications reliable, efficient and low-cost.  As an implementation of Poseidon ZKP, zkshuffle emphasizes the reduction of gas cost on Ethereum. A more detailed description of the mechanism underlying  zkshuffle can be found via [zkShuffle: Mental Poker on SNARK for Ethereum](https://hackmd.io/xj--HI7sTl2T3fbK1NONtQ). “Mental poker” protocols can be applied beyond poker to many different types of games where secure, fair exchange of information is required without a trusted third party.<br>


# State Diagram
The following state diagram provides an overview of the game process managed by the  **ShuffleManager** contract. To initiate a new game, it must first be created. Upon creation, the manager contract assigns a unique ID to this game and players can join the game with that ID. Once the final player has registered, the game starts. Players can check the current turn within the game. If it's their turn to perform an action (shuffle, deal or open), they carry out the action accordingly.
![Image text](https://github.com/matelanbo/git-test/blob/main/SimpleStateDiagram.svg)

# Main Components

## Circuits 
This directory contains circom code to implement encryption and decryption for the zk poker game. It also contains the corresponding verifier contracts generated with **snarkjs**. [View the Code](https://github.com/Poseidon-ZKP/Poseidon-ZKP/tree/main/packages/circuits)
## Shuffle Contracts
This directory contains contracts that implement management of the zk poker game. It comprises the central management contract, **ShuffleManager.sol**, as well as supplementary contracts tasked with operations such as encryption and decryption. The manager contract is responsible for creating new games, registering players, checking game states, and performing various operations required for game management. [View the Code](https://github.com/Poseidon-ZKP/Poseidon-ZKP/tree/main/packages/contracts/contracts/shuffle)
## Game Contracts
A game logic contract is needed in order to construct a complete game. You may create your own game logic contract and here we provide a simple [example](https://github.com/Poseidon-ZKP/zkShuffle/tree/main/packages/contracts/contracts/games). 



