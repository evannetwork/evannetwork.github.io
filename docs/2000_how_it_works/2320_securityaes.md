---
title: "Security"
parent: How it works
nav_order: 2320
permalink: /docs/how_it_works/securityaes.html
---

## Security

The core technology of the evan.network is based on the Ethereum blockchain technology. The protection of transactions against manipulation is an essential element of this technology. This requires that the contents of the Smart Contracts can be read, interpreted and verified by all network partners (e.g. AuthorityNodes) in the blockchain, which represents a significant hurdle in the B2B adaptation of blockchain technology.

The evan.network therefore implements a hybrid storage concept that offers transaction and data security at the same time. All user data are encrypted (AES 256bit/CBC), stored in a distributed file system (IPFS) belonging to the network and referenced from the Smart Contract. This ensures that the actual content is only visible and usable for third parties, if they are invited into a contract and thus have an authorization for the respective data.


Each user receives a public and a private key at his or her first registration. These keys are used to establish communication (Diffie Hellman) with other users and Smart Contracts.

For the interaction within a specific business relationship, additional key pairs (public / private) are created, which only apply to the specific business relationship and the Smart Contract used there. This means that Smart Contracts and the contract contents can be assigned with access rights very flexible. This makes it possible, for example, to determine which parts of a Smart Contract a network partner may read or edit.

In addition, references and keys for data stored outside the blockchain can be stored within the Smart Contract. For example, cloud storage or IoT data streams can be referenced and access to them securely managed.
