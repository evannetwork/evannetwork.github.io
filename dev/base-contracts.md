---
title: "Base Contracts"
---

At the center of the evan network blockchain infrastructure is a small number of predefined contracts and contract
types. Those are created with special Factory Contracts, which set them up with their respective
default permissions and parameters like ENS names.

# The DataContract
The DataContract implements the basic functionality used by all data storing elements in the blockchain.
Lets say you want to write a Ðapp that manages beer kegs in a festival, where there are many different independent parties and hands such a keg passes through.

The basic usage pattern is the same in all use cases though:

1\. **Get a DataContract Blockchain Core API Object**  
Usually you can just take the one from the initialized Blockchain Core runtime or from the
BusinessCenter defined in your application. Or you just create one for yourself with different configuration options.

Lets assume you just take the default API object.


```js
const dataContractAPI = blockchainCoreRuntime.dataContract;
```

2\. **Create with proper Factory**

Creating a new DataContract is a simple call of the create method in your `dataContractAPI`


```js
const new_contract = dataContractAPI.create(

    // this is the ENS of the contract factory that creates new beer contract instances for your application
    'beerkeg.beer-festival.evan',
    
    // the owner account of the beer keg
    // there are so many different breweries or logistic companies that own the keg
    
    '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d'
    
    )
```

There are more paramters, but this is the simples case, and for more look into the [blockchain core](/blockchain_core) documentation.

3\. **Load a Contract**
Loading happens also just like a normal data contract, that have their own dbcp desciption, all you need is the accountID of your deployed contract:

```js

const loaded_contract = await blockchainCoreRuntime.description.loadContract(new_contract.options.address);

// should be the same, and both are usable the same
console.log(new_contract.options.address == loadded_contract.options.address)
```



# The Profile

This is the first DataContract you create. And it is created automatically for you when you first join
evan.network.

# Working with the Addressbook

# Working with the Mailbox
