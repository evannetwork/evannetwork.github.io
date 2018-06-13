---
title: "Blockchain Core Console"
---
# Blockchain Core Console

The simplest way to just start playing with evan network is to install the blockchain-core-console, bccc.js.

Don't let the name fool you, this is not just for working with blockchain contracts, the `bccc` can be used to interact with all components of the evan.network, i.e. also the [IPFS](/dev/ipfs) file stores, the [ENS](/dev/ens).

# Installing

Installing the bccc is as simple as 

```sh
$ npm i blockchain-core-console
```

# Configuration

There is a standard configuration, which will establish default evan.network connections for all components.
If you want or have to use a different IPFS server or parity, you can change the configuration in `$HOME/.bccc.json`


# Deploy

Now that this is installed and configured, let's take our [hello world contract](/dev/hello-world) and deploy it with the evan.network toolchain instead of truffle.

Run `bccc.js`.

```javascript

```



If you are new to evan.network, no matter if you are also completely new to ethereum contract development, or if you already have a portfolio of contracts you want to deploy, you will want to put them on
the network rather sooner than later.

We have a small example on how to do this with truffle in the [Hello Contract](hello-contract), but this
is actually not the recommended way of doing things. Particularly because it avoids using [DBCP](dbcp), and with it one of the main advantages of evan.network.

So here we go:

## Compiling
Contracts are written in [solidity](https://solidity.readthedocs.io/en/v0.4.23/). Nothing else is supported.
You can write and compile and test your contracts on your private test blockchains however you like. Maybe use
truffle, as described in the Hello Contract, or [remix](https://remix.ethereum.org).

## Creating the DBCP API Files
A main feature of evan.network is to be able to streamline the interaction between applications that run outside the blockchain but use the blockchain and the contracts on the blockchain with a specification file.

One of the things that is enabled by this is the automatic updating and redeploying of contracts that belong to an application. The format is a normal JSON file.

```json
{
  "public": {
    "name": "Hello",
    "dapp": {
      "entrypoint": "task.js",
      "files": [ "testContract.js" ],
      "origin": "Qm...",
      "standalone": true,
      "type": "dapp"
    },
    "description": "Create todos and manage updates.",
    "dbcpVersion": 1,
    "i18n": {
      "description": {
        "de": "Erstelle Aufgaben oder zeige sie an",
        "en": "Create tasks or show them"
      },
      "name": {
        "de": "Task",
        "en": "Task"
      }
    },
    "imgSquare": "data:image/png;base64,...",
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
    },
    "abis": {
      "own": [
        "contract abi..."
      ]
    },
    "source": "Qm...",
    "version": "1.0.0",
  }
}
```


## Pushing it into the Blockchain


# The Simplest Way
Once it is fully released, it will be possible to just put all your .sol files in a directory and configure your smart-contracts project to include everything from this directory. It will then take care of everything for you automatically.

So:


