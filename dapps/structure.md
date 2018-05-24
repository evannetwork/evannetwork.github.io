---
title: "DApp structure"
---
# DApp structure
Each DApp looks like this on the top level.

[![dapps-tutorial - directory](/public/dapps/hello-world/dapps-tutorial-dir-structure.png){:width="150px"}](/public/dapps/hello-world/dapps-tutorial-dir-structure.png)

In order to be able to work in ordered and staked projects, it is necessary to split the project into several projects (e.g. dashboard-dapp, list-dapp, contract1-dapp, contract2-dapp) after a short time. To anticipate this problem and different building jobs, each project uses a [lerna](https://github.com/lerna/lerna) project structure to handle multiple repositories as easily as possible. The lerna project only includes the basic requirements and build jobs for the sub projects. In case of large projects that using Angular or similar, build jobs are definied within seperated projects like the [evan.network angular-gulp project](https://github.com/evannetwork/angular-gulp).

# Featured DApps VS. standalone DApps
By using the evan.network framework to create featured DApps, the initialization of DBCP or the blockchain core is completely replaced and existing, initialized and configured instances can be loaded. This has the advantage that accounts, encryptions and similar complex configurations are executed dynamically by the user when the application is started.

To do this, however, all DApps must be started via the Root evan.network application, since this provides the complete function stack and the various UIs. **As long as the provided functions are used, the application can only be started in environments that have the corresponding structures.** Alternatively, the blockchain-core can be initialized, configured and used, as in the [standalone example](/dapps/standalone/standalone).

