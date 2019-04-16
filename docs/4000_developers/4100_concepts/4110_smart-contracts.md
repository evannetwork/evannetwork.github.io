---
title: "Smart-Contracts"
parent: Developers
grand_parent: Concepts
nav_order: 4110
permalink: /docs/developers/smart-contracts.html
---

# Smart Contracts

Smart Contracts are a central piece of technology in the evan.network. Their task is not only to implement trusted user applications; the same basis of trust is utilized to implement central infrastructures for the evan.network itself.

## What are Smart Contracts?
Smart Contracts written for [Ethereum](https://ethereum.org/) based blockchains are basically pieces of code that run in the blockchain. They can be described as objects (similiar to instances from object oriented programming languages like JavaScript, Python, C#, etc.) that run in the blockchain. Users can interact with them by using their functions and they can interact with each other if the interfaces are known.

Smart Contracts can be written in different languages, the default contracts in the evan.network are written in [Solidity](http://solidity.readthedocs.io/en/latest/). You can find a list of other languages (including deprecated ones) [here](https://github.com/s-tikhomirov/smart-contract-languages#ethereum). All of these compile to Ethereum bytecode, which is executed by the EVM (Ethereum Virtual Machine). And as contract interaction depends on their interfaces (how to 'talk' with them) and their address (where their code is stored), they could be used interchangeably. But as high-level programming languages like Solidity offer useful features like inheritance, code parts that operate in an ecosystem with returning patterns, e.g. address lookup and event triggering, should be kept in the same language.

An example for a Smart Contract written in solidity can look like this:

```solidity
pragma solidity ^0.4.21;

contract Storage {
    string public data;

    function setData(string newData) public {
        data = newData;
    }
}
```

This contract definition is like a class or prototype and can be instantiated as often as desired. Every instance has its own ```data``` member that can be set or retrieved independently.


## Getting started with creating Smart Contracts
You can find good examples on how to get started with Smart Contracts and Solidity on the [Ethereum](https://ethereum.org/) homepage.

The recommendation in these samples is to use the Ethereum wallet for deploying the sample contracts, but if you want to start right away without synchronizing to the blockchain, you can use [Remix](https://remix.ethereum.org/). There, you can run your code in the JavaScript VM or, in case you want to try interacting with contracts from the evan.network, install [MetaMask](https://metamask.io/) and connect it to evan.network as described in [Web3](https://github.com/ethereum/web3.js). Alternatively, use the [evan.prompt](/docs/developers/tooling/evan.prompt.html) to compile and upload your contracts to evan.network.
