---
title: "DBCP"
---
# DBCP

## About the Protocol
DBCP is a formalized description of how to interact with (Ethereum) Smart Contracts. This makes a Smart Contract almost a single point of contact for interacting with Ethereum based blockchains.

Developers, that write applications for Smart Contracts, need at least the contract address and the ABI for writing code, that interacts with the contract. Some details about the Smart Contract and contact addresses can be helpful as well.

Users that want to use such a ÐAPP for interacting with the Smart Contract on the other hand need to know either were to find the ÐAPP and most probably want some information about the ÐAPP before they actually run in with their accounts.

The DBCP protocol faces those needs and provides a comprehensive description of contracts, their ÐAPPs or even contractless ÐAPPs. Developers can write own applications for interacting with the Smart Contract or can show details about contracts in their own ÐAPP and offer links to the contracts own ÐAPP.

Because DBCP descriptions can be stored directly at the contract itself, contracts can become standalone applications, that can be used on their own or easily included in existing applications.

This description includes technical details to enable developers to write applications that interact with this contract and/or a distributed app (ÐApp), that can be used with a web browser.


## Description and Contract Updates
As contracts may change over time, descriptions aren't set in stone as well. Updates in smart contracts can be reflected the description as well, this includes but is not limited to:
- updates in the contracts metadata, like name, description, i18n, icon, etc.
- updates in the contracts data schema (e.g. new/deleted/changed entries, lists, properties, ...)
- updates to the contracts abi, e.g.
  - make existing properties in contract public
  - update a related contracts abi

If a contract has a ÐApp for interacting with it, this ÐApp can be updated without touching the contract description at all. This behavior can be controlled by specifying the desired version range in the `dependencies` property in `dapp`, allowing to use or ignore latest features and/or bugfixes, basically allowing to use a "snapshotted" version of a ÐApp for all time.
This decision can be changed later on by updating the contract description as well.

If a description has been set to an ENS address, the same properties can be updated as well and even the contract can be updated, as this is stored at the ENS address. This allows full data and usage flexibility and provides a generic interaction schema the same time as well.


## Get in contact
Join the community at the [DBCP Community Webpage](https://dbcp.online/)<sup>[+]</sup> (German).


## Get started with DBCP
Have a look at the DBCP library GitHub [project page](https://github.com/evannetwork/dbcp)<sup>[+]</sup>.
