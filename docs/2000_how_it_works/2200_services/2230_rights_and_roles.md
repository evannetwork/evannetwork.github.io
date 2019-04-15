---
Title: "Rights and roles on contracts"
parent: How it works
grand_parent: Services
nav_order: 2230
permalink: /docs/how_it_works/services/rightsandrolesoncontracts.html
---

# Rights and roles on contracts

Smart Contracts at evan.network are by default different pieces of logic which can be executed by all accounts. Enterprise applications and smart contracts must have the ability to ensure read/write/update and delete security for the stored data in a smart contract and also the different actions a smart contract can execute. By default, all our smart contracts have a rights and roles mechanism implemented.

This rights and roles contract which is attached to every contract template which is deployed on evan.network can be configured fine granular for the needs of the owner of the contract. The owner can add up to 256 different roles and an unlimited number of accounts to every contract which is enhanced by the rights and roles contract.

Every role in this contract can be configured with different rights for Add/Modify/Delete of data in the source contract. For example when deploying a custom data contract on evan.network you can configure the rights for every data set which the contract should be held. By default, no data sets are enabled to be modified or added to the contract. The owner of the contract must enable the data fields manually which the contract should hold. Also, the owner can configure which roles are permitted to modify or delete data fields on the contract.

The rights and roles contract can also restrict the access to different contract state changing functions of the source smart contract. For example, a data contract can have different states like draft or active. The owner of the contract can now configure which roles can execute the method to change the status of the current smart contract.