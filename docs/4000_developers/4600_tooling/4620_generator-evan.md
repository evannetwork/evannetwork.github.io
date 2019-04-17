---
title: "Project Generator"
parent: Developers
grand_parent: Tooling
nav_order: 4620
permalink: /docs/developers/tooling/generator-evan.html
---

# Project Generator

The [evan.network project generator](https://github.com/evannetwork/generator-evan) is a [yeoman generator](http://yeoman.io/) for the whole evan.network project
stack. This generator will create a basic project with a lots of scripts to handle smart-contracts,
smart-agents, DApps and more.

## The generator

For instructions, how to use the generator, please have a look at the readme file of the [evan.network project generator](https://github.com/evannetwork/generator-evan).

## Before you start

It is tempting to use the project generator and start the project quickly. But, each application
requires a definition and a scope of functionality. Before starting the application in detail
including smart-contracts and UI, it is important to define what we want to do. It makes sense to
work using the bottom-up principle. In order to work as safely and cost-efficiently as possible, it
is important to pay attention to all programming paradigms, security gaps and optimizations of the
blockchain development. Everything that is written is irrevocably anchored in the blockchain and
must be correspondingly correct and secure.

<b>Test your Smart Contracts and their interaction before they are externally used for
programming.</b>

Work through the following checklist to be sure that you won't miss anything.

### 1. Think about data structures and contracts

The heart of the evan.network are the contracts on the blockchain. For this reason, you should think
about the following points before starting a project:

- Read about [Smart Contracts](/docs/developers/smart-contracts.html)
- What types of contracts are required?
- Which data and fields are required?
- What types of users are involved and what permissions are required?

### 2. Setup smart-contract structure
- use the [evan.network project generator](https://github.com/evannetwork/generator-evan) for project setup
- implement your smart-contracts
- [implement your smart-contract security](/docs/developers/concepts/smart_contract_security.html)
- test contract structure directly

### 3. Setup your connection to the world
- read about [DBCP](/docs/how_it_works/services/dbcp.html)
- name and identify your ÐApp: name, description, logos, translations, ...
- insert your contracts ABI and data schemes to your project (have a look at [Contract Implementation & Data Scheme](/docs/developers/ui/angular/task-data-contract.html))

### 4. Concept Frontend Application
- read about angular ÐApps ([frontend documentation](/docs/developers/ui/basics.html))
- Which frameworks are needed?
- Draw wireframes for your application.
- Divide the frontend into components that are as reusable and separate as possible.

### 5. Implement your project
- read tutorials about [DApps](/docs/developers/ui/writing-dapps.html)
- add your Dapps by using the [evan.network DApp generator](https://github.com/evannetwork/generator-evan/tree/develop#generate-dapp)
- implement your contract interactions and DApps structure

### 6. Deployment
- [deploy your application](/docs/developers/tooling/deployment.html)
