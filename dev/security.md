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
roles.setRoleCapability(0, storage, bytes4(keccak256("setData(string)")));
```

See [DSRoles documentation](https://dapp.tools/dappsys/ds-roles.html) for details on how to manage roles and capabilities.


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



