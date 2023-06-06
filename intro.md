# Overview 
Zkshuffle provides easy access for Ethereum developers to create "mental poker" games utilizing zero-knowledge proofs. The concept of "mental poker" refers to the implementation of a fair gaming protocol over a communication system that doesn't require the involvement of any trusted third-party. The term was initially proposed in 1979 by Adi Shamir, Ron Rivest, and Leonard Adleman in a paper where they discussed the idea of creating a fair poker game in which players could not see each other's cards or shuffle and deal the cards themselves. The challenge of building a “mental poker” game is to ensure that no one can cheat while maintaining the communications reliable, efficient and low-cost.  As an implementation of Poseidon ZKP, zkshuffle emphasizes the reduction of gas cost on Ethereum. A more detailed description of the mechanism underlying  zkshuffle can be found via [zkShuffle: Mental Poker on SNARK for Ethereum](https://hackmd.io/xj--HI7sTl2T3fbK1NONtQ). “Mental poker” protocols can be applied beyond poker to many different types of games where secure, fair exchange of information is required without a trusted third party.<br>
# State Diagram
The state diagram below illustrates the full process of a game managed by the **ShuffleManager** contract. Please be aware that this diagram is a full descrption of the state changing in the contract, while most intermediate processes like encryption have encapsulated into **zkshuffle** library. SDK users will not implement those intermediate steps themself(see examples).

To get started, a new game needs to be created with supported size. After game creation, the manager contract will generate a unique ID for that game and enters registration state. In this state, the manager contract will allow players to join in untill all the spots are filled. Player registering needs to provide valid public key, and all keys will be aggregated to an aggregated public key. After the last player joined, the manager contract will switch the game to shuffle state. In this state, each play will correctly shuffle and encrpyt the cards. After the last player shuffled, the manager contract will switch the game to cards dealing state. In this state, players will dealt cards and the decrypted cards will be updated.
![Image text](https://github.com/matelanbo/git-test/blob/main/stateDiagram.svg)
# Installation
## Prerequisite

**Setup Yarn v2 to enable workspace feature**
> Note: you need to migrate to Yarn v2 if not already, guide [here](https://yarnpkg.com/getting-started/migration). 
Follow the [Yarn official instruction](https://yarnpkg.com/getting-started/install)
`npm i -g corepack`
`corepack prepare yarn@stable --activate`
`yarn plugin import workspace-tools`
Now we can use yarn workspace commands, [more info](https://yarnpkg.com/cli/workspace)

**Install**

`yarn`

After installation, the dependencies of all the packages will be installed.

**Compile all packages**

`yarn workspaces foreach run compile`

**Test all packages**

`yarn workspaces foreach run test`

## Packages

**`💡 @poseidon-zkp/poseidon-zk-circuits`**

This package contains all the Circom circuit components with related unit test cases. Circuit integrators can directly import the circuits in this package.

**Install**

`yarn install @poseidon-zkp/poseidon-zk-circuits`

If you want to develop based on this package, it's highly recommended to change the default `ptau` setting in `hardhat.config.ts` to your own generated trust setup.

**Compile**

`yarn compile`

Compile circuits only

`yarn compile:circuits`

Compile generated contracts only:

`yarn compile:contracts`

After running compilation, zkey files, wasm files, verifier Solidity contracts will be generated, and can be imported by JavaScript users and contract users.

**Testing**

`yarn test`

**`⛓ @poseidon-zkp/poseidon-zk-contracts`**

This package depends on circuit package and its generated verifier contracts. It extends the contract of verifier contracts and can be integrated by user-end developers.

**Install**

`yarn install @poseidon-zkp/poseidon-zk-contracts`

**Compile**

`yarn compile`

**Testing**

`yarn test`

The unit tests in contracts package use proof generation utilities from `proof` package and perform some e2e tests.

**Deploy**

`yarn deploy`

**`🛠 @poseidon-zkp/poseidon-zk-jssdk`**

**Install**

`yarn install @poseidon-zkp/poseidon-zk-jssdk`

todo

**`🧾 @poseidon-zkp/poseidon-zk-proof`**

This package provides some utilities for generating zk proofs and is depended by contracts package to do some unit tests.

**Install**

`yarn install @poseidon-zkp/poseidon-zk-proof`

**Compile**

`yarn compile`
# Examples
Here we show examples of interacting with a deployed game mananger contract using **zkshuffle**. A full totuorial can be found via ![totuorial]()
- To create a zkShuffle instance with a given shuffleManager contract address and a player's signer

  ```ts
      const player = await zkShuffle.create(ShuffleManagerContract, signer)
  ```

- To join a game with specified gameID
  ```ts
      const playerIdx = await player.joinGame(gameId)
  ```

- To check player's turn in this game
  ```ts
      const turn = await player.checkTurn(gameId)
  ```

- If it's player's shuffle turn, shuffle the card
  ```ts
      await player.shuffle(gameId)
  ```

- If it's player's deal turn, draw the card
  ```ts
      await player.draw(gameId)
  ```

- If it's player's open turn, open the card
  ```ts
      const cards[] = await player.open(gameId, cardIds)
# Main Components

## Circuits 
[View the Code Here](https://github.com/Poseidon-ZKP/Poseidon-ZKP/tree/main/packages/circuits)
This directory contains circom code to implement encryption and decryption of the zk poker shuffle. It also contains the corresponding verifier contracts generated with **snarkjs**
## Shuffle Contracts
[View the Code Here](https://github.com/Poseidon-ZKP/Poseidon-ZKP/tree/main/packages/contracts/contracts/shuffle)
This folder contains contracts that implement poker shuffle.
### ShuffleManager.sol
[View the Source Code Here](https://github.com/Poseidon-ZKP/Poseidon-ZKP/blob/main/ShuffleManager.sol)
This contract is designed to manage zk shuffle games. It's responsible for creating new games, registering players, checking game states, and performing various operations required for game management.

## List of other contracts?


