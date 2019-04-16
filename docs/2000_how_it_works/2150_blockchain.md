---
title: "Blockchain"
parent: How it works
nav_order: 2150
permalink: /docs/how_it_works/blockchain.html
---

<!--
  TODO:
    - move EVE info into own section
    - links to explorer / status page?
-->

# Blockchain

evan.network is a [Proof of Authority (PoA)](https://en.wikipedia.org/wiki/Proof-of-authority) publicly accessible blockchain for Ethereum. The evan.network blockchain runs on [Parity](https://parity.io/) nodes that use the [Aura](https://wiki.parity.io/Aura.html) consensus to build a trustful, stable and fast network of authorities. The authorities are hosted and operated by evan.network [AuthorityNodes](/docs/how_it_works/authoritynode.html). The blockchain is set up and operated with the goal to be 100% Ethereum compliant. So the network can participate from the improvements and new features that are in development in the Ethereum community e.g [Plasma](https://plasma.io/), Casper, [ParityBridge](https://github.com/paritytech/parity-bridge), to name only a few. In the future we also have plans to launch use case specific optimized subchains that are connected with a bridge to the **core** chain, to meet special application needs. These subchains are operated with the same DAO governance and token structure.

The evan.network usage is publicy available. That means every user can send transactions to the evan.network, but only AuthorityNodes are authorized to sign new blocks. To send transactions the user or application needs [EVE](/docs/other/glossary.html#e) tokens to pay the transaction fees.

The **benefits** of evan.network toward the Ethereum public chains are:
* no competitive mining >> so no energy wasting
* optimized for enterprise business >> high transactions throughput and 3sec block time
* new blocks can only be signed by known [AuthorityNodes](/docs/how_it_works/authoritynode.html) >> [51%](https://learncryptography.com/cryptocurrency/51-attack) attacks are not possible

Users and developers can access the evan.network blockchain via our RPC endpoints or can sync the chain with an own Parity. An own Parity node is the best option for developers to connect on-premise applications like DB, ERP, CRMor PPS systems with evan.network. The RPC endpoint is the best option for ÐAPPs and interactive applications. The RPC endpoint is also available decentralized through all AuthorityNode providers.

Like in the public Ethrereum chain, all read applications against the chain are free. If you will submit transactions to the chain you need [EVE Tokens](/docs/other/glossary.html#e) to pay the gas costs. The amount of the needed gas is dependent on the complexity of the transactions that are submitted and can be calculated in front with the API.

Different from other blockchains the paid gas costs are not transfered to the AuthorityNode that signed the block with the transaction. All [EVE tokens](/docs/other/glossary.html#e) that are paid from users and applications for gas are gathered in a DAO owned Smart Contract. [EVE tokens](/docs/other/glossary.html#e) that are transfered to contracts or accounts are not affected, **ONLY** the transaction fees.


### EVE - Token

EVE tokens are the evan.network built-in coins to pay transaction fees. EVE is a utility token that can only be used inside the evan.network to pay for the technical infrastructure. EVE tokens will not be traded on public coin exchanges.

#### Production Tokens
The **core** production chain will be launched soon, where we also offer a service to buy EVE tokens directly.

#### Development Tokens
You can get development tokens for the [testcore chain](https://github.com/evannetwork/testcore-config) for **FREE** through the evan.network [Gitter faucet](https://gitter.im/evannetwork/faucet) channel. These EVE tokens only exists in the **testcore** chain and can't be moved to the **core** chain.
