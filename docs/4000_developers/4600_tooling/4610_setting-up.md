---
title: "Setting Up"
parent: Developers
grand_parent: Tooling
nav_order: 4610
permalink: /docs/developers/tooling/setting-up.html
---

# Setting up a Development Environment
To start developing in evan.network, you primarily need need three things:

1. You need to connect to the public evan.network blockchain
2. You need to set up `nodejs`
3. You need to install the support libraries

## Connecting to evan.network

Assuming you already know what a blockchain is and some basics about how it and the ecosystem works.

[evan.network](https://evan.network/) needs a blockchain client and uses [Parity](https://www.parity.io/) for this.
The reason to prefer it over [Geth](https://geth.ethereum.org/) is the more extensive toolchain and functionality. Geth and others cannot be used in evan.network, because there are required configurations that are not supported by Geth.

This becomes only relevant in case you want to install the blockchain client on your own machine. Most of the time it is sufficient to configure your applications to connect to one of the evan.network [AuthorityNodes](/docs/how_it_works/authoritynode.html).

However, if you do install your own AuthorityNode, you need to use the evan.network testcore blockchain for development. The Parity configuration for this is available [here](https://github.com/evannetwork/testcore-config).

The exact configuration of which blockchain client to connect to depends on the application you use, but if you don't set up your own you can always use `wss://testcore.evan.network/ws` for the development blockchain.

The development blockchain is the only one that exists at the moment for the evan.network.

There will be at least one more blockchain, the production chain, which will be called 'core' and not 'testcore'.

You might find it useful for admininistration purposes to start Parity with the `--force-ui` parameter, which allows you to access a web-GUI on http://localhost:8180 and provides a more convenient option than the command line for some functionalities.


## Create an Identity
To do anything on the blockchain, you need an account: the identity. This is not just relevant for developers and is described [here](/docs/first_steps/create-identity.html).

## Installing Solidity

There are two main options to install Solidity, via native package on Debian/ Ubuntu based distributions:

```sh
$ sudo add-apt-repository ppa:ethereum/ethereum
$ sudo apt-get update
$ sudo apt-get install solc
```

Or via `nodejs`:

```sh
$ npm install -g solc
```

There are more options and more details available [here](https://solidity.readthedocs.io/en/v0.4.23/installing-solidity.html).

## Setting up nodejs

Setting up [`nodejs`](https://nodejs.org/en/) is pretty straight forward on most operation systems.
You will also need [`npm`](https://www.npmjs.com/), almost certainly `npx` and [`nvm`](https://github.com/creationix/nvm/blob/master/README.md), too.

All the basic prerequisites for this, like `git`, need to be installed too, but usually the package manager of your OS takes care of this.

At the time `nodejs v10.*` is not supported yet though.

## Installation the Support Libraries

So far, this seems easy enough. The primary thing to install is the [blockchain-core libs](https://github.com/evannetwork/api-blockchain-core). They are written in `typescript` and implemented as a `npm` package, so the installation should be straight forward, too.

Since the node ecosystem and especially the Ethereum APIs are pretty fast moving environments, it is not unlikely to encounter dependency and version problems though, at least for the time being.
