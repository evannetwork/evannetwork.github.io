---
title: "Smart Contract Security"
parent: Developers
grand_parent: Concepts
nav_order: 4126
permalink: /docs/developers/concepts/smart_contract_security.html
---

# Smart Contract Security

## About Smart Contract Security
Smart contracts are pivotal to everything happening on evan. Almost every feature on the platform utilizes smart contracts in one way or the other. Naturally, security surrounding smart contracts is a top priority on the evan.network.

Since evan.network is an open ecosystem involving many participants, access at times has to be given trans organizational (allowing externals to access internal company data), adding yet another level of complexity.

With that in mind the Smart Contract Security is built around certain main concepts:
- prevent malicious contract manipulation
- prevent contract content from being illegally accessed by third parties
- granularly define access and role definitions

In terms of usability, this mechanism is furthermore designed to make interaction with smart contracts not only secure, but also as swift as possible.


## Aspects of Smart Contract Security
Different actions on evan.network require different permissions to be granted beforehand. Permissions are usually **granted** and not **revoked**, which means that steps have to be performed, before identities can interact with each other.

The following sections will handle the different aspects of security, but to give you a rule of thumb, remember the following points:

- If two identities want to **interact** with each other, be it directly (BMail) or indirectly (work on same contract with encrypted data), they need to perform a [Key Exchange](/docs/developers/concepts/key_exchange). This is a step often performed manually or with an initial account setup script.
- If an identity, that is not the owner of a contract, whats to **read or write** data related to a contract with encrypted data, the owner and this identity  need to exchange dedicated keys for that purpose. This is usually done via the [Sharings](/docs/developers/concepts/sharings) approach. This is often performed during a contracts lifetime, e.g. directly after its creation (if participants are known beforehand) or when a new identity needs access to the contract data.
- If an identity needs to **modify a smart contract**, this identity needs [smart contract permissions](/docs/developers/concepts/smart-contract-permissioning). The most common cases include granting identities permissions to write to properties of a [Data Contract](/docs/developers/concepts/data-contract.html).

| action                   | [Key Exchange](/docs/developers/concepts/key_exchange) | [Sharings](/docs/developers/concepts/sharings) | [contract permissions](/docs/developers/concepts/smart-contract-permissioning) |
| ---                      | :-: | :-: | :-: |
| read unencrypted data    |     |     |     |
| send a BMail             |  x  |     |     |
| share data via contract  |  x  |  x  |     |
| write data to a contract |  x  |  x  |  x  |
{: .evan-flex-table mt-4 }
