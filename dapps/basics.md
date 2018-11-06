---
title: "ÐApp Basics"
---
# ÐApp Definition
A DApp, short for 'Decentralized Application', is not much different to a regular web application at first. What sets a DApp apart from regular web-based applications, however stems from the fact that they are not under control by any third party.
All interaction with the DApp is securely encrypted from the application's side at all times.

DApps on evan.network can be reached with a standard web browser through a [user friendly address](https://evannetwork.github.io/doc/namespaces) such as 'nodeone.evan'. Decentralized Applications succeed in providing a much more trustworthy experience than traditional applications would have been able to.

Instead of relying on 'classical servers' for hosting, DApps are running on masternodes in the evan.network. Due to their decentralized nature the threat of a single point of failure scenario is eliminated entirely.

Additional benefits that come with decentralization are immunity to hacks and DDoS (Distributed Denial of Service) attacks, allowing for consistent uptime of your DApps without the usual security considerations you would be facing in a traditional environment. 


# ÐApp Basics
Each evan.network application consists of different parts and components with the purpose of creating
contracts and interacting with them.

Frontend ÐApps are mostly implemented using Typescript, Angular 5 and Ionic 3. The general ÐApp is developed as a web application. The idea that differentiates these decentralized applications from standard web applications is that they do not get their files directly from a web server, but from the IPFS. 

Via IPFS, the various files are distributed among all nodes and made decentrally available. With the help of Web3, the application can be connected to the evan.network blockchain to interact with contracts. This mechanism for interaction with contracts is generalized and simplified by different frameworks, like the DBCP and the blockchain-core.

This makes it possible to write efficient, reusable and decentralized applications. For efficient development of a resource-saving application, the various library projects are available via IPFS and can therefore be easily integrated into the project. Each ÐApp library and project is defined using the DBCP protocol and is bundled including its necessary files and its DBCP configuration.

# Packaged ÐApps VS. Standalone ÐApps
By using the evan.network framework to create packaged ÐApps, the initialization of DBCP or the blockchain-core is completely replaced and existing, already initialized and configured instances can be loaded. This has the advantage that accounts, encryptions and similar complex configurations are executed dynamically by the user when the application is started.

To do this, however, all ÐApps must be started via the evan.network ÐApp-browser application, since this provides the complete function stack and the various UIs. **As long as the provided functions are used, the application can only be started in environments that have the corresponding structures.** Alternatively, the blockchain-core can be initialized, configured and used as in the [standalone example](/dapps/standalone/standalone).

# Packaged ÐApp loading
The evan.network ÐApp-browser is the entry point for packaged ÐApps. It will handle dynamic URL routing, so ÐApp ENS addresses or contract addresses using an underlying DBCP description. If the URL changes, the ÐApp-browser will check for the new ÐApp that should be loaded.

[![Finished](/public/dapps/dapp-browser.png){:width="50%"}](/public/dapps/dapp-browser.png)

# Prerequisits
Before start developing, be sure to set up the following programs on your system:
  - [`node.js` (8+) + `npm` (5+)](https://nodejs.org/en)
  - [Gulp](https://github.com/gulpjs/gulp)
  - [Lerna](https://github.com/lerna/lerna)
  - [IPFS](https://ipfs.io/docs/install)

# ÐApp structure
Each ÐApp looks like this on the top level.

[![ÐApps-tutorial - directory](/public/dapps/hello-world/dapps-tutorial-dir-structure.png){:width="150px"}](/public/dapps/hello-world/dapps-tutorial-dir-structure.png)

In order to be able to work in ordered and staked projects, it is necessary to split the project into several sub-projects (e.g. `dashboard-ÐApp`, `list-ÐApp`, `contract1-ÐApp`, `contract2-ÐApp`) after a short time. To anticipate this problem and differentiate building jobs, each project uses a [Lerna](https://github.com/lerna/lerna) project structure to handle multiple repositories as easily as possible. The Lerna project only includes the basic requirements and building jobs for the sub-projects. In case of large projects that use Angular or similar tools, building jobs are definied within seperated projects like the [evan.network Angular-Gulp project](https://github.com/evannetwork/angular-gulp).
