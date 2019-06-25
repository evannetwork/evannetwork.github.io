---
title: "Standalone - Hello World"
parent: Developers
grand_parent: UI
nav_order: 4340
permalink: /docs/developers/ui/standalone.html
---

# Standalone - Hello World
The goal of this tutorial is to interact with different functionalities of the evan.network blockchain, by the help of DBCP or the evan.network blockchain-core. A simple HTML file is being produced, which is able to use all functionalities without any runtime environment. With the help of this small example, you can develop applications on the evan.network blockchain that run completely independently.

After creating the ÐApp functionalities, you can use a 'greeter contract' sample to create a contract instance. The DBCP description attached to the 'greeter contract' will use your ƉApp as display possiblity.

[![standalone tutorial preview](/docs/4000_developers/4300_ui/img/standalone_preview.png){:width="50%"}](/docs/4000_developers/4300_ui/img/standalone_preview.png)

## 1. Get Tutorial Application
- [Download Tutorial Application](https://github.com/evannetwork/sample-dapps-standalone)

## 2. Tutorial applications
Within the ƉApps folder, you will find frontend 'Hello World' applications for DBCP and blockchain-core (in short bcc). These projects have the minimal setup for interacting with the evan.network framework. The DBCP / bcc libraries are bundled using Browserify and published to the IPFS. So the application can attain the dependencies directly from IPFS.

In this simple scenario, both examples look almost the same. This is because the bcc is an extension of the DBCP, including various encryption mechanisms and structures, such as the mailbox or the address book, which are not used for a 'Hello World' example.

In the bcc example, the runtime is less encapsulated and can therefore be better adapted, but needs a few more configuration parameters.

### 2.1 local development
For testing, you need to open the "dapps/hello-world-bcc/src/index.html" file within you local browser.

If you want to test the application using a small web server, you can run the following command within your root Lerna project:
```sh
npm run serve
```
The web server will be started at port 3000 and each `dapps/\*\*/src` folder is mapped for file serving. So you can open the following URLs to view the application:
  - http://localhost:3000/hello-world-bcc/index.html

### 2.2 index.html
The `index.html` is the point of entry for the application that requires the necessary files to start the bcc. You can simply insert the origin of the library using a script tag. In addtion, the Web3 and IPFS library needs to be loaded.

### 2.3 index.js BCC
In comparison, the `createDefaultRuntime` of the DBCP is replaced with the following code. By using this code, you will be enabled to adjust the whole configuration and use the modular components as you like to. This means that the frontend is able to put the individual components together as required. The result looks almost like the runtime of the DBCP, but with much more features.

```js
const runtimeConfig = {
  accountMap: {
    '0x001De828935e8c7e4cb56Fe610495cAe63fb2612':
      '01734663843202e2245e5796cb120510506343c67915eb4f9348ac0d8c2cf22a',
  },
  ipfs: { host: 'ipfs.test.evan.network', port: '443', protocol: 'https' },
  web3Provider: 'wss://testcore.evan.network/ws',
};

/**
 * Create DBCP runtime.
 */
async function createRuntime() {
  // initialize dependencies
  const provider = new Web3.providers.WebsocketProvider(
    runtimeConfig.web3Provider,
    {clientConfig: {keepalive: true, keepaliveInterval: 5000}},
  );
  const web3 = new Web3(provider,
    null,
    {transactionConfirmationBlocks: 1}
  );
  const dfs = new bcc.Ipfs({remoteNode: new IpfsApi(runtimeConfig.ipfs)});

  const formattedContracts = {};
  Object.keys(smartcontracts).forEach((key) => {
      const contractKey = (key.indexOf(':') !== -1) ? key.split(':')[1] : key;
      formattedContracts[contractKey] = smartcontracts[key];
  });

  // create runtime
  const runtime = await bcc.createDefaultRuntime(web3, dfs, runtimeConfig, {
    contracts: formattedContracts,
  });

  return runtime;
}
```

## 3 Deploy it to the Real World
### 3.1 Deploy ƉApp within an Contract
Each application can be deployed together with a contract. This allows the contract to contain the information as it should be displayed. Run the following command:

```sh
npm run deploy-to-contract hello-world-dbcp
```

You will get a console output similar to the following. Behind the log parameter `created contract`, you will find the newly created contract ID.

[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/deploy-to-contract.png){:width="50%"}](/docs/4000_developers/4300_ui/img/deploy-to-contract.png)

### 3.2 View it in the Real World
After you deployed the application within a contract or by using an ENS address, the ƉApp is available from everywhere, **globally**. To test this, you can use the evan.network dashboard. Open the following URL [https://dashboard.test.evan.network/index.html](https://dashboard.test.evan.network/index.html) and navigate to the `favorites ƉApp` tab. Before you can access your favorites, it is necessary to create an evan.network identity. If you haven't created an identity before, have a look [here](/docs/first_steps.html).

Add the favorite using the following steps:

1. Open Dashboard:
[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/favorites-1.png){:width="50%"}](/docs/4000_developers/4300_ui/img/favorites-1.png)

2. Add the favorite:
[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/favorites-2.png){:width="50%"}](/docs/4000_developers/4300_ui/img/favorites-2.png)

3. Open the DApp:
[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/favorites-3.png){:width="50%"}](/docs/4000_developers/4300_ui/img/favorites-3.png)

4. Result:
<iframe width="100%" height="500px" src="https://ipfs.test.evan.network/ipfs/QmcVDvv3Q9wxc2SGsBoL56Eg31xi2tx3ovVPzktyAVZEi5/index.html?contractid=0xdD968788fC88E2373F938a61494D90958CAd2FDf">
</iframe>

By having a look into the browser network tab you will see that your data is loaded from the IPFS server:

[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/dapp-from-contract.png){:width="400px"}](/docs/4000_developers/4300_ui/img/dapp-from-contract.png)
