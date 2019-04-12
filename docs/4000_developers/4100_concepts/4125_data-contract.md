---
title: Data Contract
parent: Developers
nav_order: 125
permalink: /docs/developers/concepts/data-contract.html
---

At the center of the evan network blockchain infrastructure is a small number of predefined contracts and contract
types. Those are created with special Factory Contracts, which set them up with their respective
default permissions and parameters like ENS names.


# The DataContract

The DataContract implements the basic functionality used by all data storing elements in the blockchain.
Lets say you want to write a Ðapp that manages heavy machines, where there are many different independent parties and hands heavy machine may be rented to.

The basic usage pattern is the same in all use cases though:


1\. **Get a DataContract Blockchain Core API Object**

Usually you can just take the one from the initialized Blockchain Core runtime or from the
BusinessCenter defined in your application. Or you just create one for yourself with different configuration options.

Lets assume you just take the default API object.


2\. **Create with proper Factory**

Creating a new DataContract is a simple call of the create method in your `dataContract` API

```js
const newContract = await runtime.dataContract.create(
    // this is the ENS of the contract factory that creates new heavy machine contract instances for your application
    'factory.heavy-machines.evan',

    // the owner account of the heavy machine
    '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d'
    )
```

There are more parameters, but this is the simples case, and for more look into the [blockchain core](https://github.com/evannetwork/api-blockchain-core) documentation.


3\. **Load a Contract**

Loading happens also just like a normal data contract, that have their own [DBCP](/docs/developers/concepts/dbcp.html) description, all you need is the accountID of your deployed contract:

```js
const loadedContract = await runtime.description.loadContract(newContract.options.address);

// should be the same, and both are usable the same
console.log(newContract.options.address == loadedContract.options.address)
```
