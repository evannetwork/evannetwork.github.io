---
title: "Endpoints"
parent: Developers
grand_parent: API
nav_order: 4230
permalink: /docs/developers/api/endpoints.html
---

# Endpoints
## core - Production Chain
The production chain is named "core" and is the main blockchain from evan.network an provided by the [AuthorityNodes](/docs/how_it_works/authoritynode.html).

### RPC Endpoint
You can access the endpoint via HTTPS and WebSocket e.g via [web3](https://github.com/ethereum/web3.js) at:
- `wss://core.evan.network/ws` (WebSocket)
- `https://core.evan.network` (HTTPS)

Or if you want to start an own node that is synced with the core chain, you have to install [Parity](https://parity.io/) (Version >=1.10.0) on your server. Then you can download the Parity config file from [GitHub](https://github.com/evannetwork/core-config) and start your local node:
```bash
parity --chain "/path/to/core.json"
```
and access your Websocket or HTTP(S) endpoints of your local node.

### IPFS
You can reach the IPFS service for the core at `https://ipfs.evan.network`.


## testcore - Development Chain

To start hacking on evan.network, it is best to use the testcore network to make the first steps. The testcore network is similar to the core main network but without the need to buy [EVE](/docs/other/glossary.html#e) tokens. To get EVE tokens for the testcore network, you can join the [Gitter faucet](https://gitter.im/evannetwork/faucet) channel and post you account ID.

### RPC Endpoint
You can access the endpoint via HTTPS and WebSocket e.g via [web3](https://github.com/ethereum/web3.js) at:
- `wss://testcore.evan.network/ws` (WebSocket)
- `https://testcore.evan.network` (HTTPS)

Or if you want to start an own node that is synced with the core chain, you have to install [Parity](https://parity.io/) (Version >=1.10.0) on your server. Then you can download the Parity config file from [GitHub](https://github.com/evannetwork/testcore-config) and start your local node:
```bash
parity --chain "/path/to/testcore.json"
```
and access your Websocket or HTTP(S) endpoints of your local node.

### IPFS
You can reach the IPFS service for the testcore at `https://ipfs.test.evan.network`.
