---
title: Data Contract
parent: Developers
grand_parent: Concepts
nav_order: 4125
permalink: /docs/developers/concepts/data-contract.html
---

<!--
  TODO:
    - update encryption links
    - update sharing links
-->

# The DataContract
## The "Data" part of "DataContract"
The [`DataContract`](https://github.com/evannetwork/smart-contracts-core/blob/master/contracts/DataContract.sol) combined with its [API](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/data-contract.html) is a container, that is used to hold various types of data and therefore the default data storage for various ÐApps like the [Taskboard](/docs/first_steps/taskboard.html) and even a [user profile](/docs/first_steps/create-identity.html) is based upon it.

Data can be stored under properties - similar to class instance members in object oriented programming, whereby the following property types are supported:

- [**entries**](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/data-contract.html#entries): Basically a single property of the data contract, that holds a value. Entries are used for properties, that are only manipulated by few accounts and that can be overwritten by all parties that have write access.
- [**list entry**](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/data-contract.html#list-entries): List entries are stored - you already guessed it - in lists. Adding list entries and removing are different permissions and a common use case scenario is assigning "add" permissions to different account and keeping remove permissions to few accounts or omitting it entirely. This allows to create an append only list, that can be used as a log. Note, that lists are not necessarily sorted by date. When an entry is removed, the freed up slot is filled with the last element, so delete operations will break the temporal order of the entries. To maintain a list order by date, do not grant the "remove" permission to any role
- [**mapping**](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/data-contract.html#mappings): Similar to an **entry**, as it requires only one permission to be set, but can store values for a key range of 32Bytes. Note that permissions are granted for the entire mapping property and write access for an account means, that this account is able to set values fro the complete 32Bytes key range.

Values are technically stored as 32Bytes values and therefore can store anything, that takes up to these 32Bytes of storage, like Ethereum addresses (20Bytes) or numbers with up to 32Bytes precisions. But in most cases, the 32Bytes are used to store file hashes, which point to a file in a [distributed file system](/docs/how_it_works/ipfs.html). These files are usually [encrypted](/docs/developers/concepts/permissioning.html) and the resulting [file hashes are encrypted](/docs/developers/concepts/permissioning.html) themselves as well.

Keys for the files in a data contract are stored in so called ["sharings"](/docs/developers/concepts/permissioning.html). With the "sharings" keys for reading and writing data can be provided to other accounts. Usually a contract owner creates one or more keys for a DataContract and [shared](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/sharing.html#addsharing) (or via [extend](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/sharing.html#extendsharing)) those to other participants. When creating a data contract with different keys per section, take care that your **first** [add](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/sharing.html#addsharing) (or via [extend](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/sharing.html#extendsharing)) those keys to the sharing and **then** save data to it. Otherwise the fallback key `*` may be used for encryption and the other participants will try decrypt the data with the specific key, which would lead to errors during decryption.

If an account has access to a key for a property, this account is able to decrypt data written to that property, but is not necessarily able to write data to, because it may still be missing the proper permissions to write data to it. See next section for info about permissions in data contracts.

[![DataContract](/docs/4000_developers/4100_concepts/img/data_contract.png){:max-width="50%"}](/docs/4000_developers/4100_concepts/img/data_contract.png)


## The "Contract" part of "DataContract"
An account, that creates a data contract holds the role "owner" (role id 0) and the member role (role id 1). This account is able to update contract [sharings](/docs/developers/concepts/permissioning.html), update the [dbcp description](/docs/how_it_workds/dbcp.html) and to [invite](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/base-contract.html#invitetocontract) new accounts to the contract.

To "add" entries to a data contract, a group is [granted](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/rights-and-roles.html#setoperationpermission) the permission to write to that property. This means a property (entry, list or mapping) cannot be added to a data contract without granting a group the permission to write to it.

Invited accounts have have the role "member" (role id 1) and can usually [update their own status](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/base-contract.html#changeconsumerstate) in the contract. If the member role has been [granted](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/rights-and-roles.html#setoperationpermission) write permissions to a property or if a member has been [added](https://ipfs.test.evan.network/ipns/QmYmsPTdPPDLig6gKB1wu1De4KJtTqAXFLF1498umYs4M6/contracts/rights-and-roles.html#addaccounttorole) to another group with adequate permissions, this member is able to write to that property.