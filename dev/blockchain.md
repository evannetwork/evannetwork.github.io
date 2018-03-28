---
title: "Blockchain"
---
# Blockchain

evan.network is a [Proof of Authority (PoA)](https://en.wikipedia.org/wiki/Proof-of-authority)<sup>[+]</sup> publicly accessible blockchain for Ethereum. The evan.network Blockchain is build on [Parity](https://parity.io/)<sup>[+]</sup> nodes, that are hosted and operated by evan.network [MasterNodes](/doc/masternode). Every user can send transactions to the evan.network, but only MasterNodes are authorized to sign new blocks. To send transactions the user or application needs [EVE](/doc/eve) Tokens to pay the transaction fees.

The **benefits** of evan.network toward the Ethereum public chains are:
* no competitive mining >> so no energy wasting
* optimized for enterprise business >> high transactions throughput and 3sec BlockTime  
* new blocks can only signed by known [MasterNodes](/doc/masternode) >> [51%](https://learncryptography.com/cryptocurrency/51-attack) attacks are not possible

User and developers can access the evan.network Blockchain via our RPC Endpoints or can sync the chain with an own Parity. The own Parity node is the best option for developers to connect onpremise applications like e.g. DB, ERP, CRM, PPS system with evan.network. The RPC Endpoint is the best option for ÐAPPs and interactive applications. The RPC Endpoint is also provided decentralized through all MasterNode providers.

Like in the public Ethrereum chain, all read applications against the chain are free. If you will submit transactions to the chain you need [EVE Tokens](/doc/eve) to pay the GAS costs that depend on the complexity of the transaction.

Different from other blockchains the paid GAS costs are not get paid to the MasterNodes. All [EVE Tokens](/doc/eve) that are paid from users and applications are gathered in a [DAO](/doc/dao) owned SmartContract.

## core - Production Chain

The production chain is named [core](/doc/resources) and is the main blockchain from evan.network an provided by the [MasterNodes](/doc/masternode).

### RPC Endpoint
You can access the endpoint via HTTPS and WebSocket e.g via [Web3](/dev/web3).
`https://core.evan.network`

### Blockchain Node
To start a own node that is synced with the core chain, you must install [Parity](https://parity.io/)<sup>[+]</sup> (Version >=1.10.0) on your server. Then you can download the parity config file from [GitHub](https://github.com/evannetwork/core-config)<sup>[+]</sup> and start your local node:
```bash
parity --chain "/path/to/core.json"
```

## testcore - Development Chain

To start hacking on evan.network it is the best to use the [testcore](/doc/resources) network to make the first steps. The [testcore](/doc/resources) network is similar to the [core](/doc/resources) main network but without the need to buy [EVE](/doc/eve) tokens. To get EVE tokens for the [testcore](/doc/resources) network you can join the [Gitter faucet](https://gitter.im/evannetwork/faucet)<sup>[+]</sup> channel and post you account id.

### RPC Endpoint
You can access the endpoint via HTTPS: `https://testcore.evan.network`

and WebSocket: `wss://testcore.evan.network/ws`

e.g with [Web3](/dev/web3).


### Blockchain Node
To start a own node that is synced with the testcore chain, you must install [Parity](https://www.parity.io/) (Version >=1.10.0) on your server. Then you can download the parity config file from [GitHub](https://github.com/evannetwork/testcore-config) and start your local node:
```bash
parity --chain "/path/to/testcore.json"
```
