---
title: "Digital Twins"
parent: Developers
grand_parent: API
nav_order: 4221
permalink: /docs/developers/api/digital-twin-custom.html
---

<!--
  TODO:
    - update references here with updated digital twin api, as soon, as it has "settled"
    - replace images with images, that do not have spell checker hints...
-->

# What is a Digital Twin to begin with?
Machines, cars, products, and people can all be represented with a digital twin.

Digital twins mirror the asset’s or person’s attributes and status on the blockchain. Creating a twin for cars, forklifts, and other assets enables them to report their status to the network in fractions of a second and respond to requests autonomously.

A Digital Twin therefore is a unique representation of a real world object in the evan.network.
It can hold attributes and any other data about the real world object, and implement operations and tasks concerning
the real world object, all cryptographically secured on the blockchain.

Digital twins are implemented as DataContracts (see DataContract in [Smart Contracts](/docs/developers/smart-contracts.html#smart-contract-types)) and share their features like different field types and field security.

The field security allows to use different sharing scopes and keys for its field:

[![DataContract](/docs/4000_developers/4200_api/img/data_contract.png){:max-width="50%"}](/docs/4000_developers/4200_api/img/data_contract.png)

Allowed field types are

- entries
- lists
- mappings (similar to dictionaries/maps)

So a Digital Twin may have a data layout like:

[![DataContract](/docs/4000_developers/4200_api/img/digital-twin-example.png){:max-width="50%"}](/docs/4000_developers/4200_api/img/digital-twin-example.png)

The twins can be used in your business logic as you please, allowing for the construction of even the most complex constellations between machines, individuals and organizations alike.

In this how-to we want to show you, on which way you can create a new Digital Twin contract on the evan.network. First, you will see how the Digital Twin contract is created via our blockchain API. Afterwards, you will see how you can interact with it, like adding specific data and lists of data to it and read the data out of the twin.

You can get the full code of the example [here](https://gist.github.com/S3bb1/70d5fad1afb44f45d79bbb6f70515eff)


## 1. Setup
At first you must have a configured Runtime in your Javascript code available to create a new Digital Twin.

To create a runtime, you must fulfill the following steps:
```js
// require blockchain-core dependencies
const IpfsApi = require('ipfs-api');
const Web3 = require('web3');

// require blockchain-core
const { Ipfs, createDefaultRuntime } = require('blockchain-core');

// configure the runtime object
const runtimeConfig = {
  // account map to blockchain accounts with their private key
  accountMap: {
    'ACCOUNTID':
      'PRIVATE KEY',
  },
  // ipfs configuration for evan.network storage
  ipfs: {host: 'ipfs.test.evan.network', port: '443', protocol: 'https'},
  // web3 provider config (currently evan.network testcore)
  web3Provider: 'wss://testcore.evan.network/ws',
};

// initialize dependencies
const web3 = new Web3(runtimeConfig.web3Provider, null, { transactionConfirmationBlocks: 1 });
const dfs = new Ipfs({ remoteNode: new IpfsApi(runtimeConfig.ipfs), });

// create runtime
const runtime = await createDefaultRuntime(web3, dfs, { accountMap: runtimeConfig.accountMap, });
```

Please set your `ACCOUNTID` and your `PRIVATEKEY` from your evan.network profile to the config object above.

Now you have a configured Runtime and all the following code examples are based on the Runtime variable in the code above.


## 2. Creating a new Digital Twin

Digital Twins are created via Factories deployed on the evan.network. Factories are useful to generate pre-configured contracts like Digital Twins. They create pre-configured rights and roles on the twin and they set also the rights for specific roles to add or remove parameters on the twin.

Currently, there is a Factory deployed on the evan.network to create an 'empty' Digital Twin contract. This factory creates a Digital Twin contract with no settable properties and two roles, owner and member. The account, which creates this contract, will automatically be added to the 'owner' role.

[![Digital Twin factory](/docs/4000_developers/4200_api/img/twin_factory.png){:max-width="50%"}](/docs/4000_developers/4200_api/img/twin_factory.png)

Now we create a new Digital Twin contract via the Runtime API from the blockchain-core. We use the DataContract API from our runtime module to create a new Digital Twin contract from the general deployed Digital Twin Factory:

```js


const digitalTwin = await runtime.dataContract.create(
  // this is the ENS of generic test twin factory
  'dt.factory.testbc.evan',
  // your own accountID as the owner
  '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d'
)

console.log(digitalTwin.options.address) // print the newly created address of the digital twin
```

Simply change the second parameter of the `create` function to your configured account ID in step one. Now you have an empty Digital Twin with your account ID as 'owner' of this Digital Twin.

## 3. Set and Get your Digital Twin DBCP description

As mentioned, every Digital Twin has a [DBCP](https://github.com/evannetwork/dbcp) description that describes its API, general information, related resources and a lot more. To know what you can do with a contract, in our case a Digital Twin, you usually need to load this description and take a look at it.

[![Digital Twin set DBCP](/docs/4000_developers/4200_api/img/twin_dbcp.png){:max-width="50%"}](/docs/4000_developers/4200_api/img/twin_dbcp.png)


```js
const twin_description = await runtime.description.getDescription(reloadedDigitalTwin.options.address)
console.dir(twin_description)
```

It is null, because we have not provided a DBCP description on contract creation.

To set a description for the contract, you must define it via a JSON object with the must-have properties for the DBCP scheme:

```js
const accountId = '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d';
var description = {
    public: {
        name: "Digital Twin Machine XYZ",
        description: "A Digital Twin for machine XYZ",
        author: "evan.network tam",
        dbcpVersion: 1,
        version: "0.0.1"
        abis: {
            own: reloadedDigitalTwin.options.jsonInterface
        }
    }
}
await runtime.description.setDescriptionToContract(reloadedDigitalTwin.options.address, description, accountId);
```

Set the account ID-property to your current configured account ID.
This is the a basic description, it just fills the required fields and additionally sets its own ABI.


## 4. Loading a Digital Twin


Once you have set the description, it becomes possible to load contracts into a variable with the easier description API:

```js
const reloadedDigitalTwin = await runtime.description.loadContract('DataContract', digitalTwin.options.address)

// and loading the desciption now possible too
const twin_description = await runtime.description.getDescription(digitalTwin.options.address)
console.dir(twin_description)
// should be the same, and both are usable the same
console.log(reloadedDigitalTwin.options.address == digitalTwin.options.address)
```


## 5. Create your first property within your Digital Twin
As mentioned in part one, your created twin has no settable properties at the moment. This is because of the rights-and-roles architecture. You can enable properties on the Digital Twin by setting the new property as 'writable' by specific roles to the contract.

Now we're using the `rightsAndRoles` module from our runtime to allow the 'owner' role to set a new property called `testEntry` in the Digital Twin:

```js
// make sure, you have required the enums from rights-and-roles.ts
import { ModificationType, PropertyType } from 'blockchain-core';
const accountId = '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d';
const ownerRole = 0;
await rightsAndRoles.setOperationPermission(
  reloadedDigitalTwin,        // contract to be updated
  contractOwner,              // account, that can change permissions
  ownerRole,                  // role id, uint8 value
  'testEntry',                // name of the object
  PropertyType.Entry,         // what type of element is modified
  ModificationType.Set,       // type of the modification
  true,                       // grant this capability
);
```

With this function, we grant the owner role to set the entry called `testEntry`. By default read operations are always possible.


## 6. Set and Get the Property back from your Digital Twin
After we granted the permissions for the owner role (where your account is already in) to set a property, we now can add simple JSON files or text to the Digital Twin property:

```js
const accountId = '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d';
const sampleData = {
  foo: 'bar',
  test: 'value'
}
await runtime.dataContract.setEntry(reloadedDigitalTwin, 'testEntry', sampleData, accountId)
```

Now the JSON will be stored on the IPFS servers of the evan.network and the reference from this IPFS file will be stored in the Digital Twin Smart Contract

[![Digital Twin add IPFS property](/docs/4000_developers/4200_api/img/twin_ipfs.png){:max-width="50%"}](/docs/4000_developers/4200_api/img/twin_ipfs.png)

When you now want to get the value of the property in your Digital Twin, you can run the following code:

```js
const valueEntry = await runtime.dataContract.getEntry(reloadedDigitalTwin, 'testEntry');
console.dir(valueEntry);
// prints:
// {
//   foo: 'bar',
//   test: 'value'
// }
```



## 7. Create a list of values on your Digital Twin
You are not only able to create key value pairs in your Digital Twin to manage data. You can also create lists of data and add and remove new entries. First of all, you must set the rights to add entries to a list in your rights and roles of the contract:

 ```js
// make sure, you have required the enums from rights-and-roles.ts
import { ModificationType, PropertyType } from 'blockchain-core';
const accountId = '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d';
const ownerRole = 0;
await rightsAndRoles.setOperationPermission(
  reloadedDigitalTwin,        // contract to be updated
  contractOwner,              // account, that can change permissions
  ownerRole,                  // role id, uint8 value
  'testList',                 // name of the object
  PropertyType.ListEntry,     // what type of element is modified
  ModificationType.Set,       // type of the modification
  true,                       // grant this capability
);
```

Replace also the `accountId`-fields with your account ID. Now you can also add new entries to the list on the Digital Twin called `testList`.

[![Digital Twin add IPFS property](/docs/4000_developers/4200_api/img/twin_ipfs_list.png){:max-width="50%"}](/docs/4000_developers/4200_api/img/twin_ipfs_list.png)

## 7. Add and Get entries from a list
List entries are also stored on the IPFS servers of the evan.network and will be added to an array of elements on the Digital Twin property

```js
const accountId = '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d';
const sampleValue = {
  foo: 'sample',
  bar: 123,
};
const sampleValue2 = {
  foo: 'sample2',
  bar: 456,
};
await runtime.dataContract.addListEntries(reloadedDigitalTwin, 'testList', [sampleValue, sampleValue2], accountId);
```

You can also add multiple values to the list by extending the array in the third parameter. When this operation is done, the entries are finally stored on the IPFS and the Digital Twin contract.

When you want to get your list and its entries back, you can simply call the `getListEntries` from the data contract module:

```js
const accountId = '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d';
const listEntries = await runtime.dataContract.getListEntries(reloadedDigitalTwin, 'testList', accountId);
console.dir(listEntries);
// prints:
// [{
//   foo: 'sample',
//   bar: 123,
// },{
//   foo: 'sample2',
//   bar: 456,
// }]
```

## 8. Invite other Users to the Digital Twin
Now we have a Digital Twin with values. Nevertheless, no other user can access it because all the data is encrypted. So now we want to share the data with other accounts. Please note that when you want to share data to another account, you must have already exchanged a secret key via the `addressbook` ƉApp of the evan.network.

First, we have to invite the target user to the Digital Twin contract:

```js
const accountId = '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d';
const targetAccount = '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d';
// invite user to contract
await runtime.dataContract.inviteToContract(
  null,
  reloadedDigitalTwin,
  accountId,
  targetAccount
);
```

[![Digital Twin add IPFS property](/docs/4000_developers/4200_api/img/twin_invite.png){:max-width="50%"}](/docs/4000_developers/4200_api/img/twin_invite.png)

In the first parameter, we're using null when working without Business Centers. When working in a Business Center scope, you must use the ENS domain name of the Business Center the contract was created in.

With this code line you add the `targetAccount` to your Digital Twin contract. This is required when the account should also be able to add new entries or to set entries in the future. At the moment, it can read all the data of the Digital Twin, but it can't decrypt the data because it has no key to decrypt it.

When you want to share the key to decrypt the data, you have to extend the Sharing of the Digital Twin contract.

```js
const accountId = '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d';
const targetAccount = '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d';
// get the content sharing key
const contentKey = await runtime.dataContract.options.sharing.getKey(reloadedDigitalTwin.options.address, accountId, '*');

// share the contract with the user
await runtime.dataContract.options.sharing.addSharing(
  reloadedDigitalTwin.options.address,
  accountId,
  targetAccount,
  '*',
  0,
  contentKey,
);

const hashKey = await runtime.dataContract.options.sharing.getHashKey(reloadedDigitalTwin.options.address, accountId);
await runtime.dataContract.options.sharing.ensureHashKey(reloadedDigitalTwin.options.address, accountId, targetAccount, hashKey);
```

[![Digital Twin add IPFS property](/docs/4000_developers/4200_api/img/twin_sharing.png){:max-width="50%"}](/docs/4000_developers/4200_api/img/twin_sharing.png)

This code snippet first gets the `contentKey` of the Digital Twin. The `contentKey` is the key which is used to encrypt all the data stored in the Digital Twin. This key is normally encrypted with the contract creator's private key.

The `addSharing` function adds the sharing for the `targetAccount`. When a sharing is added, the `communcationKey` between the two parties is used to encrypt the `contentKey` and to store it on the Sharing of the contract.

Because all stored IPFS hashes in the blockchain are also encrypted, you must ensure that the `hashKey` of the contract is also shared with the new account.

Now the added `targetAccount` can also read the `listEntries` or entries in the DataContract too. Not too difficult, right?

