---
title: "Planning the ÐApp structure"
---
# Planning the ÐApp structure
Each application requires a definition and a scope of functionality. Before starting the application in detail including the UI, its important to defined what we want to do. It makes sense to work using the bottom up principle. In order to work as safely and cost-efficiently as possible, it is important to pay attention to all programming paradigms, security gaps and optimizations of the blockchain development. Everything that is written is irrevocably anchored in the blockchain and must be correspondingly correct and secure.

<b>Test your smart contracts and their interaction before they are externally used for programming.</b>

Work through the following checklist, to be sure, that you wont miss anything.

## 1. Think about data structures and contracts
- Read about [smart-contracts](/dev/smart-contracts)
- What types of contracts are required?
- Which data and fields are required?
- What types of users are involved and what permissions are required?

## 2. Setup Contract Structure
- ...
- test contract structure directly

## 3. Setup DBCP.json
- read about [DBCP](/dev/dbcp)
- name and identify your ÐApp: name, description, logos, translations, ...
- insert contract abi definitions to load
- insert data schemes for your contracts

## 4. Concept Frontend Application
- Which frameworks are needed?
- Draw wireframes for your application.
- Divide the frontend into components that are as reusable and separate as possible.

## 5. Setup Frontend Application
- read about angular ÐApps ([frontend documentation](/frontend/basic))
- Use seed project to setup your basic project ([Seed Project](git@github.com:evannetwork/contractus-dapps-tutorial.git))
- Develop your frontend application.

## 6. Deployment
- deploy your application
