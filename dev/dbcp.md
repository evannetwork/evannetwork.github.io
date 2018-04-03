---
title: "DBCP"
---

# DBCP 
## About
The Decentralized Business Communication Protocol (DBCP) is a formalized description of how to interact with (Ethereum) smart contracts. This makes a smart contract almost a single point of contact for interacting with the evan.network. This description includes technical detail to enable developers to write applications that interact with this contract and/or a distributed app (ÐApp), that can be used with a web browser.


## Structure
The DBCP description is saved as a JSON file, which is stored is a distributed filesystem (IPFS). Files stored in the distributed filesystem can be retrieved via their hashes and this hash is stored at the smart contract. Further dependencies are resolved in the same manner. Description files for subcomponents are pulled from distributed filesystem as well and so on.

This description resembles a package.json known from NodeJS modules in its functionality.

The following information can be included in the description file:

  - basic information about the contract, for example:
    - name
    - description
    - version
  - [ÐAPPs](/dev/dapps) for interacting with the contract<br>
    Web pages build for interacting with the contract are referenced in the description, the physical files themselves are stored in a distributed file system and a reference to them is stored in the description.

References in the description can be stored in two ways:
  - distributed filesystem references:<br>
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
    "img": "data:image/png;base64,...",
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
| author | x | string | author of the dapp |
| version | x | string | version information about the contract |
| dataSchema | | string | json schema definition for data in the contract, written as [ajv](https://github.com/epoberezkin/ajv)<sup>[+]</sup> schemas |
| tags | | string[] | tags for categorizing the contract |
| i18n | | object | labels for displaying contract information (multilingual) |
| img | | string | contract logo |
| dapp | | object | details about the used dapp, see following table for properties |


## ÐApp Definition
Contracts that use a ÐApp for interacting with it, need the "dapp" property, that supports the following elements:

| Property | Required? | Type | Description |
| -------- | --------- | ---- | ----------- |
| entrypoint | x | string | startup file for ÐApp |
| files | x | string[] | included files (.css, .js, ...) |
| type | x | string | library/dapp |
| module | x | string | start module for embedded Angular application |
| origin | x | string | hash reference where the ÐApp is stored in the distributed filesystem |
| primaryColor | | string | color code for primary color |
| secondaryColor | | string | color code for secondary color |
| standalone | | bool | indicates whether this ÐApp runs in "fullscreen" without a run container |


## Community Webpage
You can find more information about DBCP on the [DBCP Community Webpage](https://dbcp.online/)<sup>[+]</sup> (German).