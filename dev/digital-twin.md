---
title: "Digital Twin"
---

In this How To we want to show you how you can create a new Digital Twin contract on the evan.network. First you will see how the Twin contract is created via our blockchain api. Afterwards you will see how you can interact with it, like adding specific data and lists of data to it and read the data out of the twin.

You can get the full code of the example [>>HERE<<](https://gist.github.com/S3bb1/70d5fad1afb44f45d79bbb6f70515eff)


# Digital Twin

A digital twin is a unique representation of a real world object in the evan network.
It can hold attributes and any other data about the real world object, and implement operations and tasks concerning
the real world object, all cryptographically secured on the blockchain.


## 1. Setup
First you must have a configured runtime in your javascript code available to create a new digital twin.

To create a runtime, you must do the following steps:
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
  ipfs: {host: 'ipfs.evan.network', port: '443', protocol: 'https'},
  // web3 provider config (currently evan.network testcore)
  web3Provider: 'wss://testcore.evan.network/ws',
};

// initialize dependencies
const web3 = new Web3();
web3.setProvider(new web3.providers.WebsocketProvider(runtimeConfig.web3Provider));
const dfs = new Ipfs({ remoteNode: new IpfsApi(runtimeConfig.ipfs), });

// create runtime
const runtime = await createDefaultRuntime(web3, dfs, { accountMap: runtimeConfig.accountMap, });
```

Please set your "ACCOUNTID" and your "PRIVATEKEY" from your evan.network profile to the config object above.

Now you have a configured runtime, all the following code examples are based on the "runtime" variable in the code above.


## 1. Creating a new Digital Twin

Digital Twins are created via factories deployed on the evan.network. Factories are useful to generate pre configured contracts like digital twins. They create pre configured rights and roles on the twin and they set also the rights for specific roles to add or remove parameters on the twin.

Currently is a Factory deployed on the evan.network to create a "empty" digital twin contract. This Factory creates a digital twin contract with no settable properties and 2 roles, Owner and Member. The Account which creates this contract will automatically be added to the "owner" role.


[![digital twin factory](/public/dev/twin1.png){:max-width="50%"}](/public/dev/twin1.png)

Now we create a new digital twin contract via the runtime api from the blockchain core. We use the "dataContract" api from our runtime module to create a new digital twin contract from the general deployed digital twin factory:

```js


const digitalTwin = await runtime.dataContract.create(
  // this is the ENS of generic test twin factory
  'dt.factory.testbc.evan',
  // your own accountID as the owner
  '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d'
)

console.log(digitalTwin.options.address) // print the newly created address of the digital twin
```

Just change the second parameter of the "create" function to your configured accountid in step 1. Now you have an empty Digital Twin with your accountid as "owner" of this digital twin.

## 2. Set and Get your Digital Twin DBCP description

As mentioned, every digital twin has a [DBCP](https://github.com/evannetwork/dbcp) description that describes it's API, general informations, related resources and a lot more. To know what we can do with a contract, a digital twin in our case, you usually need to load this description and take a look at it.

[![digital twin set dbcp](/public/dev/twin_dbcp.png){:max-width="50%"}](/public/dev/twin_dbcp.png)


```js
const twin_description = await runtime.description.getDescription(reloadedDigitalTwin.options.address)
console.dir(twin_description)
```

Which is null, because we have not provided a dbcp description on contract creation.

To set a description for the contract you must first define it via a JSON object with the must have properties for the DBCP Schema:

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

Set the "accountId" property to your current configured accountid.
This is the a basic desciption, it just fills the required fields, and additionally sets its own ABI.


## 3. Loading a Digital Twin


Once you have set the description, it becomes possible to load contracts into a variable with the easier description API:

```js
const reloadedDigitalTwin = await runtime.description.loadContract('DataContract', digitalTwin.options.address)

