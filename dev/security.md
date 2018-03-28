---
title: "Security"
---
# Security

## About
To ensure that contents stored can be read by all related parties and cannot be read or even manipulated by unrelated parties, the contractus contracts for evan.network utilize multiple security approaches.

These approaches have the following responsibilities:
- prevent undesired contract manipulation
- prevent contract content from being leaded to third parties
- make access to contract content possible without exchanging keys for every different peace of data stored in contracts


## Permissions in Smart Contracts
### Basic Permissions
Basic permission checks in smart contracts verify that the calling user is the owner of the contract. For this approach the contract inherits from a Contract like the Owned in ```Core.sol```:
```solidity
contract Owned {
    address public owner;

    function Owned() {
        owner = msg.sender;
    }

    function transferOwnership(address newOwner) only_owner {
        owner = newOwner;
    }

    // This only allows the owner to perform function
    modifier only_owner {
      assert(msg.sender == owner);
      _;
    }
}
```
Contract transactions that should only used by the contract owner use the ```only_owner``` modifier, for example:
```
contract OwnedStorage is Owned {
    string public data;
    
    function setData(string newData) public only_owner {
        data = newData;
    }
}
```
can have its storage only be set by the owner.

The ```Owned``` contract provides sufficiant permissions for easy contracts or contracts with only one contributor and many consumers, but fails to support different contract structures with different roles.


