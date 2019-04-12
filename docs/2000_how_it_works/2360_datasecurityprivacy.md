---
Title: "Data Security and Privacy"
parent: How it works
nav_order: 36
permalink: /docs/how_it_works/datasecurityprivacy.html
---

# evan.network Data Security and Privacy

## Security and Privacy Challenges on Blockchain

The benefit of DLT is that every participant can proof transactions, which represents an issue for privacy and security. This is because in a public chain, everybody can read the transaction and the processed data. Most enterprises tend to use no public ledgers for that reasons and plan to use private ledgers. However, the problem is not solved with private chains alone, because the business partners of the chains can read and understand all transactions. So it is rather a feeling of security, because the partners are in most cases external companies.


## Handling of Private Data in evan.network

At evan.network, we have built an integrated data security and privacy layer. Every identity at evan has an on-chain key store to encrypt and decrypt transactions on identity and smart contract level. So transactions that are processed in the chain at the nodes are fully encrypted and can only be decrypted from invited participants. The whole key management and key exchange is on-chain, so a manual key exchange is not needed anymore to communicate with business partners.

[![profile keys and encryption](/docs/2000_how_it_works/img/profile_keys.png){:class="center"}](/docs/2000_how_it_works/img/profile_keys.png)

Personal data is encrypted with a key only known to the author of this piece of information. The encrypted data is then stored in a [distributed file system](/docs/developers/concepts/ipfs.html) and the author can decide to delete it at any time. Only a reference to the data in the encrypted file system is stored in the blockchain and neither transactions nor the smart contracts themselves contain personal data. This could be done via a custom solution, but such and approach is not part of the provided API and of course it is not advised to do so for obvious reasons.

All accounts have a profile in which they store keys they use for communicating and sharing keys for encrypted data with other accounts. This profile itself is encrypted with a key the user holds off-chain and only known to the user. Keys for data in smart contracts are stored at the smart contract and encrypted per party the keys are shared with.

When storing personal data on the blockchain the data would be persisted forever in the smart contract and a deletion would be not possible. On evan.network this data is not stored directly on the blockchain. The personal files are encrypted on the client itself and then uploaded a distributed file system. The filesystem returns a unique hash to directly access the uploaded data. Now only this hash as a reference to the data is stored in the smart contract. This implicates that the owner of the data has the full control about his assets and is also able to delete his data store assets.

Now all references to the encrypted data are public visible to everyone who's validating and inspecting the blockchain. This would enable data hoarding by third parties with the intention of a mass decryption of these data elements if the currently used encryption algorithm is broken. To prevent this, all referenced hashes are encrypted as well before they are stored into a smart contract or any other element in the blockchain.

The security mechanism with the encryption of the files and sharing of the keys to these files ensures the all data is shared only **intentionally** with other parties.


## How keys are exchanged

When two parties want to start communicating, they first need to exchange a communication key. This key is later on used to encrypt messages between these two and for sharing further keys (see last illustration).

Communication keys are exchanged via Diffie-Hellman key exchange, which is usually described as following:
- both parties commit on a common (publicly known)
- both parties own a private key, each only known to one of them
- both parties create a public key by combining the own private key and the common part
- public keys are exchanged between them and used to create a final key from each end

This approach is adapted and used on evan.network in this way:
- common part is publicly known and known to the API
- both parties create private and public key at account creation
- public key is stored a the profile of each account and can be accessed by everyone, so no extra communication is required to get another parties public key
- Diffie-Hellman key can be creating by combining own private key and public key from other parties profile (called "exchange key")
- exchange key is used to encrypt and share the "communication key" with the other party, this is done via the mailbox
- as public key can be retrieved from profile and the encrypted communication key can be send to mailbox, this process can be initiated by one side, if a confirmation is not required, the process is completed at the initiators end
- the other party can finalize at its end at any time, optionally a confirmation can be send to the initiator

The following illustration shows the entire key exchange process:

[![key exchange flow](/docs/2000_how_it_works/img/key_exchange.png){:class="center"}](/docs/2000_how_it_works/img/key_exchange.png)


## What can be deduced from the transactions

If anyone inspects the blockchain transactions, they can deduce the following attributes/elements:
- The source accountid which has sent the transaction
- The target accountid/smart contract where the transaction has been sent to
- if source or target belong to a known business partner, an action can be linked to this partner (though business partner are not forded to use only one account for all actions)
- if the smart contract called has a well known interface (e.g. `DataContracts`), the type of transaction can be deduced (e.g. in `DataContracts`, the setting of a property could be deduced, but not which property if not having any more info about the use case of the contract and the transaction)

Your data is therefore never processed by anonymous parties but handled by trusted network actors.
By means of our privacy mechanisms, we can render data stored on the distributed file system as well as smart contracts inaccessible, satisfying the ‘right to erasure’ directive.


## GDPR compliance

The combination of the blockchain with the distributed file system enables users to develop GDPR compliant DApps on the evan.network. The user itself has the full control of the data which is stored on the distributed file system. He can delete all uploaded data which is uploaded from his account.

In summary, the evan.network has widely developed security concepts and is thus the first blockchain that enables the development of GDPR-compliant applications.


## Smart Contract Security

Smart Contracts at evan.network are by default different pieces of logic which can be executed by all accounts. Enterprise applications and smart contracts must have the ability to ensure read/write/update and delete security for the stored data in a smart contract and also the different actions a smart contract can execute. By default, all our smart contracts have a rights and roles mechanism implemented.

This rights and roles contract which is attached to every contract template which is deployed on evan.network can be configured fine granular for the needs of the owner of the contract. The owner can add up to 256 different roles and an unlimited number of accounts to every contract which is enhanced by the rights and roles contract.

Every role in this contract can be configured with different rights for Add/Modify/Delete of data in the source contract. For example when deploying a custom data contract on evan.network you can configure the rights for every data set which the contract should be held. By default, no data sets are enabled to be modified or added to the contract. The owner of the contract must enable the data fields manually which the contract should hold. Also, the owner can configure which roles are permitted to modify or delete data fields on the contract.

The rights and roles contract can also restrict the access to different contract state changing functions of the source smart contract. For example, a data contract can have different states like draft or active. The owner of the contract can now configure which roles can execute the method to change the status of the current smart contract.

By design the Ethereum blockchain allows reading values stored in a contract. For restricting read access to the values to different accounts, we've implemented an encryption mechanism for data which is described above.