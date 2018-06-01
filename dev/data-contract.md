---
title: "DataContract"
---

# DataContract
The DataContract is secured data storage contract for single properties and lists.

It relies on the [Hybrid Storage](/dev/ipfs#hybrid-storage) concept for data storage and secures its data via contract permissions, sharings and key management described in [Security](/dev/security).

[![data contract](/public/dev/data_contract.png){:max-width="50%"}](/public/dev/data_contract.png)

The DataContract allows to:
- set/update properties
- add/remove list entries
- move entries between lists
- update the contract state (set it to Draft, Active, etc.) that follows a preconfigured workflow
- update consumer states (set it to Draft, Active, etc.) that follows a preconfigured workflow


## Configuring DataContracts
If created on its own, DataContracts cannot do very much. They rely on their authority to check which entries or lists can be used. Basically every imaginable entry name or list name can be used, but before actual data can be stored in it, permissions to do so have to be granted.

Its authority is an instance of the contract `DSRolesPerContract` and created alongside the DataContract, when the factory is called.

Functions are secured in the following manner:
- the contract functions have to be unlocked for each role that should be allowed to use it,
  so if the role "member" wants to add entries to *any* list, this role needs permissions to use the ```addListEntries``` function
- for each property, that should be manipulated, an operation permission for this entry or list has to be granted
- state changes (contract and consumer states) require permissions for a combination of
  + a role that updates the state
  + the current state
  + the target state
- this means that for example a contract member may set the state from the current state "Active" to the state "PendingApproval", and only the owner may set it from "PendingApproval" to "Terminated"