### Function Permissions
The [Dappsys collection](https://dapp.tools/dappsys/) from [DappHub](https://dapphub.com/) is a bundle of contracts, which solve different common problems contract developers may encounter. Two of those contracts are the [DSAuth](https://dapp.tools/dappsys/ds-auth.html) and the [DSRoles](https://dapp.tools/dappsys/ds-roles.html) contracts, which are used to control contract function access.

If a contract has a function that only a specific scope of users are allowed to use, the contract has to inherit from ```DSAuth```. This adds the ```authority``` property to the contract and allows to use the ```auth``` modifier.

An ```authority``` is basically just a contract that inherits from ```DSAuth```. To use roles for contract permissions, this can be an instance of ```DSRoles```. Using this in the previous example contract looks like this:

```solidity
contract OwnedStorage is DSAuth {
    string public data;
    
    function setData(string newData) public auth {
        data = newData;
    }
}
```

This basically forbids almost everyone from using the ```setData``` function except:
- the contract itself
- the owner of the autority contract
- (if registered) root users
- (if registered) public capabilities (functions can be made public accessible for everyone if required)

Permissions can be granted by:
1. creating a roles contract for the contract and assign it as the authority
2. assigning an account id to a role
3. granting this role permission (capabilitiy) to a function

```solidity
// sampe contract
DSAuth storage = new OwnedStorage();

// create a roles contract for the contract and assign it as the authority
DSRoles roles = new DSRoles();
storage.setAuthority(roles);

// assign an account id to a role (role 0 is an owner like role in this example)
roles.setUserRole(msg.sender, 0, true);

// grant this role permission (capabilitiy) to a function
roles.setRoleCapability(0, storage, bytes4(keccak256("setData(string)")), true);
```

Passing ```false``` as the last argument revokes permissions.

Authorities are usually set up to be their own authorities, which means, that groups (and their members) can be granted permissions to maintain capabilities in the same way.

See [DSRoles documentation](https://dapp.tools/dappsys/ds-roles.html) for details on how to manage roles and capabilities in Ethereum smart contracts.


### Operations Permissions
Function permissions are granted to function signatures and are ```bytes4``` based, note the signature creation from the sample above:
```solidity
bytes4(keccak256("setData(string)"))
```

Operations are bytes32 hashes that are generated in functions and checked against the authority. As many hashes generated throughout the contract code are ```bytes32``` hashes, Operation hashes are combinations of those hashes. For example the permission hash for adding list entries to the list "sampleList" in a DataContract is build this way:
```solidity
keccak256(keccak256(keccak256("listentry"), keccak256("sampleList")), keccak256("set"))
```

Looks a bit more confusing than it actually is, if aligned by its hashing steps, it looks like this:
```solidity
keccak256(
  keccak256(
    keccak256("listentry"),
    keccak256("sampleList")
  ),
  keccak256("set")
)
```
So basically the name "sampleList" is hashed with its type "listentry" and the result is hashed with the operation type "set".

This hash can then be assigned in the same manner as granting permissions for function hashes:
```solidity
// create hash
bytes32 operation = keccak256(keccak256(keccak256("listentry"), keccak256("sampleList")), keccak256("set"));

// assign the permission to group 0 and address 0
roles.setRoleOperationCapability(0, 0, operation, true);
```

As seen in the example above, permissions are granted to address 0. An address is passed to the function to keep interface compatibility, but the checks are performed independant from the contract address and a roles authority is created for each contract.

Again, passing ```false``` as the last argument revokes permissions.

See section "DataContract" for more example for configurable operations.


## Sharings
### About
As the main part of data related to contracts is stored in the distributed filesystem, only references to the DFS are stored in the contract. Contents in the DFS are encrypted with one or more keys specific to the contract instance they belong to.

Contract participants that should be enabled to read and/or write contract content, need to have access to the keys responsible for the contract data (called "data keys" in this context). This is done by maintaing a "sharings" info, which is basically a key store, keeping data keys, grouped by the following criteria:
- **participant** - the contract participant, the key is intended for
- **section** - the section in the contract, which holds encrypted data
- **block** - this annotes the _starting_ point from which on the key is valid

### Key Criteria
#### Data Keys
The creator of a contract creates a data key on contract creation and adds this to the sharings as 'shared with herself/himself'. This key is not stored on the owners side and the owner performs exaclty the same steps to retrieve the data key as all contract participants.

#### Participants
The is no catch-all keyword for sharing encrypted contents with everyone or a similar mechanic. Sharing happens explicitely and directed from the owner to a participant.

When sharing keys with contract participants, the data key is encrypted with the communication key (in short "comKey") between the party sharing the key and the party the key is shared with. This means, that before sharing encrypted contract contents with another party, usually a key exchange has to been made beforehand.

To expose encrypted content to a broader scope without performing a key exchange beforehand, keys can be shared via a scope. This scope has to be known by all participating parties and key that belongs to the scope has to be accessable by all participating parties. An example for a scope can be common business context - like a business center where all participating parties work in.

#### Sections
Typical examples for sections are lists and properties in DataContracts. Each participant gets an entry in the sharings with the section names that are shared with him or her.
Other contracts like AssetContracts or ServiceContracts hold data in applicable properties, to which can be referred in the same manner.

If all contents of a contract are encrypted with the same key, this key can be shared for the section "*", which means all sections. Key retrievals get the section names as an argment and for keys in this manner:

1. check if a section with the same name as requested, has been added to the participants key section, if one exists, use keys from it
2. if no matching section was found, check if this participant has keys for the all section "*", if so, use keys from it

#### Blocks
##### Key lifetimes 
Blocks in sharings signal the starting point from which on this key is valid. So to be able to read data added at a specific block, a participant requires a key shared before or at the same block.
Data added **after** this block can be read by the participant, the data has been shared with. Data added **before** this block cannot be read by this participant through this key.

![mutlikeys](/public/dev/multikeys.png)

Keys are valid until they are replaced by a new one, which is then valid until replaced or indefinitely.

![mutlikeys - lifetime](/public/dev/multikeys_lifetime.png)

This principle is for example used for retrieving keys for decrypting data from lists, where keys might have been updated over time. Taking the example from the last picture, an entry added at block 37 has to be encrypted with the block 20 key. Elements added in or after block 40 use the block 40 key for en- and decryption.

This ensures, that:
- keys can be updated
- old entries stay visible for participants that have been granted access to the old key
- newer entries can only be read by participants that have the current key


##### Zero and Infinity
**Granting** a key starting from block 0, makes this key valid, as any data has been added after block 0. This is used for adding a generic key during contract creation.

**Requesting** a key from block "infinity" by omitting the block argument returns the latest valid key. This can be used when encrypting new data. The timestamp when retrieving this key has to be added to the cryptoInfo to ensure that the data can be decrypted later on.


##### Sharing Keys
When sharing keys with another user the same block number should be used as the original key. So if user A has a key, that is valid starting from block 30 and shares it with user B, the sharing should be made as 'starting from block 30'. This means that user B can read entries added at or after block 30. 
If user B gets the key shared as 'starting from 50' for example this user would not be able to read contents added before this block (even if the key might match the content).


