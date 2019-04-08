---
title: "Blockchain"
layout: default
parent: Developers
---
# Blockchain

evan.network is a [Proof of Authority (PoA)](https://en.wikipedia.org/wiki/Proof-of-authority)<sup>[+]</sup> publicly accessible blockchain for Ethereum. The evan.network blockchain runs on [Parity](https://parity.io/)<sup>[+]</sup> nodes that use the [Aura](https://wiki.parity.io/Aura.html) consensus to build a trustful, stable and fast network of authorities. The authorities are hosted and operated by evan.network [AuthorityNodes](/doc/authoritynode). The blockchain is set up and operated with the goal to be 100% Ethereum compliant. So the network can participate from the improvements and new features that are in development in the Ethereum community e.g [Plasma](https://plasma.io/)<sup>[+]</sup>, Casper, [ParityBridge](https://github.com/paritytech/parity-bridge)<sup>[+]</sup>, to name only a few. In the future we also have plans to launch use case specific optimized subchains that are connected with a bridge to the **core** chain, to meet special application needs. These subchains are operated with the same DAO governance and token structure.

The evan.network usage is publicy available. That means every user can send transactions to the evan.network, but only AuthorityNodes are authorized to sign new blocks. To send transactions the user or application needs [EVE](/doc/eve) tokens to pay the transaction fees.

The **benefits** of evan.network toward the Ethereum public chains are:
* no competitive mining >> so no energy wasting
* optimized for enterprise business >> high transactions throughput and 3sec block time
* new blocks can only be signed by known [AuthorityNodes](/doc/authoritynode) >> [51%](https://learncryptography.com/cryptocurrency/51-attack) attacks are not possible

User and developers can access the evan.network blockchain via our RPC endpoints or can sync the chain with an own Parity. An own Parity node is the best option for developers to connect on-premise applications like DB, ERP, CRMor PPS systems with evan.network. The RPC endpoint is the best option for ÐAPPs and interactive applications. The RPC endpoint is also available decentralized through all AuthorityNode providers.

Like in the public Ethrereum chain, all read applications against the chain are free. If you will submit transactions to the chain you need [EVE Tokens](/doc/eve) to pay the gas costs. The amount of the needed gas is dependent on the complexity of the transactions that are submitted and can be calculated in front with the API.

Different from other blockchains the paid gas costs are not transfered to the AuthorityNode that signed the block with the transaction. All [EVE tokens](/doc/eve) that are paid from users and applications for gas are gathered in a [DAO](/doc/dao) owned Smart Contract. [EVE tokens](/doc/eve) that are transfered to contracts or accounts are not affected, **ONLY** the transaction fees.

## core - Production Chain

The production chain is named [core](/doc/resources) and is the main blockchain from evan.network an provided by the [AuthorityNodes](/doc/authoritynode).

### RPC Endpoint
You can access the endpoint via HTTPS and WebSocket e.g via [Web3](/dev/web3).
`https://core.evan.network`

### Blockchain Node
To start an own node that is synced with the core chain, you must install [Parity](https://parity.io/)<sup>[+]</sup> (Version >=1.10.0) on your server. Then you can download the Parity config file from [GitHub](https://github.com/evannetwork/core-config)<sup>[+]</sup> and start your local node:
```bash
parity --chain "/path/to/core.json"
```

## testcore - Development Chain

To start hacking on evan.network, it is best to use the [testcore](/doc/resources) network to make the first steps. The [testcore](/doc/resources) network is similar to the [core](/doc/resources) main network but without the need to buy [EVE](/doc/eve) tokens. To get EVE tokens for the [testcore](/doc/resources) network, you can join the [Gitter faucet](https://gitter.im/evannetwork/faucet)<sup>[+]</sup> channel and post you account ID.

### RPC Endpoint
You can access the endpoint via HTTPS: `https://testcore.evan.network`

and WebSocket: `wss://testcore.evan.network/ws`

e.g with [Web3](/dev/web3).


### Blockchain Node
To start an own node that is synced with the testcore chain, you must install [Parity](https://www.parity.io/) (Version >=1.10.0) on your server. Then you can download the Parity config file from [GitHub](https://github.com/evannetwork/testcore-config) and start your local node:
```bash
parity --chain "/path/to/testcore.json"
```

### EVE - Token

EVE tokens are the evan.network built-in coins to pay transaction fees. EVE is a utility token that can only be used inside the evan.network to pay for the technical infrastructure. EVE tokens will not be traded on public coin exchanges.

#### Production Tokens
The **core** production chain will be launched soon, where we also offer a service to buy EVE tokens directly.

#### Development Tokens
You can get development tokens for the [testcore chain](https://github.com/evannetwork/testcore-config) for **FREE** through the evan.network [Gitter faucet](https://gitter.im/evannetwork/faucet)<sup>[+]</sup> channel. These EVE tokens only exists in the **testcore** chain and can't be moved to the **core** chain.
