---
title: "Blockchain"
---
# Blockchain

The evan.network Blockchain is build on [Parity](https://www.parity.io/) nodes, that are hosted and operated by evan.network [MasterNodes](/docs/masternode). These nodes building the fundamental consensus to sign new blocks in the evan.network.

User and developers can access the evan.network Blockchain via RPC Endpoints or can sync the chain with an own node.

## core - Production Chain

The production chain is named [core](/docs/urls) and is the main blockchain offered by the [MasterNodes](/docs/masternode).

### RPC Endpoint
You can access the endpoint via HTTPS and WebSocket.
`https://core.evan.network`

### Blockchain Node
To start a own node that is synced with the core chain, you must install [Parity](https://www.parity.io/) (Version >=1.10.0) on your server. Then you can download the parity config file from [GitHub](https://github.com/evannetwork/core-config) and start your local node:
```bash
parity --chain "/path/to/core.json"
```

## testcore - Development Chain

To start hacking on evan.network it is the best to use the [testcore](/docs/urls) network to make the first steps. The [testcore](/docs/urls) network is similar to the [core](/docs/urls) main network but without the need to buy [EVE](/docs/eve) tokens. To get EVE tokens for the [testcore](/docs/urls) network you can join the [Gitter faucet](https://gitter.im/evannetwork/faucet) channel and post you account ID.

### RPC Endpoint
You can access the endpoint via HTTPS and WebSocket.
`https://testcore.evan.network`

### Blockchain Node
To start a own node that is synced with the testcore chain, you must install [Parity](https://www.parity.io/) (Version >=1.10.0) on your server. Then you can download the parity config file from [GitHub](https://github.com/evannetwork/testcore-config) and start your local node:
```bash
parity --chain "/path/to/testcore.json"
```
