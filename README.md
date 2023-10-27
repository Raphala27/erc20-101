# ERC20 101
Elias 
## Introduction

Welcome! This is an automated workshop that will explain how to deploy and ERC20 token, and customize it to perform specific functions.
It is aimed at developpers that have never written code in Solidity, but who understand its syntax.

## How to work on this TD

### Introduction

The TD has two components:

- An ERC20 token, ticker TD-ERC20-101, that is used to keep track of points
- An evaluator contract, that is able to mint and distribute TD-ERC20-101 points

Your objective is to gather as many TD-ERC20-101 points as possible. Please note :

- The 'transfer' function of TD-ERC20-101 has been disabled to encourage you to finish the TD with only one address
- You can answer the various questions of this workshop with different ERC20 contracts. However, an evaluated address has only one evaluated ERC20 contract at a time. To change the evaluated ERC20 contract associated with your address, call `submitExercice()` with that specific address.
- In order to receive points, you will have to do execute code in `Evaluator.sol` such that the function `TDERC20.distributeTokens(msg.sender, n);` is triggered, and distributes n points.
- This repo contains an interface `IExerciceSolution.sol`. Your ERC20 contract will have to conform to this interface in order to validate the exercice; that is, your contract needs to implement all the functions described in `IExerciceSolution.sol`.
- A high level description of what is expected for each exercice is in this readme. A low level description of what is expected can be inferred by reading the code in `Evaluator.sol`.
- The Evaluator contract sometimes needs to make payments to buy your tokens. Make sure he has enough ETH to do so! If not, you can send ETH directly to the contract.

### Getting to work

- Clone the repo on your machine
- Install the dependencies. Deps in Foudry are git submodules, you have to run `git submodule init` and `git submodule update`.
- Register for an infura API key
- Create a `.env` file that contains private key for deployment, an infura API key.
- To deploy a contract, configure a script in the [scripts folder](script). Look at the way the TD is deployed and try to iterate
- Test your deployment locallly with `anvil` and `forge script script/your-script.s.sol --fork-url http://localhost:8545 --broadcast -vvvv`
- Deploy on Sepolia `forge script script/deployTD.s.sol --rpc-url $sepolia_url --broadcast -vvvv `

## Points list

### Setting up

- Create a git repository and share it with the teacher
- Install Foundry and create an empty Foundry project (2 pts). Create an infura API key to be able to deploy to the Sepolia testnet
  These points will be attributed manually if you do not manage to have your contract interact with the evaluator, or automatically in the first question.

### ERC20 basics

- Call `ex1_getTickerAndSupply()` in the evaluator contract to receive a random ticker for your ERC20 token, as well as an initial token supply (1 pt). You can read your assigned ticker and supply in `Evaluator.sol` by calling getters `readTicker()` and `readSupply()`
- Create an ERC20 token contract with the proper ticker and supply (2 pt)
- Deploy it to the Sepolia testnet (1 pts)
- Call `submitExercice()` in the Evaluator to configure the contract you want evaluated (Previous 5 points are attributed at that step)
- Call `ex2_testErc20TickerAndSupply()` in the evaluator to receive your points (2 pts)

### Distributing and selling tokens

- Create a `getToken()` function in your contract, deploy it, and call the `ex3_testGetToken()` function that distributes token to the caller (2 pts).
- Create a `buyToken()` function in your contract, deploy it, and call the `ex4_testBuyToken()` function that lets the caller send an arbitrary amount of ETH, and distributes a proportionate amount of token (2 pts).

### Creating an ICO allow list

- Create a customer allow listing function. Only allow listed users should be able to call `getToken()`
- Call `ex5_testDenyListing()` in the evaluator to show he can't buy tokens using `buyTokens()` (1 pt)
- Allow the evaluator to buy tokens
- Call `ex6_testAllowListing()`in the evaluator to show he can now buy tokens `buyTokens()` (2 pt)

### Creating multi tier allow list

- Create a customer multi tier listing function. Only allow listed users should be able to call `buyToken()`; and customers should receive a different amount of token based on their level
- Call `ex7_testDenyListing()` in the evaluator to show he can't buy tokens using `buyTokens()` (1 pt)
- Add the evaluator in the first tier. He should now be able to buy N tokens for Y amount of ETH
- Call `ex8_testTier1Listing()` in the evaluator to show he can now buy tokens(2 pt)
- Add the evaluator in the second tier. He should now be able to buy 2N tokens for Y amount of ETH
- Call `ex9_testTier2Listing()` in the evaluator to show he can now buy more tokens(2 pt)

### All in one

- Finish all the workshop in a single transaction! Write a contract that implements a function called `completeWorkshop()` when called. Call `ex10_allInOne()` from this contract. All points are credited to the validating contract (2pt)

### Extra points

Extra points if you find bugs / corrections this TD can benefit from, and submit a PR to make it better. Ideas:

- Adding a way to check the code of a specific contract was only used once (no copying)

## TD addresses

- ERC20TD [`0xa62463D928143452D23F5C92853397648380c2e5`](https://sepolia.etherscan.io/address/0xa62463D928143452D23F5C92853397648380c2e5)
- Evaluator [`0x95583e7C50Fba579D2Ad18a30C31D2B881B9B3AF`](https://sepolia.etherscan.io/address/0x95583e7C50Fba579D2Ad18a30C31D2B881B9B3AF)