// and loading the desciption now possible too
const twin_description = await runtime.description.getDescription(digitalTwin.options.address)
console.dir(twin_description)
// should be the same, and both are usable the same
console.log(reloadedDigitalTwin.options.address == digitalTwin.options.address)
```


## 4. Create your first property within your digital twin
As mentioned in part 1, your created twin has no settable properties at the moment. This is because of the rights and roles architecture. You can enable properties on the digital twin by setting the new property as "writeable" by specific roles to the contract. 

Now we're using the "rightesAndRoles" module from our runtime to allow the "owner" role to set a new property called "testEntry" in the digital twin:

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

With this function we grant the "owner" role to "Set" the "Entry" called "testEntry". By default read operations are always possible


## 5. Set and Get the Property back from your digital Twin
After we granted the permissions for the owner role (where your account is already in) to set a property, we now can add simple JSON files or text to the digital twin property:

```js
const accountId = '0xb00fbeef5a926fa150baeaf04bfd673b056ba83d';
const sampleData = {
  foo: 'bar',
  test: 'value'
}
await runtime.dataContract.setEntry(reloadedDigitalTwin, 'testEntry', sampleData, accountId)
```

Now the JSON will be stored on the IPFS servers of the evan network and the reference from this IPFS file in the digital twin smart contract

[![digital twin add ipfs property](/public/dev/twin_ipfs.png){:max-width="50%"}](/public/dev/twin_ipfs.png)

When you now want to get the value of the property in your digital twin you can run the following code:

```js
const valueEntry = await runtime.dataContract.getEntry(reloadedDigitalTwin, 'testEntry');
console.dir(valueEntry);
// prints:
// {
//   foo: 'bar',
//   test: 'value'
// }
```



## 6. Create a list of values on your digital twin
You can not only create key value pairs in your digital twin to manage data. You can also create lists of data and add and remove new entries. First of all you must also set the rights to add entries to a list in your rights and roles of the contract:

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

Replace also the accountId with your accountId. Now you can also add new entries to the list on the digital twin called "testList"

[![digital twin add ipfs property](/public/dev/twin_ipfs_list.png){:max-width="50%"}](/public/dev/twin_ipfs_list.png)

## 7. Add and Get entries from a list
Listentries are also stored on the IPFS servers of the evan.network and will be added to an array of elements on the digital twin property

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

You can add also multiple values to the list by extending the array in the third parameter. When this operation is done, the entries are finally stored on the IPFS and the digital twin contract.

When you want to get back your list and its entries, you can simply call the "getListEntries" from the dataContract module:

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

## 8. Invite other Users to the digital twin
Now we have a digital twin with values ... but no other can access it because all the data is encrypted. So now we want to share the data with other accounts. Please note that when you want to share data to a other account, you must have already exchanged a secret key via the addressbook dapp of the evan.network.

First we must invite the target user to the digital twin contract:

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

[![digital twin add ipfs property](/public/dev/twin_invite.png){:max-width="50%"}](/public/dev/twin_invite.png)

In the first parameter we're using null when working without business center. When working in a businesscenter scope here you must use ENS domain name of the business center the contract was created in.

With this code line you add the "targetAccount" to your digital twin contract. This is required when in the future the account should also be able to add new entries or setting entries. At the moment he can read all the data of the digital twin but he can't decrpyt the data because he has no key to decrypt it.

When you want to share the key to decrpyt the data, you have to extend the "Sharing" of the digital twin contract.

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

[![digital twin add ipfs property](/public/dev/twin_sharing.png){:max-width="50%"}](/public/dev/twin_sharing.png)

This code snippet first gets the "contentKey" of the digital twin. The contentKey is the key which is used to encrypt all the data stored in the digital twin. This key is normally encrypted with the contract creators private key.

The "addSharing" function adds the sharing for the "targetAccount". When a sharing is added, the communcationKey between the two parties is used to encrypt the "contentKey" and store it on the "sharing" of the contract. 

Because all stored ipfs hashes in the blockchain are also encrypted, you must ensure that the "hashKey" of the contract is also "shared" wit the new account.

Now the added targetAccount can also read the listEntries or Entries in the dataContract too :) Easy eh?

