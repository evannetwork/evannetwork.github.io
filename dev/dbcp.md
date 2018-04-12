---
title: "DBCP"
---

# DBCP 
## About
DBCP is a formalized description of how to interact with (Ethereum) smart contracts. This makes a smart contract almost a single point of contact for interacting with Ethereum based blockchains.

Developers, that write applications for smart contracts, need at least the contract address and the ABI for writing code, that interacts with the contract. Some details about the Smart Contract and contact addresses can be helpful as well.

Users, that want to use such a ÐAPP for interacting with the smart contract on the other hand, need to know either were to find the ÐAPP and most probably want some information about the ÐAPP before they actually run in with their accounts.

The DBCP protocol faces those needs and provides a comprehensive description of contracts, their ÐAPPs or even contractless ÐAPPs. Developers can write own applications for interacting with the smart contract or can show details about contracts in their own ÐAPP and offer links to the contracts own ÐAPP.

Because DBCP descriptions can be stored directly at the contract itself, contracts can become standalone applications, that be used on their own or easily included in existing applications.

This description includes technical details to enable developers to write applications that interact with this contract and/or a distributed app (ÐApp), that can be used with a web browser.


## Structure
The DBCP description is saved as a JSON file, which is stored is a distributed file system (IPFS). Files stored in the distributed file system can be retrieved via their hashes and this hash is stored at the smart contract. Further dependencies are resolved in the same manner. Description files for subcomponents are pulled from distributed file system as well and so on.

This description resembles a package.json known from NodeJS modules in its functionality.

The following information can be included in the description file:

  - basic information about the contract, for example:
    - name
    - description
    - version
  - [ÐAPPs](/dev/dapps) for interacting with the contract<br>
    Web pages build for interacting with the contract are referenced in the description, the physical files themselves are stored in a distributed file system and a reference to them is stored in the description.

References in the description can be stored in two ways:
  - distributed file system references:<br>
    This is used when files are stored directly. Examples are configuration files, files used within an app and documents that belong to a contract directly.
  - module references:<br>
    Module references are references to a description file on a module. These are resolved like an original description and allow nesting of modules, [ÐAPPs](/dev/dapps) and module versioning.

DBCP descriptions can be stored at ENS names as well. ENS can be used to address smart contracts (which can by default only be addressed with their technical address) via a human readable DNS domain like syntax. Therefore it is possible to setup smart contracts and their ÐApps like websites.

DBCP based applications can be described as a bundle of the ENS address, where the DBCP description can be retrieved from, the smart contract that handles the logic and the ÐApps for interacting with it.

![DBCP bundle](/public/dev/dbcp_bundle.png)


## Properties in Description
example DBCP file:
```json
{
  "public": {
    "autor": "contractus",
    "dapp": {
      "entrypoint": "dapp-taskboard.js",
      "files": [
        "dapp-taskboard.js",
        "dapp-taskboard.css"
      ],
      "type": "dapp",
      "module": "TaskBoardModule",
      "origin": "Qm...",
      "primaryColor": "#e87e23",
      "secondaryColor": "#fffaf5",
      "standalone": true
    },
    "i18n": {
      "description": {
        "en": "Create todos and manage updates",
        "de": "Erstelle Aufgaben und überwache Änderungen"
      },
      "name": {
        "en": "Task Board",
        "de": "Task Board"
      }
    },
    "description": "Create todos and manage updates.",
    "name": "taskboard",
    "tags": [
      "dapp",
      "contractus"
    ],
    "imgSquare": "data:image/png;base64,...",
    "version": "0.1.0",
    "dataSchema": {
      "list_settable_by_member": {
        "$id": "list_settable_by_member_schema",
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "foo": { "type": "string" },
          "bar": { "type": "integer" }
        }
      },
      "entry_settable_by_member": {
        "$id": "entry_settable_by_member_schema",
        "type": "integer",
      }
    }
  }
}
```
Depending on the visibility of the properties, these are placed under a different scope. These scopes are "public" (unencrypted, visible for everyone) and "private" (encrypted, visible for a limited scope of people).

