---
title: "Authority Nodes"
parent: How it works
nav_order: 2420
permalink: /docs/how_it_works/authoritynode.html
---

# Proof-of-Authority Consensus & AuthorityNodes

Consensus on the evan.network is established by a [Proof-of-Authority(PoA) algorithm](https://wiki.parity.io/Aura.html), under the custody of AuthorityNodes(also referred to as AuthorityNodes).

Utlizing PoA comes with certain benefits. It allows for network-wide GDPR compliance, as data is handled by known Data Processors. In comparison to e.g. Bitcoin's Proof-of-Work algorithm, PoA is very easy on energy consumption as well.

In this model, nodeoperators are handpicked and comprise of qualified entities, usually companies actively engaged in the network.

New transactions are legitimized by AuthorityNodes. Transactions broadcasted to the network are received by the nodes and signed into new blocks, adding them to the blockchain.

Since AuthorityNode security is critical, these nodes have no open ports to any RPC or Websocket API. They only sign transactions and seal blocks. Nodeoperators on the evan.network provide several servers.
The servers have to be hosted in an European data center.
