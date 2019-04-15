---
title: "Endpoints"
parent: Developers
grand_parent: API
nav_order: 4230
permalink: /docs/developers/api/endpoints.html
---

# Endpoints
## RPC
### core - Production Chain

The production chain is named "core" and is the main blockchain from evan.network an provided by the [AuthorityNodes](/docs/how_it_works/authoritynode.html).

#### RPC Endpoint
You can access the endpoint via HTTPS and WebSocket e.g via [web3](https://github.com/ethereum/web3.js) at: `https://core.evan.network`

#### Blockchain Node
To start an own node that is synced with the core chain, you must install [Parity](https://parity.io/)<sup>[+]</sup> (Version >=1.10.0) on your server. Then you can download the Parity config file from [GitHub](https://github.com/evannetwork/core-config)<sup>[+]</sup> and start your local node:
```bash
parity --chain "/path/to/core.json"
```

### testcore - Development Chain

To start hacking on evan.network, it is best to use the testcore network to make the first steps. The testcore network is similar to the core main network but without the need to buy [EVE](/docs/other/glossary.html#e) tokens. To get EVE tokens for the testcore network, you can join the [Gitter faucet](https://gitter.im/evannetwork/faucet)<sup>[+]</sup> channel and post you account ID.

#### RPC Endpoint
You can access the endpoint via HTTPS: `https://testcore.evan.network`

and WebSocket: `wss://testcore.evan.network/ws`

e.g with [Web3](https://github.com/ethereum/web3.js).


#### Blockchain Node
To start an own node that is synced with the testcore chain, you must install [Parity](https://www.parity.io/) (Version >=1.10.0) on your server. Then you can download the Parity config file from [GitHub](https://github.com/evannetwork/testcore-config) and start your local node:
```bash
parity --chain "/path/to/testcore.json"
```


## IPFS