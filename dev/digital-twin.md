---
title: "Digital Twin"
---

# Digital Twin

A digital twin is just a unique representation of a real world object in the evan network.
It can hold attributes and any other data about the real world object, and implement operations and tasks concerning
the real world object, all cryptographically secured on the blockchain.

## Implementation

Fundamentally, a digital twin is just a normal evan.network data contract: something that sits on the blockchain and holds data and data references, and manages how the data and data references are accessed and updated.

# Usage

A digital twin is just a normal [basic data contract](/dev/basic-contracts#the-datacontract) and is used like one.
All you need to do is to use the right factory on creation.

But first lets get a few API references and helpers to save typing:

```js
const dataContractAPI = blockchainCoreRuntime.dataContract;
const contractLoaderAPI = blockchainCoreRuntime.contractLoader;
const descriptionAPI =  blockchainCoreRuntime.desciption;
const executorAPI =  blockchainCoreRuntime.executor;
const rightsAndRolesAPI =  blockchainCoreRuntime.rightsAndRoles;
```
## Creation

Depending on your project you may have deployed your own factories. For general test purposes we have a test twin factory, which will create a new digital twin contract instance, with a few predefined fields and roles and operations.

```js


const new_twin = await dataContractAPI.create(

    // this is the ENS of generic test twin factory
    'dt.factory.testbc.evan',
    
    // your own accountID/profileID as the owner
    '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d'
    
    )
console.log(new_twin.options.address) // print your accountID
```

The new_contract is now a normal web3 contract object and can be used like one, and are also used in our APIs.

## Loading

Loading happens also just like a normal data contract. We didn't set any [DBCP description](https://github.com/evannetwork/dbcp), which usually makes it harder to load contracts, but since a digital twin is just a normal data contract,
which is a core component of evan.network, the ABI is known by the blockchain-core library, and can be used to load the contract.

```js

const loaded_twin = await contractLoaderAPI.loadContract('DataContract' ,new_twin.options.address);

// should be the same, and both are usable the same
console.log(new_twin.options.address == loadded_twin.options.address)

```

Which is null, because we have not provided a dbcp description on contract creation. Always do that if possible.

## Interaction

For now you have only a skeleton contract with no description, a skeleton twin.
It does have a few default entries though. so it's still possible to do things with it:

```js
// if you want to treat it like a normal web3 contract, you do that with the executor
const owner = await executorAPI.executeContractCall(loaded_twin, 'owner')
console.log(owner)
```

The owner is of course the one you provided at creation: yourself.

But since it is a digital twin and an evan.network data contract, there is a far more convenient API.

```js

await dataContractAPI.getEntry(loaded_twin, 'technicalData', owner, false,false).then(console.log)

// output: 0x0000000000000000000000000000000000000000000000000000000000000000
// is an empty hash, because nothing was set

// must be a hash32 string, because we want to store the value directly in the blockchain
const value = '0x0000000000000000000000000000000000000000000000000000000000000003'
await dataContractAPI.setEntry(loaded_twin, 'technicalData', value, owner,
                               false,  // tells the API to store value directly in blockain
                               false   // tells the API to stroe value unencrypted
                               )
```

By default setEntry function stores the values in IPFS and only stores references to IPFS,
and it also encrypts all stored data. For a faster and better displayable example, the last two paramters tell the
API not to do that.

Since `new_twin` and `loaded_twin` point to the same contract instance,
We can read what we just deployed via `new_contract`.

We also have to tell the `getEntry` function, that the data is stored directly in the blockchain, unencrypted.

```js

dataContractAPI.getEntry(new_twin, 'technicalData', owner,
                               false,  // tells the API value directly in blockain
                               false   // tells the API value unencrypted
                               ).then(console.log)
                               
// output: 0x0000000000000000000000000000000000000000000000000000000000000003
```

## More and Larger Entries

It's obviously not good being limited to just the entries that were initialized by the factory. And it is also not good to be limited to data values directly in the blockchain, where they can only be 32bytes at most.

So first lets create the rights to 



```js
// this allows the creation and writing of a new 'parts' list in the contract
rightsAndRolesAPI.setOperationPermission(loaded_contract, owner, 0, 'parts', PropertyType.ListEntry, ModificationType.Set)

// now the owner can write into it

dataContractAPI.addListEntries(loaded_twin, 'parts', 
    [ 
      { name: 'baseplate',
        weight: '1kg',
        width: '100mm',
        length: '100mm',
        height: '5mm' },
      { name: 'coverplate',
        weight: '0.1kg',
        width: '10mm',
        length: '10mm',
        height: '1mm' },
      { name: 'handle', weight: '0.2kg' } ],
      owner)
      
// and lets read it out again

dataContractAPI.getListEntries(loaded_twin, 'parts', owner).then(console.log)

// should write your input list out again
```

The list is of course longer than 32 bytes and thus not stored directly on the blockchain, which is actually
the default behavior (not the missing false parameters at end of the set call). It is far more convenient to do it lijke this, since you can just pass in any ECMAScript type, and the data is encrypted and stored as a json dataset in our distributed file system, and all that is stored on the blockchain is an encrypted reference to the DFS store.

## Descriptions

As mentioned, every digital twin has a [DBCP]() description field that usually describes its API and related resources and a lot more. To know what we can do with a contract, a digital twin in our case, you usually need to load this description and take a look at it.

```js
var twin_description = await descriptionAPI.getDescription(loaded_twin.options.address)
console.dir(twin_description)
```

It's empty of course, because we didn't provide a description. Let's change that.


```js

var description = {
    public: {
        name: "Toy Contract",
        description: "A Toy Contract for Teaching Purposes",
        author: "It'sa meee Maario.",
        dbcpVersion: 1,
        version: "0.0.0.1"
        abis: {
            own: loaded_twin.options.jsonInterface
        }
    }
}

descriptionAPI.setDescription(loaded_twin, description, owner)
```

This is the a basic desciption, it just fills the required fields, and additionally sets its own ABI.
Once you have set this, it becomes possible to load contracts with the easier description API:

```js
const described_twin = await descriptionAPI.loadContract(new_twin.options.address)

// and loading the desciption now possible too
var twin_description = await descriptionAPI.getDescription(loaded_twin.options.address)
console.dir(twin_description)
```

