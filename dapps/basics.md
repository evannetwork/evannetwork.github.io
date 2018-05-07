---
title: "ÐApp basics"
---
# ÐApp basics
Each Contractus application consists of different parts and components with the purpose of creating
contracts and interacting with them. 

Frontend DApps are implemented using Typescript, Angular 5 and Ionic 3. The general DApp is developed as a web application. The idea that differentiates these decentralized applications from standard web applications is, that they do not get their files directly from a web server, but from the IPFS. Via IPFS, the various files are distributed among all nodes and made available decentrally. With the help of web3, the application can be connected to the evan.network blockchain and interact with contracts. This mechanism for interaction with contracts is generalized and simplified by different frameworks, like the DBCP and the blockchain-core, of contractus. This makes it possible to write efficient, reusable decentralized applications. For efficient development of a resource-saving application, the various library projects are available via IPFS and can therefore be easily integrated into the project. Each ÐApp-library and project is defined using the DBCP protocol and is bundled including its necessary files and its DBCP configuration.

## DBCP in deep
For more information, about how projects and libraries define their definition, visit the [dbcp documentation](/dev/dbcp).

## Frontend in deep
For more information, about how the contractus DApp framework organizes the loading of applications and their dependencies from the IPFS and how to develop full blown angular applications using the contractus stack, visit the documentation about [contractus frontend applications](/angular/basic).

## Blockchain-core and its bundle for UI in deep
For more information, about how the contractus DApp framework interacts with contracts, visit the ["backend" documentation](https://github.com/evannetwork/blockchain-core).
