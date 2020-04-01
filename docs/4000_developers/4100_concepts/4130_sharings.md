---
title: "Sharings"
parent: Developers
grand_parent: Concepts
nav_order: 4130
permalink: /docs/developers/concepts/sharings.html
---

# Sharings

## Sharing Criteria
As the main part of data related to contracts is stored in the distributed file system, only references to the DFS are stored in the contract. Contents in the DFS are encrypted with one or more keys specific to the contract instance they belong to.

Contract participants, which should be enabled to read and/or write contract content, need to have access to the keys responsible for the contract data (called 'data keys' in this context). This is done by maintaining a 'sharings' info, which is basically a key store keeping data keys, grouped by the following criteria:
- **participant** - the contract participant, the key is intended for
- **section** - the section in the contract, which holds encrypted data
- **block** - this annotates the _starting_ point, from which on the key is valid

The Sharings of a contract is basically a structured list of encrypted keys.

In a simple contract, the creator of the contract creates a single data key for this contract and wants to share it with other contract members to enable them to read the data in the contract. Therefore, the creator puts the data key into the Sharings info. To prevent third parties from accessing this data key, it is encrypted with the communication key between the contract owner and the contract participant.

![sharings - schema](/docs/4000_developers/4100_concepts/img/sharings_schema.png)


## Key Identification
### Data Keys
The creator of a contract creates a data key on contract creation and adds this to the Sharings as 'shared with herself/himself'. This key is not stored on the owners side and the owner performs exactly the same steps to retrieve the data key as all contract participants.

### Participants
There is no catch-all keyword for sharing encrypted contents with everyone, or a similar mechanic. Sharing happens explicitly and directed from the owner to a participant.

When sharing keys with contract participants, the data key is encrypted with the communication key ('comKey') between the party sharing the key and the party the key is shared with. This means that before sharing encrypted contract contents with another party, usually a [key exchange](/docs/developers/concepts/key_exchange) needs to be undertaken beforehand.

To expose encrypted content to a broader scope without performing a key exchange beforehand, keys can be shared via a scope. This scope has to be known by all participating parties and the key that belongs to the scope has to be accessible by all participating parties. An example for a scope can be a common business context - like a Business Center, where all participating parties cooperate in.

### Sections
Typical examples for Sections are lists and properties in [Data Contracts](/docs/developers/concepts/data-contract.html). Each participant gets an entry in the Sharings with the section names that are shared with him or her.
Other contracts like Service Contracts hold data in applicable properties, to which can be referred in the same manner.

If all contents of a contract are encrypted with the same key, this key can be shared for the section '*', which means 'all' section. Key retrievals get the section names as an argument and for keys in this manner:

1. Check if a section with the same name as requested has been added to the participant's key section - if one exists, use keys from it
2. If no matching section was found, check if this participant has keys for the all section '*' - if so, use keys from it

This fallback behavior is applied when reading **and** writing data. So take care, that if you want to use a specific key for the data and share it to contract participants, you have to share this key with yourself **before** writing data to it. If you do it the other way around, data encryption would just fallback to the "*" key and then add a key for that section, that wasn't used to encrypt the data. When another identity then tries to read this section, it would find a specific key, but be unable to decrypt data with it.


### Blocks
#### Key Lifetimes
Blocks in Sharings signal the starting point, from where on this key is valid. So to be able to read data added at a specific block, a participant requires a key shared before or at the same block.
Data added **after** this block can be read by the participant the data has been shared with. Data added **before** this block cannot be read by this participant through this key.

![multikeys](/docs/4000_developers/4100_concepts/img/multikeys.png)

Keys are valid until they are replaced by a new one, which is then valid until replaced or indefinitely removed.

![multikeys - lifetime](/docs/4000_developers/4100_concepts/img/multikeys_lifetime.png)

This principle is for example used for retrieving keys to decrypt data from lists, where keys might have been updated over time. Taking the example from the last picture, an entry added at block 37 has to be encrypted with the block 20 key. Elements added in or after block 40 use the block 40 key for en- and decryption.

This ensures that:
- keys can be updated
- old entries stay visible for participants that have been granted access to the old key
- newer entries can only be read by participants that have the current key


#### Zero and Infinity
**Granting** a key starting from block 0 makes this key ultimately valid, as any data has been added after block 0. This is used for adding a generic key during contract creation. Replacing this key with a key starting at a later block, will of course replace it starting from that block. 

**Requesting** a key from block 'infinity' by omitting the block argument returns the latest valid key. This can be used when encrypting new data. The timestamp when retrieving this key has to be added to the `cryptoInfo` to ensure that the data can be decrypted later-on, as the key may have been replaced at a later point of time.


#### Sharing Keys
*New keys* are usual generated by a cryptor, usually a [Cryptor AES](https://api-blockchain-core.readthedocs.io/en/latest/encryption/cryptor-aes.html) and instance, which is retrieved from a [cryptor provider](https://api-blockchain-core.readthedocs.io/en/latest/encryption/crypto-provider.html) and then shared other identities with [addSharing](https://api-blockchain-core.readthedocs.io/en/latest/contracts/sharing.html#addsharing) (or via [extendSharing](https://api-blockchain-core.readthedocs.io/en/latest/contracts/sharing.html#extendsharing)).

Sharing *existing keys* to identities requires to fetch the existing key before, e.g. with [`getKey`](https://api-blockchain-core.readthedocs.io/en/latest/contracts/sharing.html#getkey) and then sharing it to the desired identities with [addSharing](https://api-blockchain-core.readthedocs.io/en/latest/contracts/sharing.html#addsharing) (or via [extendSharing](https://api-blockchain-core.readthedocs.io/en/latest/contracts/sharing.html#extendsharing)).

When sharing keys with another user, the same block number should be used as the original key. So if user A has a key that is valid starting from block 30 and shares it with user B, the sharing should be made as 'starting from block 30'. This means that user B can read entries added at or after block 30.
If user B gets the key shared as 'starting from 50' for example, this user would not be able to read contents added before this block (even if the key might match the content).
