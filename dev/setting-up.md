---
title: "Setting Up"
---

# Setting up a Development Environment
To start developing in the evan network, you primarily need need 3 things:

1. You need to connect to the right blockchain
2. You need to set up nodejs
3. You need to install the support libraries

## Connecting to the blockchain

Assuming you already know what the blockchain is and some basics about how it works and the ecosystem.

The [evan.network](https://evan.network/) uses [parity](https://www.parity.io/) as its blockchain client.
The reason to use it over [geth](https://geth.ethereum.org/) is the more extensive toolchain and functionality. Geth and others can't even be used in evan.network, because there are required configurations
that are not supported by geth.

This is only really relevant if you want to install the blockchain client on your own machine. Most of the time it is sufficient to configure your applications to connect to one of the [MasterNodes](/doc/masternodes).

But if you do install your own parity, you need to use the testcore blockchain for development. The configuration for this is available [here](https://github.com/evannetwork/testcore-config).

The exact configuration of which blockchain client to connect to depends on the application you use, but if you don't set up your own, you can always use `wss://testcore.evan.network/ws` for the development blockchain.

The development blockchain is the only that exists at the moment for the evan.network.

There will be at least one more, the production chain, which will be called "core" and not "testcore".

It is very useful to start parity with the `--force-ui` parameter, which allows you to access a web-admin on http://localhost:8180 which provides a lot of functionality where the command line is just a little more complicated.


## Create an Identity
To do anything on the blockchain, you need an account, an identity. This is not just relevant for developers, and is described [here](/tutorial/create-identity).

## Installing Solidity

There are two main options to install solidity, via native package on debian/ubuntu based distributions:

```sh
$ sudo add-apt-repository ppa:ethereum/ethereum
$ sudo apt-get update
$ sudo apt-get install solc
```

Or via nodejs:

```sh
$ npm install -g solc
```

There are more options and more details available [here](https://solidity.readthedocs.io/en/v0.4.23/installing-solidity.html).

## Setting up nodejs

Setting up [nodejs](https://nodejs.org/en/) is pretty straightforward on most operation systems.
You will also need [`npm`](https://www.npmjs.com/), almost certainly `npx` and [`nvm`](https://github.com/creationix/nvm/blob/master/README.md), too.

All the basic prerequisites for this, like `git`, need to be installed too, but usually the package manager of your OS takes care of this.

## Install the Support Libraries

So far this seems easy enough. The primary thing to install is the [blockchain-core libs](https://github.com/evannetwork/blockchain-core). They are written in typescript and implemented as an npm package, so the installation should be pretty straightforward.

Since the node ecosystem, and especially the ethereum apis are pretty fast moving environments it is not unlikely to encounter dependency and version problems though, at least for the time being.

# Your first evan.network Contract

Don't let yourself be intimidated by the word "contract". A contract in the ethereum context is not too different from a class like in Java in the way it is written and used: It contains data fields, methods/functions that work with those data fields and some permission facilities to access those.  
The big difference is of course, each contract is a global singleton and all data changes are cryptographically verfied and agreed upon by the blockchain users.

It will be a simple Hello World, where the string comes from the blockchain.
We will be using the defacto-standard blockchain development framework, [truffle](http://truffleframework.com), simply because it is so easy to set up and use and a lot of resources exist online.

[Hello World](/dev/hello-world)


# Your first SmartAgent

[SmartAgent](/doc/smart-agents) is just a fancy name for a web service that provides blockchain access but has no own user interface. Usually it has some kind of RPC API, in REST format or otherwise, or it connects to some other service and listens for events.

The agent you will be writing will use the [blockchain-core](https://github.com/evannetwork/blockchain-core) library, which bundles and encapsulates a lot of specialized functionality for evan.network, but also just provides a lot of standard blockchain functionality.

[Hello Agent](/dev/hello-agent)

# Your first Ðapp

A [Ðapp](/dev/dapps) is just an application that utilizes the blockchain, and has distributed logic as a result. This is most often just a web application accessible via browser. But it is very possible to write Ðapps in any runtime environment, even native applications, as long as there is access to a blockchain, which usually means access to the network, at least some of the time.

Evan.network Ðapps utilize the evan.network framework. This makes a lot of things easier.

Your first Ðapp will be a simple web application, that connects to the previous SmartAgent and directly to the blockchain itself.

[Hello Ðapp](/dev/hello-dapp)
