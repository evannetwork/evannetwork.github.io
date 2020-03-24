---
title: "Smart Contract Permissioning"
parent: Developers
grand_parent: Concepts
nav_order: 4132
permalink: /docs/developers/concepts/smart-contract-permissioning.html
---

# Smart Contract Permissioning 

Smart contract permissions mostly cover *write* operations against smart contracts. *Read* operations are usually covered with encryption and [Sharings](/docs/developers/concepts/sharings). If you're unsure which of those to use to secure your applications data, have a look at [Smart Contract Security](/docs/developers/concepts/smart_contract_security.html).


## Basic Permissions
Basic permission checks in Smart Contracts verify that the calling user is the owner of the contract. For this approach, the contract inherits from a contract like the owned in ```Core.sol```:
```javascript
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
Contract transactions that should only be used by the contract owner use the ```only_owner``` modifier, for example:
```javascript
contract OwnedStorage is Owned {
    string public data;

    function setData(string newData) public only_owner {
        data = newData;
    }
}
```
can have its storage only be set by the owner.

The ```Owned``` contract provides sufficient permissions for easy contracts or contracts with only one contributor and many consumers, but fails to support different contract structures with different roles.


## Function Permissions
The [Dappsys collection](https://dapp.tools/dappsys/) from [DappHub](https://dapphub.com/) is a bundle of contracts, which solve different common problems contract developers may encounter. Two of those contracts are the [DSAuth](https://dapp.tools/dappsys/ds-auth.html) and the [DSRoles](https://dapp.tools/dappsys/ds-roles.html) contracts, which are used to control contract function access.

If a contract has a function that only a specific scope of users are allowed to use, the contract has to inherit from ```DSAuth```. This adds the ```authority``` property to the contract and allows to use the ```auth``` modifier.

An ```authority``` is a contract that inherits from ```DSAuth```. To use roles for contract permissions, the authority can be an instance of ```DSRoles```. Using this in the previous example, the contract looks like this:

```javascript
contract OwnedStorage is DSAuth {
    string public data;

    function setData(string newData) public auth {
        data = newData;
    }
}
```

The `auth` modifier is used on functions that should be restricted to specific roles and forbids access to them, if the calling identity does not meet the permission requirements.

[![Smart Contract authority](/docs/4000_developers/4100_concepts/img/smart_contract_authority.png){:max-width="50%"}](/docs/4000_developers/4100_concepts/img/smart_contract_authority.png)

This basically forbids almost everyone from using the ```setData``` function, except:
- the contract itself
- the owner of the authority contract
- (if registered) root users
- (if registered) public capabilities (functions can be made public accessible for everyone if required)

Permissions can be granted by:
1. creating a roles contract for the contract and assign it as the authority
2. assigning an identitiy to a role
3. granting this role permission (capability) to a function

```javascript
// sample contract
DSAuth storage = new OwnedStorage();

// create a roles contract for the contract and assign it as the authority
DSRoles roles = new DSRoles();
storage.setAuthority(roles);

// assign an identitiy to a role (role 0 is an owner like role in this example)
roles.setUserRole(msg.sender, 0, true);

// grant this role permission (capability) to a function
roles.setRoleCapability(0, storage, bytes4(keccak256("setData(string)")), true);
```

Passing ```false``` as the last argument revoking permissions.

Authorities are usually set up to be their own authorities, which means that groups (and their members) can be granted permissions to maintain capabilities in the same way.

See [DSRoles documentation](https://dapp.tools/dappsys/ds-roles.html) for details on how to roles and capabilities in Ethereum Smart Contracts.


## Operation Permissions
Function permissions are granted to function signatures and are ```bytes4``` based, note the signature creation from the sample above:
```javascript
bytes4(keccak256("setData(string)"))
```

Operations are `bytes32` hashes that are generated in functions and checked against the authority. As many hashes generated throughout the contract code are ```bytes32``` hashes, operation hashes are combinations of those hashes. For example, the permission hash for adding list entries to the list `sampleList` in a Data Contract is build this way:
```javascript
keccak256(keccak256(keccak256("listentry"), keccak256("sampleList")), keccak256("set"))
```

Looks a bit more confusing than it actually is. If aligned by its hashing steps, it looks like this:
```javascript
keccak256(
  keccak256(
    keccak256("listentry"),
    keccak256("sampleList")
  ),
  keccak256("set")
)
```
So basically, the name `sampleList` is hashed with its type `listentry` and the result is hashed with the operation type `set`.

This hash can then be assigned in the same manner as granting permissions for function hashes:
```javascript
// create hash
bytes32 operation = keccak256(keccak256(keccak256("listentry"), keccak256("sampleList")), keccak256("set"));

// assign the permission to group 0 and address 0
roles.setRoleOperationCapability(0, 0, operation, true);
```

As seen in the example above, permissions are granted to address `0`. An address is passed to the function to keep interface compatibility, but the checks are performed independent from the contract address and a roles authority is created for each contract.

Again, passing ```false``` as the last argument revokes permissions.

See section [Data Contracts](/docs/developers/concepts/data-contract.html) for more example of configurable operations.
