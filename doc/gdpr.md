---
Title: "GDPR Compliance"
---
# Evan.network GDPR compliance

Evan.network successfully provides an answer to the controversial question of how a blockchain solution can remain in compliance with GDPR regulations.

Per blockchains nature, nothing is ever forgotten as transactions are stored indefinitely. 

Personal data is encrypted with a key only known to the author of this piece of information. The encrypted data is then stored in a [distributed file system](/dev/ipfs) and the author can decide to delete it at any time. Only a reference to the data in the encrypted file system is stored in the blockchain and neither transactions nor the smart contracts themselves contain personal data. This could be done via a custom solution, but such and approach is not part of the provided API and of course it is not advised to do so for obvious reasons.

All accounts have a profile in which they store keys they use for communicating and sharing keys for encrypted data with other accounts. This profile itself is encrypted with a key the user holds off-chain and only known to the user. Keys for data in smart contracts are stored at the smart contract and encrypted per party the keys are shared with.

This leads to some advantages security wise:
- only references to encrypted data is stored in the blockchain and not the encrypted data itself
- additionally, theses references are encrypted as well to prevent hoarding of encrypted data if hoping for later mass decryption
- encrypted data is shared only **intentionally** with other parties, keys to the encrypted data can be stored encrypted and made accessible to selected parties
- data stored in the distributed file system has a limited time to life and will be deleted when this has expired

Only sources account id, targets account id and types of can be deduced via transactions:
- if source or target belong to a known business partner, an action can be linked to this partner (though business partner are not forded to use only one account for all actions)
- if the smart contract called has a well known interface (e.g. `DataContracts`), the type of transaction can be deduced (e.g. in `DatacContracts`, the setting of a property could be deduced, but not which property if not having any more info about the use case of the contract and the transaction)

[Authority Nodes](/doc/authoritynode) on the network are verified and known organizations.

Your data is therefore never processed by anonymous parties but handled by trusted network actors. 
By means of our privacy mechanisms, we can render data stored on the distributed file system as well as smart contracts inaccessible, satisfying the ‘right to erasure’ directive.

Additionally, our API enables you to build GDPR compliant decentralized applications. 
