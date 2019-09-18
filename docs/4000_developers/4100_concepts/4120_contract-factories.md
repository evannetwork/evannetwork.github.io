---
title: "Contract Factories"
parent: Developers
grand_parent: Concepts
nav_order: 4120
permalink: /docs/developers/concepts/contract-factories.html
---

# Contract Factories
## About
Some contracts, like the [DataContract](/docs/developers/concepts/data-contract.html) require a few more steps to be set up during their creation. These steps may depend on each other, so a user creating these contracts would have to wait for the single steps to be completed before being able to work with the contract.

These contracts are usually created by using contract factories, which offers a few enhancements to the process:
- it is faster - instead of n single transactions only one transaction is performed
- creating contracts becomes cheaper -  overhead is reduced when performed in a single transaction
- it can become safer - if one of the setup steps that follow the contract creation fails, the entire creation process is rolled back and if executed via the evan API, this transaction will not be started (if executed with the [Blockchain Core API](/docs/developers/api/blockchain-core.html), gas is estimated before each transaction and a failing transaction would be detected and prevented)
- factories are deployed to [ENS](/docs/how_it_works/services/ensnameservice.html) addresses and can be updated without delivering code to each client application


## Usage
### ENS Address
Contract factories that belong to a Business Center are usually deployed at `${FACTORY_NAME}.factory.${BUSINESS_CENTER_ADDRESS}`, so a factory for tasks in the business center "sample.evan" would be deployed at "tasks.factory.sample.evan".

### Factories and BusinessCenters
If a factory creates contracts for a Business Center, it has to be registered as a valid factory in that Business Center. Factories register all new contracts they create in the Business Center they belong to, and to be able to do so, they need to be registered at the Business Center as a valid factory.

For this purpose the owner of a business center can call the function [`registerFactory`](https://github.com/evannetwork/smart-contracts-core/blob/0cff8bf94bb1ce578c702764483a0a33450236c6/contracts/BusinessCenter.sol#L179) at a BusinessCenter, e.g. with:

```typescript
await runtime.executor.executeContractTransaction(
  businessCenter,
  'registerFactory',
  { from: executingAccount },
  factory.options.address,
);
```

This will allow the given factory to call the function [`registerContract`](https://github.com/evannetwork/smart-contracts-core/blob/0cff8bf94bb1ce578c702764483a0a33450236c6/contracts/BusinessCenter.sol#L125) at the BusinessCenter and therefore allow it to automatically add new contracts, the factory created, to the business center.


### Getting Addresses of new Contracts
When creating a contract via factory the address is returned via the [`ContractCreated`](https://github.com/evannetwork/smart-contracts-core/blob/0cff8bf94bb1ce578c702764483a0a33450236c6/contracts/BaseContractFactory.sol#L29) event from the factory, so an event listener, that watches for those events has to be created beforehand.

When using the [Blockchain Core API](/docs/developers/api/blockchain-core.html), the events for retrieving the contract address can be given to a contract function execution as well, as used in [`base-contract.ts`](https://github.com/evannetwork/api-blockchain-core/blob/88105e2ec6eca0ff571019c5e79b57e5bc006b7f/src/contracts/base-contract/base-contract.ts#L127) for example:

```typescript
const contractId = await this.options.executor.executeContractTransaction(
  factory,
  'createContract', {
    from: accountId,
    autoGas: 1.1,
    event: { target: 'BaseContractFactoryInterface', eventName: 'ContractCreated', },
    getEventResult: (event, args) => args.newAddress,
  },
  businessCenterAddress,
  accountId,
  descriptionDfsHash,
  this.options.nameResolver.config.ensAddress,
);
```
