---
Title: "Contract & Content encryptions"
parent: How it works
grand_parent: Services
nav_order: 2210
permalink: /docs/how_it_works/services.html
---

# Contract & Content encryption

The benefit of DLT is that every participant can proof transactions, which represents an issue for privacy and security. This is because in a public chain, everybody can read the transaction and the processed data. Most enterprises tend to use no public ledgers for that reasons and plan to use private ledgers. However, the problem is not solved with private chains alone, because the business partners of the chains can read and understand all transactions. So it is rather a feeling of security, because the partners are in most cases external companies.


## Handling of Private Data in evan.network

At evan.network, we have built an integrated data security and privacy layer. Every identity at evan has an on-chain key store to encrypt and decrypt transactions on identity and smart contract level. So transactions that are processed in the chain at the nodes are fully encrypted and can only be decrypted from invited participants. The whole key management and key exchange is on-chain, so a manual key exchange is not needed anymore to communicate with business partners.

Personal data is encrypted with a key only known to the author of this piece of information. The encrypted data is then stored in a [distributed file system](/docs/how_it_works/services/ipfsfilehandling.html) and the author can decide to delete it at any time. Only a reference to the data in the encrypted file system is stored in the blockchain and neither transactions nor the smart contracts themselves contain personal data. This could be done via a custom solution, but such and approach is not part of the provided API and of course it is not advised to do so for obvious reasons.

All accounts have a profile in which they store keys they use for communicating and sharing keys for encrypted data with other accounts. This profile itself is encrypted with a key the user holds off-chain and only known to the user. Keys for data in smart contracts are stored at the smart contract and encrypted per party the keys are shared with.

When storing personal data on the blockchain the data would be persisted forever in the smart contract and a deletion would be not possible. On evan.network this data is not stored directly on the blockchain. The personal files are encrypted on the client itself and then uploaded a distributed file system. The filesystem returns a unique hash to directly access the uploaded data. Now only this hash as a reference to the data is stored in the smart contract. This implicates that the owner of the data has the full control about his assets and is also able to delete his data store assets.

Now all references to the encrypted data are public visible to everyone who's validating and inspecting the blockchain. This would enable data hoarding by third parties with the intention of a mass decryption of these data elements if the currently used encryption algorithm is broken. To prevent this, all referenced hashes are encrypted as well before they are stored into a smart contract or any other element in the blockchain.

The security mechanism with the encryption of the files and sharing of the keys to these files ensures the all data is shared only **intentionally** with other parties.

## Smart Contract Security

Smart Contracts at evan.network are by default different pieces of logic which can be executed by all accounts. Enterprise applications and smart contracts must have the ability to ensure read/write/update and delete security for the stored data in a smart contract and also the different actions a smart contract can execute. By default, all our smart contracts have a rights and roles mechanism implemented.

This rights and roles contract which is attached to every contract template which is deployed on evan.network can be configured fine granular for the needs of the owner of the contract. The owner can add up to 256 different roles and an unlimited number of accounts to every contract which is enhanced by the rights and roles contract.

Every role in this contract can be configured with different rights for Add/Modify/Delete of data in the source contract. For example when deploying a custom data contract on evan.network you can configure the rights for every data set which the contract should be held. By default, no data sets are enabled to be modified or added to the contract. The owner of the contract must enable the data fields manually which the contract should hold. Also, the owner can configure which roles are permitted to modify or delete data fields on the contract.

The rights and roles contract can also restrict the access to different contract state changing functions of the source smart contract. For example, a data contract can have different states like draft or active. The owner of the contract can now configure which roles can execute the method to change the status of the current smart contract.

By design the Ethereum blockchain allows reading values stored in a contract. For restricting read access to the values to different accounts, we've implemented an encryption mechanism for data which is described above.

## GDPR compliance

The combination of the blockchain with the distributed file system enables users to develop GDPR compliant DApps on the evan.network. The user itself has the full control of the data which is stored on the distributed file system. He can delete all uploaded data which is uploaded from his account.

In summary, the evan.network has widely developed security concepts and is thus the first blockchain that enables the development of GDPR-compliant applications.