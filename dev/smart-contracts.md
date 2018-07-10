---
title: "Smart-Contracts"
---

# Smart Contracts

Smart Contracts are a central piece of technology in the evan.network. Not only to implement trusted user applications; that same basis of trust is utilized to implement central infrastructure for evan.network itself

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

The recommendation in these samples is to use the Ethereum wallet for deploying the sample contracts, but if you want get started right away without synchronizing a the blockchain, you can use [Remix](https://remix.ethereum.org/)<sup>[+]</sup>. There you can run your code in the JavaScript VM or if you want to try interacting with contracts from the evan.network, install [MetaMask](https://metamask.io/)<sup>[+]</sup> and connect it to evan.network as described in [web3](/dev/web3#with-metamask). Or use the [](/dev/evan.prompt) to compile and upload your contracts to evan.network.

# Smart Contracts in evan.network

## Base Contract

## DataContract
The DataContract is secured data storage contract for single properties and lists.

It relies on the [Hybrid Storage](/dev/ipfs#hybrid-storage) concept for data storage and secures its data via contract permissions, sharings and key management described in [Security](/dev/security).

[![data contract](/public/dev/data_contract.png){:max-width="50%"}](/public/dev/data_contract.png)

The DataContract allows to:
- set/update properties
- add/remove list entries
- move entries between lists
- update the contract state (set it to Draft, Active, etc.) that follows a preconfigured workflow
- update consumer states (set it to Draft, Active, etc.) that follows a preconfigured workflow


### Configuring DataContracts
If created on its own, DataContracts cannot do very much. They rely on their authority to check which entries or lists can be used. Basically every imaginable entry name or list name can be used, but before actual data can be stored in it, permissions to do so have to be granted.

Its authority is an instance of the contract `DSRolesPerContract` and created alongside the DataContract, when the factory is called.

Functions are secured in the following manner:
- the contract functions have to be unlocked for each role that should be allowed to use it,
  so if the role "member" wants to add entries to *any* list, this role needs permissions to use the ```addListEntries``` function
- for each property, that should be manipulated, an operation permission for this entry or list has to be granted
- state changes (contract and consumer states) require permissions for a combination of
  + a role that updates the state
  + the current state
  + the target state
- this means that for example a contract member may set the state from the current state "Active" to the state "PendingApproval", and only the owner may set it from "PendingApproval" to "Terminated"

## Profile

## Mailbox

## Rights and Roles

## Business Center
Business Centers are communities for working together on specific topics. They group together accounts and contracts and set a context for the work on the contracts. These contexts may be companies, projects or common interests.

Depending on the setup of the business center users may
- join on their own
- be invited to join
- be added by anyone that is already a member

Users may join as many Business Centers they like and they all are independent working spaces with their own scope and data. Their [ÐAPPs](/dev/dapps) are similar to dashboards and members can start working on contracts in the current business center or create new contracts in it.

Accounts can create a Business Center scoped profile, which is similar to a business card for that context. In it users may provide data for other members to find them and start working together or share their qualifications or certificates with the Business Center community.

## Event Hub
The event hub is a smart contract deployed at `events.evan`, which is used by many contracts in the evan.network ecosystem for announcing status updates. Contracts that use the event hub include but are not limited to:
- [Business Center](/dev/smart-contracts#business-center)
- [Mailbox](/tutorial/mailbox)
- [Data Contract](/dev/smart-contracts#data-contract)

It is a central contract, which other contracts locate via ENS lookup. The `EventHub` contract inherits from multiple base contracts which add events and event trigger functions to its functionality. Every contract, that uses the event hub, knows only a limited scope of its functions due to only knowing the event hub base class related to itself -e.g. the `MailBox` contract only knows the base class `EventHubMailBox` and can only trigger events for those.

![Event Hub inheritance](/public/dev/eventhub_inheritance.png)

## Contract Factories
### About
Some contracts, like the [DataContract](/dev/data-contract) require a few more steps to be set up during their creation. These steps may depend on each other, so a user creating these contracts would have to wait for the single steps to be completed before being able to work with the contract.

These contracts are created by using contract factories, which offers a few enhancements to the process:
- the overall process is faster - instead of n single transactions only one transaction is performed
- creating contracts becomes cheaper -  overhead is reduced when performed in a single transaction
- it can become safer - if one of the setup steps that follow the contract creation fails, the entire creation process is rolled back and if executed via the evan API, this transaction will not be started (gas is estimated before each transaction and a failing transaction would be detected and prevented)
- factories are deployed to [ENS](/dev/ens) addresses and can be updated without delivering code to each client application


### Usage
#### ENS Address
Contract factories that belong to a [Business Center](/dev/business-center) are usually deployed at `${FACTORY_NAME}.factory.${BUSINESS_CENTER_ADDRESS}`, so a factory for tasks in the business center "sample.evan" would be deployed at "tasks.factory.sample.evan".

#### Factories and BusinessCenters
If a factory is supposed to create contracts for a [Business Center](/dev/business-center), it has to be registered as a valid factory in that Business Center. Factories register all new contracts they create in the Business Center they belong to, and to be able to do so, they need to be registered at the Business Center as a valid factory.

#### Getting Addresses of new Contracts
When creating a contract via factory the address is returned via an event from the factory, so when creating new contracts with factories, an event listener, that watches for those events has to be created beforehand.

