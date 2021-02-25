---
title: "Fork evan.network"
parent: What's evan?
nav_order: 1500
permalink: /docs/whats_evan/fork_evan_network.html
---

# Technical overview creating a fork of evan.network

## Hard Forks

When Partners want to cancel the membership of the ENO but has an existing use case deployed and working on evan.network where the partner wants to take the existing data to his own blockchain network.

It is possible to create a hard fork of the network at a given block by creating a "own" blockchain.

The following steps must be done to create a "fork" of the given network.

evan.network operates fully on OpenEthereum nodes. The wiki with all options can be found [here](https://openethereum.github.io/).

### Create own chain spec

The chain specification contains the information of the "first block" of a blockchain network. This specification can be adjusted to provide additional features to a network.

To create a new fork you must sync the existing blockchain on a local computer to the block where you want to fork the chain.

Download the latest chain spec from the [evan.network GitHub](https://github.com/evannetwork/core-config/blob/master/core.json)

The description of all available configuration properties can be found on the [OpenEthereum wiki](https://openethereum.github.io/Chain-specification).

#### Create new signing account

To "fork" the current chain you have to create a new signing account for the OpenEthereum client. This can be done with the CLI command

```
openethereum --chain PATH/TO/CHAINSPEC account new
```

When executing this command you will be prompted to enter a password for the new signing account

```
Please note that password is NOT RECOVERABLE.
Type password:
Repeat password:
```

When you entered a password for the new account, your new signer address shows up in the command line (e.g. 0x66a4b6f39b4c3e7203ab9caeecbad58d8f29b046)

#### Adjust chain spec

With this new account you can adjust the signing settings for your own fork of the evan.network. Go to your cloned spec.json and edit it with your favorite editor.

from line 7-12 you have the configuration of the AuRa mechanism:

```json
"validators": {
  "multi": {
    "0": { "contract": "0x1000000000000000000000000000000000000001" }
  }
},
```

In this object you can configure the authorities (value of the "multi" object) in the chain at a specific block (key of the "multi" object).

The default chain specification of evan.network includes a smart contract which manages the authorities on the network.

To add a single account as authority add a new entry in the object and set the key to the block number where the client consensus stopped syncing and as value an object with the key "list" and the value to an array with the accounts which should be the new authorities of the network:

```json
"validators": {
  "multi": {
    "0": { "contract": "0x1000000000000000000000000000000000000001" },
    "20000000": { "list": ["0x66a4b6f39b4c3e7203ab9caeecbad58d8f29b046"] },
  }
},
```

This config tells the client that from block 20.000.000 the authorities change from the initial smart contract to a fixed list of accounts.

#### Adjust NetworkID

Every chain has also a specific ID which will be communicated to the network of clients. To not get any syncing issues with the original chain you have to give your network a new unique hex id.

The ID will be defined in the params section of the chain spec:

```json=
"params": {
  ...
  "networkID": "0xC06E",
  ...
}
```

change the networkID to something different and add a "chainID" parameter with the 0xC06E in the object.

```json=
"params": {
  ...
  "networkID": "0xDEADBEEF",
  "chainID": "0xC06E",
  ...
}
```

#### Remove Bootnodes

Because you want your own fork of evan.network your node is not able to sync to the original evan.network bootnodes anymore. You can remove them in the array of `nodes` and you can also add your own nodes (when available) to the array in the spec

#### Adding new authorities

When you want to add new authorities (one or more) to your specification you have to add a new section in your validators list:

```json
"validators": {
  "multi": {
    "0": { "contract": "0x1000000000000000000000000000000000000001" },
    "20000000": { "list": ["0x66a4b6f39b4c3e7203ab9caeecbad58d8f29b046"] },
    "21000000": { "list": [
        "0x66a4b6f39b4c3e7203ab9caeecbad58d8f29b046",
        "0x66a4b6f39b4c3e7203ab9caeecbad58d8f29b047"
        "0x66a4b6f39b4c3e7203ab9caeecbad58d8f29b048"
    ] },
  }
},
```

Then you have to provide the adjusted chainspec.json to all existing and new authorities who are running the OpenEthereum client.

---

With these settings you can start your own fork of evan.network. When you start the OpenEthereum client make sure that you pass your new chain spec:

`openethereum --chain /YOUR/PATH/TO/CHAINSPEC --engine-signer=[NEW SIGNER ADDRESS]`

----

## Authoritynode Contract

### About the Authoritynode Contract

The section "Hard Fork" describes how to create a new chain specification with a new set of authorities on the new chain. In the case you want to manage the allowed authorities (like adding a new account), you have to modify the `chainspec.json` and then distribute it to all authorities on your network. This is not an efficient way to manage a large amount of authorities.

OpenEthereum has the ability to have a smart contract as authority management instance. The detailed documentation is on the [openethereum wiki](https://openethereum.github.io/Validator-Set).

This contract can be deployed on the network and then defined in the chainspec.json as a `safeContract`.

### How it works

On common Proof of Work chains, every client which solves the "calculation puzzle" is able to add a new block to the blockchain. In consortial chains which use the Proof of Authority consensus, only defined clients/accounts are able to add new blocks to the chain. The Authoritynode contract is called whenever a new block arrives at the client. The contact verifies if the issuer of the block is included in the contracts authorities list. If the account is not available in the list, the block will be refused by the client.

This mechanism is called "AuthorityRound". Every authority gets a slot in which he can propose a new block. For example your chain specification defines that every 3 seconds a new block should be created and you have 3 authorities in your spec. The AuRa consensus now allows the following order of block creations:

- Authority 1
- ... 3 Sec
- Authority 2
- ... 3 Sec
- Authority 3
- ... 3 Sec
- Authority 1

All these 3 authorities are allowed to publish a new block when their slot takes place. If they miss their slot (for example a node is offline) then the block will be skipped and the next authority slot creates a new block. In this case it takes 6 seconds until the next block arrives.

The Authoritynode Contract can dynamically manage the list of authorities. The [BaseOwnedSet.sol](https://github.com/evannetwork/smart-contracts-admin/blob/master/contracts/authority/BaseOwnedSet.sol) contains all methods to add/remove new authorities from the contract.

#### Setup on evan.network

On evan.network we deployed a initial set of the contract with 3 authorities. This contract is placed in the chainspec in the section of the `validators` section as `safeContract`.

#### Adding authorities

To add a new authority you have to execute the smart contract function `addValidator` on the authority contract. This function takes 1 address which should be added to the authority list. After executing the transaction, the address is added to the `pending` addresses array in the contract. The OpenEthereum client now takes notice of the change in the Authority contract. The consensus defines that every authority in the current status has to confirm the add of the new authority address. This takes 1 block for every authority. After every existing authority signaled the acceptance of the new authority member, the change will be activated and the pending address is transferred to the `validators` address array and from this point, the new authority address is a validated member which can propose new blocks.

#### Removing authorities

To remove an existing authority you have to execute the smart contract function `removeValidator` on the authority contract. The function takes also 1 address as parameter. The address in the parameter should be removed from the `validators` address array. The procedure is the same like in the `addValidator` function. Every authority must signal the removal of the account to finalize the change of the `validators` array.

If you want to know more about the AuthorityRound contract and the consensus mechanism, visit the OpenEthereum Wiki <https://openethereum.github.io/Validator-Set>

---

## Transaction Permissions

### About Permissions

The [`TransactionPermission`](https://github.com/evannetwork/smart-contracts-admin/blob/f4882bb02732a999e266257076f52e6d49faaf7f/contracts/TransactionPermissionContract.sol) contract is responsible for controlling which users are allowed to perform transactions on the evan.network. It is a permissioning contract build as described in the [OpenEthereum wiki](https://openethereum.github.io/Permissioning.html) and configured in the evan.network [chain spec](https://github.com/evannetwork/core-config/blob/c551046dd78f307c56f529b7fa359f0c13c9c63b/core.json#L22).

On evan.network no sender is allowed to perform any transaction unless permissions have been explicitly granted to it, which happens during onboarding on evan.network upon accepting the terms of use. Those permissions can be revoked in case of misbehavior like unlawful activities. This can be performed by the owner of the contract, like a ENO controlled wallet.

### How it works

Every transaction that should be included in a block is checked for its validity against the `allowedTxTypes` function.

The owner of the contract is allowed to perform all transactions. Every other sender needs either specific permissions assigned to him or her or the transaction falls into the scope of the `minimumPermission` property. For example calling contracts might be allowed in `minimumPermission` but creating contracts might require higher level of permissions assigned to the sender of a transaction.

### Transaction Permissions Setup on evan.network

One might be wondering why the [default value](https://github.com/evannetwork/smart-contracts-admin/blob/f4882bb02732a999e266257076f52e6d49faaf7f/contracts/TransactionPermissionContract.sol#L34) in the transaction permission contract is defined as `ALL`, because this would mean that every sender can perform all transactions. This was indeed the case during migration, when this permissioning system had been introduced, but if you check `minimumPermission` on evan.network, you'd get the value `0` as the result. Therefore transactions are disabled for all new accounts and enabled for every single user after accepting the terms of use.

### Managing the Transaction Permissions Contract

The owner of the contract can use the following flags to control allowed transaction types per address on evan.network:

```solidity
    uint32 public constant NONE = 0;
    uint32 public constant ALL = 0xffffffff;
    uint32 public constant BASIC = 0x01;
    uint32 public constant CALL = 0x02;
    uint32 public constant CREATE = 0x04;
    uint32 public constant PRIVATE = 0x08;
```

These permissions are then combined into a bitmask that represents an accounts permissions, e.g. `BASIC` and `CALL` might be combined as `BASIC | CALL`, which would result in `0x03` as the value for an accounts permission bitmask.

Those masks can be passed to

- `grantPermission`: adds certain permissions to an accounts current permission setup
- `revokePermission`: removes certain permissions from an accounts current permission setup
- `setPermission`: overwrites a users permission setup with given bitmask
- `setMinimumPermission`: defines the basic permissions for all users as the given bitmask

### Service Transactions

Accounts can be configured as service accounts, which are allowed to perform transactions without paying for the gas costs in the transactions. Such transactions have to include gas like regular transactions but the gas price is set to `0`. This feature is currently used by the onboarding smart agent for creating new users profiles and allowing them to perform transactions via the `TransactionPermissionsContract`.

Which users are allowed to perform service transactions is controlled by the `service_transaction_checker` certifier, see [Gas Price](https://openethereum.github.io/Permissioning.html#gas-price) in the OpenEthereum wiki.

---

## BridgeContract

### About Blockrewards and Bridge Contract

In Ethereum based chains normally every "miner" or "validator" of a block gets a reward in form of native coins. On Proof of Authority chains based on OpenEthereum it is also possible that you not give any rewards to the authorities, instead a smart contract can manage the "minting" of these coins and can send these to the receivers on the network. On evan.network the coins are called EVEs and can be bought through a web UI via credit card or receipt. When the network received a payment by the payment provider, it triggers a transaction to the "BlockRewardContract" and this contract is called like the AuthorityRound Contract also every new block and checks if any "minting" must be done.

### How it works

The [`BlockReward.sol`](https://github.com/evannetwork/smart-contracts-admin/blob/master/contracts/BlockReward.sol) contract is defined in the chainspec.json file in the authorityround params section:

```json
    "authorityRound": {
      "params": {
        ...
        "blockRewardContractAddress": "0x1000000000000000000000000000000000000002",
        "blockRewardContractTransition": "0x0"
      }
    }
```

With the parameter `blockRewardContractAddress` you can define the address where the blockreward contract is deployed.

With the parameter `blockRewardContractTransition` you define the blocknumber (as hex value) from which block number on the contract should be responsible for the payouts/minting of the coins.

### Creating a payout

The contract itself has one main function which can be called from the owner of the contract (which can be either a single Ethereum address or a multi sig wallet).

The main function is called `addExtraReceiver` which takes two arguments

- `_amount` - a uint256 which defines the to be generated coin amount
- `_receiver` -  a address of an account which should receive the amount of coins

The amount is defined in WEI (the smallest amount of Ethereum). As a example 1 EVE is equivalent to 1000000000000000000 Wei so if the contract should generate 101 EVE for account `0xB88E14514C8b5983EDBAB3c33534b75911eae302` you have to pass `101000000000000000000` as `_amount` parameter and `0xB88E14514C8b5983EDBAB3c33534b75911eae302` as `_receiver` parameter.

The minting is then done in the next block which is included in the blockchain.

### Getting different payout information

The BlockReward contract provides also several getters which give you more information about the amounts generated with the contract:

- `mintedForAccount(address _account)` - gives you the whole amount minted for a specific address
- `mintedForAccountInBlock(address _account, uint256 _blockNumber)`- gives you the amount minted for a specific address in a specific block number
- `mintedInBlock(uint256 _blockNumber)` - gives the whole amount minted in a specific block number
- `mintedTotally()` - gives you the whole amount minted from this contract

---

## ENS usage

### About

The ENS (Ethereum Name Service) is used throughout evan.network to store and access human readable address names (e.g. `'profile.factory.evan'`) and resolve them into technical contract addresses or data (e.g. `'0xFEd281e8433Ca7B92333347C9a3D46545319a8ff'`).

ENS service on evan.network is build upon the well known [ENS service](https://docs.ens.domains) with a few additions:

- storing data on addresses
- time limited addresses, buyable by evan.network users

### Storing data on addresses

This follows the implementation [guidelines for resolvers](https://docs.ens.domains/contract-developer-guide/writing-a-resolver) but for clarification, keep the following things in mind:

- The data is not actually stored as binary data. `content` contains a `bytes32` representation of an IPFS hash pointing to evan.network IPFS.
- To shorten the `base58` IPFS hash, it is converted to a `Byte` array and the leading two Bytes with the multihash id are dropped. This reduces the length to 32 Bytes, which can be stored via ENS.
- Utilizing this approach, ENS addresses can be equipped with descriptive information on how to use the contract referenced in the address, for example with a [DBCP](https://github.com/evannetwork/dbcp) description. Dapps are usually stored as [DBCP](https://github.com/evannetwork/dbcp) description and most often do not have an underlying contract, so `addr` for this ENS address is `0x` in these cases.

### Timed ENS

Whoever deploys an ENS infrastructure on a chain, usually owns the addresses assigned to it, at least initially.

As a structure like this would not allow partners to roll out own contracts with easy-to-use addresses and deploy their own business logic dapps on the chain in usable way, other participants should be allowed to own their own address domains (e.g. `'partner123.evan'`). One approach would be to let them request the domains they want from the original deployer and this instance then assigns domains to the respective partners. This would work, but it is also a perfect use case for smart contracts that can handle the management of these domains.

Therefore the ownership of the domain `'.evan'` has been transferred to [`PayableRegistrar`](https://github.com/evannetwork/smart-contracts-core/blob/eff445aec0c76f810f9ebb7bab2513c652d4795f/contracts/PayableRegistrar.sol) smart contract. Only this smart contract is now able to assign ownership of subdomains of `'.evan'`, like the previously mentions `'partner123.evan'`. This can be done _time limited_ by any network use or  _permanently_ by the owner of the registrar.

See section "Addresses on evan.network" for the address of the registrar, ens and well known ENS addresses on evan.network.

#### Time Limited Addresses

To get access to a time limited address, a user can call the [`register`](https://github.com/evannetwork/smart-contracts-core/blob/eff445aec0c76f810f9ebb7bab2513c652d4795f/contracts/PayableRegistrar.sol#L72) function of the registrar.

Time limited domains **and their subdomains** cannot be resolved after their expiration time has been reached. The exact time window depends on the registrar (see below) and the ENS, that resovles the addresses. On evan.network we use [`TimedENS`](https://github.com/evannetwork/smart-contracts-core/blob/eff445aec0c76f810f9ebb7bab2513c652d4795f/contracts/TimedENS.sol) for this. By default, domains are valid for 52 weeks and the TimedENS allows resolval up to 8 weeks after the expiration time has been reached, can be checked by calling `validPostExipireWindow` on the TimedENS.

Consider the following things when registering new subdomains:

- The `label` argument is a `keccak256` hash of the subdomains label. For example if a user wants to register `'partner123.evan'`, this is then hash of `'partner'` ('`0x988189638926a160e48a2550e7a8b2e45071f9193f3aeff6387adb9942eeccd6`').
- The `owner` argument is the new owner of the subdomain. Usually this is the address of the caller.
- Note that the function is `payable` and the correct fee for registering new subdomains has to be sent with the transaction. The fee can be checked by calling `price` at the registrar.
- The addresses are by default limited to 52 weeks, the time frame can be checked by calling `validDuration` at the registrar.
- The lifetime of addresses can be extended by calling `register` again. Note that this can only be done in a certain time window ahead of expiration. This time window is 8 weeks ahead and can be checked by calling `validPreExipireWindow` at the registrar.

#### Permanent Addresses

The owner of the registrar can also call [`registerPermanent`](https://github.com/evannetwork/smart-contracts-core/blob/eff445aec0c76f810f9ebb7bab2513c652d4795f/contracts/PayableRegistrar.sol#L110) to set subdomains that do not expire without funds. The same notes about the arguments from above apply here as well.

#### Notes about managing PayableRegistrar and TimedENS

The owner of the registrar can perform administrative tasks on the registrar as well, this includes:

- Setting a new price for the `register` function with `setPrice`.
- Defining new time windows for address expiration with `setValidDuration`.
- Defining new time windows for renewing ownerships of addresses with `setValidPreExipireWindow`.
- Withdrawing accumulated funds from registered addresses with `claimFunds`.

The owner of the timed ENS can define how long after its expiration an ENS address can be resolved with `setValidPostExipireWindow` at the TimedENS.

---

## MultiSig wallets

### About

Multisig wallets are a mechanism to allow multiple parties to act as a single entity on the chain. This entity is the Multisig wallet and the accounts controlling it can act as this wallet.

When using wallets, usually transactions are delegated through wallets. Therefore instead of calling a contract directly, a transaction is made against the wallet and the wallet then calls the other contract.  Smart contracts which have technically one owner, can be controlled by multiple owners, when ownership is assigned to a wallet and the wallet is controlled by multiple parties. Depending on the setup of the wallet, transaction can be made by any party or an agreement of multiple or all wallet owners may be required before such a transaction can be made.

This allows to build important scenarios on evan.network like multi-party ownership of central contracts like the transaction permission contract. A good example is the usage of the `TransactionPermission` contract. This contract is owned by such a wallet and all wallet owners are able to grant or revoke transaction permissions if required.

The implementation for the MultiSig wallet used on evan.network can be found [here](https://github.com/evannetwork/smart-contracts-core/blob/eff445aec0c76f810f9ebb7bab2513c652d4795f/contracts/MultiSigWallet.sol).

### Types of MultiSig Wallets on evan.network

- [`MultiSigWalletSG`](https://github.com/evannetwork/smart-contracts-core/blob/79b923d87400f10c65848fc055a7044d1ff70178/contracts/MultiSigWalletSG.sol) - a self governed (hence the "SG") wallet where all owners of the wallet can execute transaction with the wallet and configure it
- [`MultiSigWallet`](https://github.com/evannetwork/smart-contracts-core/blob/79b923d87400f10c65848fc055a7044d1ff70178/contracts/MultiSigWallet.sol) - a wallet that has a single "admin" like owner that can configure the wallet and all owners can make transactions with it
- [`VerificationHolder`](https://github.com/evannetwork/smart-contracts-core/blob/79b923d87400f10c65848fc055a7044d1ff70178/contracts/verifications/VerificationHolder.sol) and its inherited wallet logic implementation from [KeyHolder](https://github.com/evannetwork/smart-contracts-core/blob/79b923d87400f10c65848fc055a7044d1ff70178/contracts/verifications/KeyHolder.sol) - used as primary identities on evan.network

### Using the Wallets

#### MultiSigWalletSG

##### User Management

Adding and removing users can be done pretty straight forward with `addOwner`, `removeOwner` and `replaceOwner`.

Note that `removeOwner` will also reduce the required number of confirmations for a wallet transaction if it would exceed the number of owners left in the wallet.

##### Transaction Handling

To execute transactions via a wallet, call the `submitTransaction` on your wallet. The arguments are as following:

- `destination` - a contract the wallet should call or an address funds should be transferred to
- `value` - amount of Wei to send to `destination`
- `data` - an [ABI byte string](https://docs.soliditylang.org/en/latest/abi-spec.html) for transaction, usually consists of contract function hash and encoded input data

If the required number of confirmations in the wallet is set to `1`, the transaction will immediately be executed. If not, the id of the submitted transaction has to be taken from the `Submission` event and confirmed by the required number of owners. For this they can use the `confirmTransaction` function, which takes the transaction id as its argument. As soon as the required number of confirmations has been reached, the transactions is submitted.

Keep in mind, that executing transactions is more expensive, the larger the `data` part is. `data` is stored in the wallet contract and is used as `data` upon execution. This has two implications:

- If the required number of confirmations is larger than `1`, the last confirmation will most probably have much higher transaction costs than the other confirmations, as this is the transaction where the wallet will actually perform the transaction, the confirmations were collected for.
- Creating contracts via wallet is usually two times as expensive, compared to creating the same contract directly. The reason for this is that in such transactions the entire byte data of the smart contract is stored twice: One time at the wallet and upon execution a second time for the new contract.

##### Confirmations

The contract member `required` reflects the required number of confirmations before a transaction submitted to the wallet is executed. Depending on the scenario different values might be used for the number of confirmations:

- act on behalf: Setting `required` to `1` allows any owner to act on behalf of the wallet.
- ballot: Setting `required` to desired number or even to the same number as the number of owners allows to collect confirmations for the transaction form multiple participants before submitting the transaction.

The number of required transactions can be checked by calling `required` on the wallet. It can also be configured by using `changeRequirement` to set a new value.

#### MultiSigWalletSG

Works like the `MultiSigWallet` wallet except that the wallet can only be managed by the administrative account of the wallet. This account can be checked by calling `owner`, ownership can be transferred with `setOwner`.

The following functions can only be used by the administrative account:

- `changeRequirement`
- `addOwner`
- `removeOwner`
- `replaceOwner`

#### VerificationHolder aka "Identity"

Every user receives an instance of `VerificationHolder` during onboarding and usually performs transactions through it and DIDs and DID documents are bound to this. Therefore it is usually just called "identity". Other users may be granted permissions to act on behalf of this identity (make transactions through it) as well.

These identities are based on [ERC725 v1](https://github.com/ethereum/EIPs/issues/734) and [ERC735](https://github.com/ethereum/EIPs/issues/735).

##### User Management

User management is key based in [`VerificationHolder`](https://github.com/evannetwork/smart-contracts-core/blob/79b923d87400f10c65848fc055a7044d1ff70178/contracts/verifications/VerificationHolder.sol) as it inherits from [`KeyHolder`](https://github.com/evannetwork/smart-contracts-core/blob/79b923d87400f10c65848fc055a7044d1ff70178/contracts/verifications/KeyHolder.sol). Users (addresses on evan.network) may hold one or multiple keys in an identity, the owner for example holds the keys `MANAGEMENT_KEY` and `ACTION_KEY`.

Keys are usually `keccak256` hashes of account addresses. These keys may have one or multiple purposes (similar to the account having certain roles). Multiple functions for managing keys are offered in the [`KeyHolder`](https://github.com/evannetwork/smart-contracts-core/blob/79b923d87400f10c65848fc055a7044d1ff70178/contracts/verifications/KeyHolder.sol) smart contract, with the following functions being the most important ones:

- `keyHasPurpose` - Used to check if a certain key has a certain purpose. Default purposes can be found in [`ERC725.sol`](https://github.com/evannetwork/smart-contracts-core/blob/79b923d87400f10c65848fc055a7044d1ff70178/contracts/verifications/ERC725.sol). The most important ones here are the `MANAGEMENT_KEY` (allows to configure the identity) and the `ACTION_KEY` (allows to perform transaction with the identity)
- `addKey` - adds a key with given purpose and type (`ECDSA`, `RSA`, ...)
- `removeKey` - removes a given purpose from a key, if this was the only purpose, the entire key is removed

##### Transaction Handling

Accounts with the `ACTION_KEY` key are allowed to call `execute` to execute a transaction via wallet. The arguments are similar to the arguments described in `MultiSigWalletSG`:

- `_to`- a contract the wallet should call or an address funds should be transferred to
- `_value` - amount of Wei to send to `_to`
- `_data` - an [ABI byte string](https://docs.soliditylang.org/en/latest/abi-spec.html) for transaction, usually consists of contract function hash and encoded input data

It is also possible to let an unrelated account execute a contract transaction. For this the function `executeDelegated` can be used. This function has the same arguments plus `_signedTransactionInfo`, which is a signed hash of the transaction details. The signer has to hold an `ACTION_KEY` in the identity. This allows to prepare transactions and let another account execute the transaction and pay for it, without granting the paying account any undesired privileges in the identity while having zero gas cost on the side of the signing account.

##### Confirmations

Even if not used broadly, the `execute` function can be used to prepare transactions and confirm them later on by any account with the `ACTION_KEY`. Group based decision making cannot be build with this setup as the first account with the `ACTION_KEY` will execute the transaction. To prepare a transaction this way, call `execute` with an account **without** the `ACTION_KEY` and grab the execution nonce from the `ExecutionRequested` event. Then call `approve` with an account **with** the `ACTION_KEY` and the nonce from before to execute the transaction.

---

## Onboarding Agent

### Onboarding of new Users

The onboarding agent is primarily used to help new users get started on evan.network. This includes

- creating a profile and an identity on evan.network for the new user
- storing that the terms of use have been accepted
- allowing the new user to perform transactions on evan.network
- opening a payment channel to allow the new user to store files on evan.network IPFS
- (on testcore) provide some initial funds to start working on evan.network

#### Onboarding Flow

When a user onboards via the [, a seed phrase is generated for the user and the user uses it to generate a local Ethereum account for evan.network. This account is then used to sign a message that is sent to the server to prove the ownership over the new account.

Then the user calls the endpoint `smart-agents/profile/create` and the server creates the user identity setup on even network, which primarily consists of the following components:

- an identity contract, see "VerificationHolder" in section "MultiSig wallets"
- a profile digital twin to hold user related data, create with the [`ProfileDataContractFactory`](https://github.com/evannetwork/smart-contracts-admin/blob/f4882bb02732a999e266257076f52e6d49faaf7f/contracts/ProfileDataContractFactory.sol)

After this the use can prepare data to be inserted into the profile digital twin and encrypts it locally. The encrypted data is then sent to the `smart-agents/profile/fill` endpoint, which then continues with the onboarding steps:

- user data is inserted into the digital twin
- the server creates two verifications to proof that the terms of use have been accepted by the user
  - `'/evan/onboarding/termsofuse'` - terms of use have been accepted
  - `'/evan/onboarding/termsofuse-${ termsOfUseOrigin }'` - version of the terms of use that has been accepted
- a payment channel is opened for the user to allow storing files in IPFS
- the profile digital twin is finally handed over to the user and the server is removed from its permissions

### Faucet

The onboarding agent also allows to hand out funds on evan.network testcore to allow easier developing on the test environment. For this the `smart-agents/faucet/handout` endpoint can be used.

A Gitter based chatbot can also be configured to handout funds via Gitter chats.

Handing out funds is time gated depending on the configuration and is only done on testcore.

### Terms of Use

Terms of use may change over time and the users consent has to be renewed as well. To be able to do so, the latest terms of use can be fetched with the `smart-agents/faucet/terms-of-use/get` endpoint.

The user can then accept it and call the `smart-agents/faucet/terms-of-use/accept` endpoint to signal approval. The agent then issues then updated terms of use verifications for the terms of use:

- `'/evan/onboarding/termsofuse'` - terms of use have been accepted
- `'/evan/onboarding/termsofuse-${ termsOfUseOrigin }'` - version of the terms of use that has been accepted

---

## IPNS Key Management

The evan.network dashboard and APIs are written in JavaScript to be displayed in the browser. To use the full power of decentralization, the JavaScript APIs and the dashboard UIs are hosted on a private IPFS network.

The nature of IPFS is that when you upload a file to IPFS you receive a unique Hash of the file as result. Now if you change a single character in the file and upload it again you receive a new unique hash of the file.

This turns out negative when you have a static website which should load always the latest JavaScript API in the browser.

IPFS provides a feature called IPNS (Interplanetary Name Service) where you can register fixed Hashes and map them to an existing IPFS Hash.

Every IPNS resolvable hash is controlled by a key. You can generate a new key on the IPFS node with the command:

`ipfs key gen MyKeyName`

This returns the public key of your generated key

`> k51qzi5uqu5dh5kbbff1ucw3ksphpy3vxx4en4dbtfh90pvw4mzd8nfm5r5fnl`

with your new generated key you can now publish a given IPFS hash (of your document) to a fixed key in the IPNS namespace

`ipfs name publish --key=MyKeyName /ipfs/QmUVTKsrYJpaxUT7dr9FpKq6AoKHhEM7eG1ZHGL56haKLG`

The command above publishes the IPFS hash `QmUVTKsrYJpaxUT7dr9FpKq6AoKHhEM7eG1ZHGL56haKLG` with your created key to a fixed name.

`> Published to k51qzi5uqu5dh5kbbff1ucw3ksphpy3vxx4en4dbtfh90pvw4mzd8nfm5r5fnl: /ipfs/QmUVTKsrYJpaxUT7dr9FpKq6AoKHhEM7eG1ZHGL56haKLG`

Now you can resolve your document from the given ID

```
curl https://gateway.ipfs.io/ipns/k51qzi5uqu5dkkciu33khkzbcmxtyhn376i1e83tya8kuy7z9euedzyr5nhoew
```

IPNS names expire after a certain time. To fix this you can generate a bash script which runs the `name publish` command every 20 minutes

```bash
while :
do
  ipfs name publish --key=MyKeyName /ipfs/QmUVTKsrYJpaxUT7dr9FpKq6AoKHhEM7eG1ZHGL56haKLG
  sleep 1200
done
```

Now your IPNS name is resolvable forever. If your IPFS hash changes (due to update of the code or smth. else) simply change the hash in the script and restart it.

If you want to know more about IPNS, go to the official [IPFS documentation](https://docs.ipfs.io/concepts/ipns/#interplanetary-name-system-ipns).
