---
title: "project generator"
---
# project generator

The [evan.network project generator](https://github.com/evannetwork/generator-evan) is a [yeoman generator](http://yeoman.io/) for the whole evan.network project
stack. This generator will create a basic project with a lots of scripts to handle smart-contracts,
smart-agents, DApps and more.

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

### 1. Think about Data Structures and Contracts
- Read about [Smart Contracts](/dev/smart-contracts)
- What types of contracts are required?
- Which data and fields are required?
- What types of users are involved and what permissions are required?

### 2. Setup Contract Structure
- ...
- test contract structure directly

### 3. Setup DBCP.json
- read about [DBCP](/dev/dbcp)
- name and identify your ÐApp: name, description, logos, translations, ...
- insert contract ABI definitions to load
- insert data schemes for your contracts

### 4. Concept Frontend Application
- Which frameworks are needed?
- Draw wireframes for your application.
- Divide the frontend into components that are as reusable and separate as possible.

### 5. Setup Frontend Application
- read about angular ÐApps ([frontend documentation](/dapps/basics))

### 6. Deployment
- deploy your application

## The generator
