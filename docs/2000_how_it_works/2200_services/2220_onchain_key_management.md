---
Title: "Onchain key management"
parent: How it works
grand_parent: Services
nav_order: 2360
permalink: /docs/how_it_works/services/onchainkeymanagement.html
---

# Onchain key management

At evan.network, we have built an integrated data security and privacy layer. Every identity at evan has an on-chain key store to encrypt and decrypt transactions on identity and smart contract level. So transactions that are processed in the chain at the nodes are fully encrypted and can only be decrypted from invited participants. The whole key management and key exchange is on-chain, so a manual key exchange is not needed anymore to communicate with business partners.

When the user registers on evan.network he gets his own profile smart contract where all his exchanged keys are stored. So when the user gets an invitation to a smart contract, the invitiation arrives in his mailbox where he can accept it. When he accepts the invitation, the secret key of the smart contract is decrypted and automatically stored in his profile.