| Property | Required? | Type | Description |
| -------- | --------- | ---- | ----------- |
| name | x | string | name of the contract |
| description | x | string | short description of the contract |
| author | x | string | author of the ÐAPP |
| version | x | string | version information about the contract |
| abi | | object[] | if this DBCP description describes a contract, the ABI for this contract, see "ABI example" section below for an example  |
| dataSchema | | string | json schema definition for data in the contract, written as [ajv](https://github.com/epoberezkin/ajv) schemas |
| tags | | string[] | tags for categorizing the contract |
| i18n | | object | labels for displaying contract information (multilingual) |
| imgSquare | | string | contract logo (square) e.g. for icons - can be Data URL or regular URL   |
| imgWide | | string | contract logo (wide) e.g. for sidebar - can be Data URL or regular URL |
| dapp | | object | details about the used ÐApp, see section "ÐApp Definition" below |
| blockchain | | object | blockchain reference, see section "Blockchain Reference" below |
| dfs | | object | distributed file system reference, see section "Distributed File System Reference" below |


## ÐApp Definition
Contracts that use a ÐApp for interacting with it, need the "dapp" property, that supports the following elements:

| Property | Required? | Type | Description |
| -------- | --------- | ---- | ----------- |
| entrypoint | x | string | startup file for ÐApp |
| files | x | string[] | included files (.css, .js, ...) |
| type | x | string | library/dapp |
| module | x | string | start module for embedded Angular application |
| origin | x | string | hash reference where the ÐApp is stored in the distributed file system |
| primaryColor | | string | color code for primary color |
| secondaryColor | | string | color code for secondary color |
| standalone | | bool | indicates whether this ÐApp runs in "full screen" without a run container |
| dependencies | | object | dependencies of this ÐAPP |

ÐAPP dependencies are similar to dependencies in npm packages and allow to specify their required version range, example:
```json
"dependencies": {
  "angular-bc": "^0.1.0",
  "angular-core": "^0.1.0",
  "angular-libs": "^0.1.0",
  "bcc-bc": "^0.1.0"
}
```

Taking the version from the example, the ÐAPP will try to locate the latest minor version of the dependencies and load it from their respective ENS address. This example would use the latest feature adding or bug fixing versions but ignore possible breaking changes.

Applications build this way can be deployed once and used as long as desired, as they use a stable code base, that can be fixed if bugs occur.


## Blockchain Reference
Contracts may be stored in side chains. Such contracts need the property "blockchain" in their DBCP description to point to that chain.

If omitted, the default blockchain is used

| Property | Required? | Type | Description |
| -------- | --------- | ---- | ----------- |
| referenceType | x | string | type of the reference, see below | 
| referenceValue | x | string | value describing the reference, see below |

| referenceType | description | example |
| ------------- | ----------- | ------- |
| ens | blockchain reference is stored in an own ENS entry | default.blockchainregistry.eth |
| url | a link to an RPC endpoint | http://localhost |


## Distributed File System Reference
Contract data may be stored in different distributed file systems. Such contracts need the property "dfs" in their DBCP description to point to that storage.

If omitted, the default DFS is used

| Property | Required? | Type | Description |
| -------- | --------- | ---- | ----------- |
| referenceType | x | string | type of the reference, see below | 
| referenceValue | x | string | value describing the reference, see below |

| referenceType | description | example |
| ------------- | ----------- | ------- |
| ens | DFS reference is stored in an own ENS entry | default.dfsregistry.eth |
| url | a link to an DFS endpoint, like a IPFS server endpoint | ws://localhost:8546 |


## ABI Example
This section shows an example for an ABI, which allows to setting/getting the description and setting/getting the owner of the contract. Contracts, that use DBCP for their own descriptions or to extend descriptions of an ENS address, they are registered at, should at least implement the `contractDefinition` function, which returns a DFS hash, that points to the description.
```json
[
  {
    "constant": true,
    "inputs": [],
    "name": "contractDefinition",
    "outputs": [
      {
        "name": "",
        "type": "bytes32"
      }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "constant": false,
    "inputs": [
      {
        "name": "owner_",
        "type": "address"
      }
    ],
    "name": "setOwner",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "constant": false,
    "inputs": [
      {
        "name": "_contractDefinition",
        "type": "bytes32"
      }
    ],
    "name": "setDescription",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "constant": true,
    "inputs": [],
    "name": "owner",
    "outputs": [
      {
        "name": "",
        "type": "address"
      }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  }
]
```

## Community Webpage
You can find more information about DBCP on the [DBCP Community Webpage](https://dbcp.online/)<sup>[+]</sup> (German).