---
title: "Taskboard"
---

# Taskboard Example
Work in progress...

This section will show an example how to create a Taskboard [ÐAPP](/dev/dapp) by
- creating a [factory](/dev/contract-factories) for task contracts
- creating a standalone ÐAPP, that can be used to interact with the contract


## Configuring the Factory
This section describes how to setup a [factory](/dev/contract-factories) for using the [DataContract](/dev/data-contract) as a TaskList contract. An implementation that follows this schema can be found in the ```TaskDataContractFactory.sol``` contract.

- owner of a task contract should be able to add ToDos ("todos")
    ```
    roles.setRoleOperationCapability(
        ownerRole, 0, keccak256(keccak256(
        dc.LISTENTRY_LABEL(),
        keccak256("todos")), dc.SET_LABEL()), true);
    ```

- member in the contract should be able to add logs about the ToDos ("todologs")
    ```
    roles.setRoleOperationCapability(
        memberRole, 0, keccak256(keccak256(
        dc.LISTENTRY_LABEL(),
        keccak256("todologs")), dc.SET_LABEL()), true);
    ```

- a set of metadata for the task has to be saved at the contract by the owner
    ```
    roles.setRoleOperationCapability(
        ownerRole, 0, keccak256(keccak256(
        dc.ENTRY_LABEL(),
        keccak256("metadata")), dc.SET_LABEL()), true);
    ```

- to be able to use the appropriate contract functions, these permissions have to be granted for the contract functions as well:
    - owner has to be able to set entries
    ```roles.setRoleCapability(ownerRole, 0, bytes4(keccak256("setEntry(bytes32,bytes32)")), true);```
    - member (which includes the owner per default) have to be able to add list entries
    ```roles.setRoleCapability(memberRole, 0, bytes4(keccak256("addListEntry(bytes32,bytes32)")), true);```

- the owner should be allowed to update the contract state from Intial to Draft, then to Active and then to Terminated, so contract states are configured as:
    ```
    roles.setRoleOperationCapability(
        ownerRole, 0, keccak256(keccak256(
        dc.CONTRACTSTATE_LABEL(),
        BaseContractInterface.ContractState.Initial),
        BaseContractInterface.ContractState.Draft), true);
    roles.setRoleOperationCapability(
        ownerRole, 0, keccak256(keccak256(
        dc.CONTRACTSTATE_LABEL(),
        BaseContractInterface.ContractState.Draft),
        BaseContractInterface.ContractState.Active), true);
    roles.setRoleOperationCapability(
        ownerRole, 0, keccak256(keccak256(
        dc.CONTRACTSTATE_LABEL(),
        BaseContractInterface.ContractState.Active),
        BaseContractInterface.ContractState.Terminated), true);
    ```

- members can update their own status from Draft to Active or Rejected and from Active to Terminated, so the own-state config looks like:
    ```
    roles.setRoleOperationCapability(
        ownerRole, 0, keccak256(keccak256(
        dc.CONTRACTSTATE_LABEL(),
        BaseContractInterface.ContractState.Initial),
        BaseContractInterface.ContractState.Draft), true);
    roles.setRoleOperationCapability(
        ownerRole, 0, keccak256(keccak256(
        dc.CONTRACTSTATE_LABEL(),
        BaseContractInterface.ContractState.Draft),
        BaseContractInterface.ContractState.Active), true);
    roles.setRoleOperationCapability(
        ownerRole, 0, keccak256(keccak256(
        dc.CONTRACTSTATE_LABEL(),
        BaseContractInterface.ContractState.Active),
        BaseContractInterface.ContractState.Terminated), true);
    ```

- after the roles instance is set as the authority in the DataContract, the owner cat add new tasks with ```addListEntry(keccak256("todos"), value)``` and member can add logs about the tasks via ```addListEntry(keccak256("todologs"), value)```
