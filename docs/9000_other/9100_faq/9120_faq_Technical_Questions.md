---
title: Technical Questions
parent: Other
grand_parent: FAQ
nav_order: 9120
permalink: /docs/other/faq/technical.html
---

# FAQ

**Technical Questions**

#### Q.
***What is the underlying distributed ledger technology?***

#### A.
The offered blockchain framework is based on Ethereum private blockchain, operated as a consortial blockchain.
Every [AuthorityNode](/docs/how_it_works/authoritynode.html) hosts a Parity V1.10.x node to build the core network. The nodes are managed by a [Smart Contract](/docs/developers/smart-contracts.html), that signals all AuthorityNodes whether a software upgrade is needed or a hardfork must be done. So extensive software management on the AuthorityNode site is not needed. The Smart Contract itself is controlled by the DAO Smart Contract, operated by the evan.network, where the partners vote for needed upgrades or potential chain-forks.


#### Q.
***What kind of consensus protocol is used in the evan.network?***

#### A.
A Smart Contract based Proof Of Authority consensus is used. [AuthorityNode](/docs/how_it_works/authoritynode.html) operators (Affiliates) are added to the group of authorities (DAO). Only these are able to sign new blocks.
The network doesn’t use competitive mining on the chain and also the transactions fees are not distributed to the AuthorityNode that signed a new block (gas is burned). All AuthorityNodes are working for the same goal - a save, fast and cost-efficient chain.

#### Q.
***What is the maximum of transactions per second?***

#### A.
This depends on the types of transactions performed. There is a maximum amount of 950 transactions per second possible. This amount of transactions can only be achieved with transactions that use the minimum amount of gas. The evan.network has a minimum block time of 3 seconds.
There are also plannings to add sharding and other performance optimization technologies to the evan.network as soon as they are available in Ethereum.

Furthermore, there is an ongoing work for subchain support, to allow [AuthorityNodes](/docs/how_it_works/authoritynode.html) to connect a private subchain to the evan.network using a bridge. With subchains, partners have full control over the subchain and still take advantage of the core evan.network.

#### Q.
***Which challenges are solved with the evan.network and which features are addressed in the solution?***

#### A.
**Challenge 1:**    Trustful digital value exchange

Features:
* Secure exchange of digital values and documents
* Trustful interaction between individuals, machines and corporates
* Automate administrative cross-company processes

**Challenge 2:**    Decentralized Identity Management

Features:
* Identities and profiles for individuals and companies
* Self-controlled identity for all business networks
* Confirmation of identity and trust

**Challenge 3:**    End-to-End Tracking

Features:
* Process transparency and tracking
* Tracking of assets like products and parts
* Tamper-proof asset history

**Challenge 4:**    Decentralized Marketplaces & Matchmaking

Features:
* Easy to find and connect with partners
* Digital matchmaking of supply and demand

**Challenge 5:**    Trustful M2M Communication

Features:
* Digital asset representation
* Secure machine to blockchain communication

#### Q.
***Who can contribute to further developments and how to get involved?***

#### A.
Chain specifications, operation configurations, chain management Smart Contracts and Smart Contract templates will be made available under open source at GitHub.
evan also releases [DBCP](/docs/how_it_works/services/dbcp.html) (distributed business communication protocol), a toolchain for [Smart Contract](/docs/developers/smart-contracts.html) and [ÐApp](/docs/developers/ui/writing-dapps.html) specifications under open source. With these library developers can describe in a manifest a ÐApp and how it works together with security, role models, name service.


#### Q.
***Is it possible for third parties to implement software modules to add further features around the core application?***

#### A.
It's not only possible but very welcomed and intended. The evan.network is an open platform to create distributed application. The network is open to everyone to create and use Smart Contracts and [ÐApps](/docs/developers/ui/writing-dapps.html).

#### Q.
***What is the path to access bit44 keys?***

#### A.
The bit44 keys can be accessed using the Keystore library in the [Blockchain Core API](/docs/developers/api/blockchain-core.html) via the hdpathstring `m/45'/62'/13'/7`. The hdpathstring is deconstructed as 'm / purpose' / coinType' / Account' / Chain / addressIndex.

#### Q.
***What are the endpoints in evan.network?***

#### A.
The evan.network currently consist of two [endpoints](/docs/developers/api/endpoints.html) `core-Production Chain` and `testcore-Development Chain`. The RPC endpoint in both cores can be accessed via HTTPs and WebSocket.