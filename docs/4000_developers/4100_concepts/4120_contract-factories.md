---
title: "Contract Factories"
parent: Developers
nav_order: 120
permalink: /docs/developers/concepts/contract-factories.html
---

# Contract Factories
## About
Some contracts, like the [DataContract](/docs/developers/concepts/data-contract.html) require a few more steps to be set up during their creation. These steps may depend on each other, so a user creating these contracts would have to wait for the single steps to be completed before being able to work with the contract.

These contracts are created by using contract factories, which offers a few enhancements to the process:
- the overall process is faster - instead of n single transactions only one transaction is performed
- creating contracts becomes cheaper -  overhead is reduced when performed in a single transaction
- it can become safer - if one of the setup steps that follow the contract creation fails, the entire creation process is rolled back and if executed via the evan API, this transaction will not be started (gas is estimated before each transaction and a failing transaction would be detected and prevented)
- factories are deployed to [ENS](/docs/developers/concepts/ens.html) addresses and can be updated without delivering code to each client application


## Usage
### ENS Address
Contract factories that belong to a [Business Center](/docs/developers/concepts/business-center.html) are usually deployed at `${FACTORY_NAME}.factory.${BUSINESS_CENTER_ADDRESS}`, so a factory for tasks in the business center "sample.evan" would be deployed at "tasks.factory.sample.evan".

### Factories and BusinessCenters
If a factory is supposed to create contracts for a [Business Center](/docs/developers/concepts/business-center.html), it has to be registered as a valid factory in that Business Center. Factories register all new contracts they create in the Business Center they belong to, and to be able to do so, they need to be registered at the Business Center as a valid factory.

### Getting Addresses of new Contracts
When creating a contract via factory the address is returned via an event from the factory, so when creating new contracts with factories, an event listener, that watches for those events has to be created beforehand.