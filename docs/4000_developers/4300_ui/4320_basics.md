---
title: "ÐApp Basics"
parent: Developers
grand_parent: UI
nav_order: 4320
permalink: /docs/developers/ui/basics.html
---

# ÐApp Definition
A ÐApp, short for 'Decentralized Application', is not much different to a regular web application at first. 
What sets a ÐApp apart from regular web-based applications however, is that this new kind of application is not hosted on a traditional server. 
In lieu of the standard Client-Server structure, ÐApps serve clients from the blockchain. With applications running on the blockchain new benefits are introduced: 

* All interaction with the ÐApp is securely encrypted from the application's side at all times

* Critical components are distributed, significantly improving fault tolerance and rendering DDoS(Distributed Denial of Service) attacks practically impossible

* Building on ÐApps significantly improves security - cross-site scripting, SQL injections and XML attacks are made obsolete

* The increase of data volume that comes with millions of new IoT devices, amongst others, is an aspect that can be handled significantly more efficient and cost effective with blockchain based distributed storage. Data is stored encrypted by default. 

ÐApps on evan.network can be reached with a standard web browser through a [user friendly address](/docs/how_it_works/services/ensnameservice.html) such as 'nodeone.evan'. Decentralized Applications succeed in providing a much more trustworthy experience than traditional applications would have been able to.

# ÐApp Basics
Each evan.network application consists of different parts and components with the purpose of creating
contracts and interacting with them.

Frontend ÐApps are mostly implemented using Typescript, Angular 5 & Ionic 3 or Vue.js. The general ÐApp is developed as a web application. The idea that differentiates these decentralized applications from standard web applications is that they do not get their files directly from a web server, but from the IPFS. 

Via IPFS, the various files are distributed among all nodes and made decentrally available. With the help of Web3, the application can be connected to the evan.network blockchain to interact with contracts. This mechanism for interaction with contracts is generalized and simplified by different frameworks, like the DBCP and the blockchain-core.

This makes it possible to write efficient, reusable and decentralized applications. For efficient development of a resource-saving application, the various library projects are available via IPFS and can therefore be easily integrated into the project. Each ÐApp library and project is defined using the DBCP protocol and is bundled including its necessary files and its DBCP configuration.

# Featured ÐApps VS. Standalone ÐApps
By using the evan.network framework to create featured ÐApps, the initialization of DBCP or the blockchain-core is completely replaced and existing, already initialized and configured instances can be loaded. This has the advantage that accounts, encryptions and similar complex configurations are executed dynamically by the user when the application is started.

To do this, however, all ÐApps must be started via the evan.network ÐApp-browser application, since this provides the complete function stack and the various UIs. **As long as the provided functions are used, the application can only be started in environments that have the corresponding structures.** Alternatively, the blockchain-core can be initialized, configured and used as in the [standalone example](/docs/developers/ui/standalone.html).

# Featured ÐApp loading
The evan.network ÐApp-browser is the entry point for featured ÐApps. It will handle dynamic URL routing, so ÐApp ENS addresses or contract addresses using an underlying DBCP description. If the URL changes, the ÐApp-browser will check for the new ÐApp that should be loaded. Internal, the ÐApp-browser simply uses [SystemJS](https://github.com/systemjs/systemjs) for a dynamic source loading. When a url is opened, it detects the several parts of the UI. It uses the ens or contract address that is opened using the has within the url, to load the DApps DBCP description from the evan.network ENS service. Within this DBCP description, all dependencies, required files and IPFS origins are saved. For example have a look at the ui-angular-core and it's structure:

```json
{
  "public": {
    "author": "evan GmbH",
    "dapp": {
      "dependencies": {
        "angular-libs": "^2.1.0",
        "bcc": "^2.7.1",
        "smart-contracts": "^2.3.1"
      },
      "entrypoint": "angularcore.js",
      "files": [
        "angularcore.css",
        "angularcore.js"
      ],
      "origin": "QmcqTrS5fEw6SdJpMEr7N5XWTdNhKztFsu3NojoLcNBYVH",
      "type": "library"
    },
    "dbcpVersion": 2,
    "description": "Contractus core angular modules & components.",
    "license": {
      "file": "https://ipfs.test.evan.network/ipns/QmT1FwnYyURjLj7nKMwEuTPUBc5uJ6z1zAVsYnKfUL1X1q/AGPL-3.0-only.txt",
      "type": "AGPL-3.0-only"
    },
    "name": "angularcore",
    "tags": [
      "contractus",
      "library"
    ],
    "version": "2.1.1",
    "versions": {
      "2.1.0": "QmPNFiPvR3k1AjbrQduD4xGmQHd7keuKXgUeyktsEQ3Mho"
    }
  }
}
```

The ENS name of this application is `angularcore`. Within other DBCP files, the `angularcore` can  be simply marked as dependency and it will loaded by the SystemJS ENS loader. But the project itself is defined as `@evan.network/ui-angular-core` within it's package.json. If we would try to load the `angularcore` via DBCP-ENS and want to require the `@evan.network/ui-angular-core`, we would receive an error, that the `@evan.network/ui-angular-core` is not defined. SystemJS maps the loaded address for the loaded ÐApp, so we would have to load `angularcore` directly. But in a world of using typescript, the ÐApp compiler would also throw errors, that `angularcore` is not defined... We can solve this in 2 ways. Defining an alias map within the `tsconfig.json` file of the requiring ÐApp or by using SystemJS custom map structure within the original library DApp (we would recommend the second way).

- tsconfig map
```json
{
  "compilerOptions": {
    "paths": {
      "angular-core": [
        "../../../node_modules/@evan.network/ui-angular-core/dist/angularcore.js"
      ],

    }
  }
}
```

- System map
```ts
import { System } from '@evan.network/ui-dapp-browser';

System.map['@evan.network/ui-angular-core'] = 'angularcore.evan!dapp-content';
```

Here an example how nested ÐApp loading works:

[![sample loading structure](/docs/4000_developers/4300_ui/img/dapp-browser.png){:width="50%"}](/docs/4000_developers/4300_ui/img/dapp-browser.png)
