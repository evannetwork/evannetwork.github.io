---
title: "Smart-Contracts"
---

# Smart Contracts

## What are Smart Contracts?
Smart contrcacts written for [Ethereum](https://ethereum.org/)<sup>[+]</sup> based blockchains are basically pieces of code that run in the blockchain. They can be described as objects (similiar to instances from object oriented programming languages like JavaScript, Python, C#, etc.) that run in the blockchain. Users can interact with them by using their functions and they can interact with each other if the interfaces are known.

Smart contracts can be written in different languages, the default contracts in the evan.network are written in [Solidity](http://solidity.readthedocs.io/en/latest/)<sup>[+]</sup>. You can find a list of other languages (including deprecated ones) [here](https://github.com/s-tikhomirov/smart-contract-languages#ethereum)<sup>[+]</sup>. All of these compile to Ethereum bytecode which is executed by the EVM (Ethereum virtual machine). And as contract interaction depends on their interfaces (how to "talk" with them) and their address (where their code is stored), they could be used interchangeably. But as high-level programming languages like Solidity offer useful features like inheritance, code parts that operate in an ecosystem with returning patterns, e.g. address lookup and event triggering, should be kept in the same language.

An example for a smart contract written in solidity can look like this:

```solidity
pragma solidity ^0.4.21;

contract Storage {
    string public data;
    
    function setData(string newData) public {
        data = newData;
    }
}
```

This contract defintion is like a class or prototype and be instantiated as often as desired. Every instance has its its own ```data``` member, that can be set or retrieved independently.


## Getting started with creating Smart Contracts
You can find good examples about getting started with smart contracts and Solidity on the [Ethereum](https://ethereum.org/)<sup>[+]</sup> homepage.

The recommendation in these samples is to use the Ethereum wallet for deploying the sample contracts, but if you want get started right away without synchronizing a the blockchain, you can use [Remix](https://remix.ethereum.org/)<sup>[+]</sup>. There you can run your code in the JavaScript VM or if you want to try interacting with contracts from the evan.network, install [MetaMask](https://metamask.io/)<sup>[+]</sup> and connect it to evan.network as described in [web3](/dev/web3#with-metamask).

