---
title: "evan.network framework Hello World"
parent: Developers
grand_parent: UI
nav_order: 4330
permalink: /docs/developers/ui/js-hello-world.html
---

# evan.network framework Hello World
The goal of this tutorial is to interact with different functionalities of the evan.network blockchain with the help of DBCP or the evan.network blockchain-core (bcc). Only simple Javascript is used to create an evan.network ƉApp-browser embedded application.

After creating the ÐApp functionalities, you can use a 'greeter contract' sample to create a contract instance. The DBCP description attached to the 'greeter contract' will use your ƉApp as display possiblity.

[![js tutorial preview](/public/docs/developers/ui/js-hello-world.html-preview.png){:width="50%"}](/public/docs/developers/ui/js-hello-world.html-preview.png)

## 1. Get Tutorial Application
- [Download Tutorial Application](https://github.com/evannetwork/sample-dapps-js)

## 2. Tutorial applications
Within the ƉApps folder, you will find the 'Hello World' application. Compared to the standalone example, you will realize quickly that the initialization of a runtime environment is omitted and the existing bcc instance can be used. This instance is enriched with all necessary configurations and information about the logged-in user. This makes it possible to load and write data in the user's context.

## 2.1 Build Jobs
Due to the development for the evan.network framework, it becomes necessary to use an existing development runtime, which brings with it all different prerequisites. It is installed via Lerna. To be able to open this application in the framework, the `index.js` file is made AMD-enabled via a `rollup.js` construction job and copied into the development runtime. This means that the applications can also be tested locally on your own computer.

The build job is defined here: [daps-tutorial-js/scripts/dapps-serve.js](https://github.com/evannetwork/sample-dapps-js/blob/master/scripts/dapps-serve.js).

To start your application, open two command lines and run the following two commands:

To start the local file server and development runtime:
```js
npm run serve
```

To build and watch the ƉApps and copy them into the development runtime:
```js
npm run dapps-serve
```

When you started both scripts, your ƉApp files were copied into your local runtime and you can open the following URL: "http://localhost:3000/dev.html#/dashboard.evan/helloworldjs.evan". There, you will find the current representation of your ƉApp. You can also add your ƉApp to your [favorites](/docs/first_steps/dashboard.html).

## 2.2 index.js
The `index.js` file is the main point of entry for the application, which is configured by the `dbcp.json` in the `dapps/hello-world` folder. This file needs a `startDApp`-function, so the evan.network wrapper application can run the `point of entry`-function for the ƉApp.

The `loadData`-function shows how to access the current bcc instance to access blockchain data.

```js
async function loadData() {
  const runtime = CoreBundle.CoreRuntime;
  const data = { };

  // get contract id from current url or from parent
  let contractId = window.location.href.split('/').pop();

  if (!contractId || contractId.indexOf('0x') !== 0) {
    contractId = '';
  } else {
    // load opened contract
    const contract = await runtime.description.loadContract(contractId);

    // load sample contract data
    data['contract-id'] = contractId;
    data['owner'] = await contract.methods.owner().call();
    data['contract-methods'] = Object.keys(contract.methods).join(', ');
    data['sample1'] = await contract.methods.greet().call();
    data['sample2'] = await runtime.executor.executeContractCall(contract, 'greet');
  }

  // load contract description
  const description = await runtime.description.getDescription(
    contractId || 'dashboard.evan',
    '0x001De828935e8c7e4cb56Fe610495cAe63fb2612'
  );

  data['description'] = JSON.stringify(
    description,
    null,
    2
  );;

  return data;
}

```

## 2.3 index.html / templates
In this case, we need the `startDApp`-function as point of entry. As a result of this, we cannot work with an `index.html` file. This has the disadvantage that no HTML files can be loaded directly (due to [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)). HTML files must be compiled into strings via building jobs or anchored directly as strings in the application. In this simple example, an extra construction job was not needed and the template was anchored directly in the `index.js` file.

Initially, the data is loaded and then written to the container using a simple `innerHTML` call.

```js

export async function startDApp(container, dbcpName) {
  // hide dapp-browser loading
  loading.finishDAppLoading();

  const helloWorldEl = createElement(container);
  const data = await loadData();

  helloWorldEl.innerHTML = `
    <h2>Hello World JS</h2>
    <table>
      <thead>
        <tr>
          <th>Field</th>
          <th>Value</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Contract ID</td>
          <td>${ data['contract-id'] || '---' }</td>
        </tr>
        <tr>
          <td>Owner</td>
          <td>${ data['owner'] || '---' }</td>
        </tr>
        <tr>
          <td>Sample 1</td>
          <td>${ data['sample1'] || '---' }</td>
        </tr>
        <tr>
          <td>Sample 2</td>
          <td>${ data['sample2'] || '---' }</td>
        </tr>
        <tr>
          <td>Contract Methods</td>
          <td>
            <textarea rows="10">${ data['contract-methods'] || '---' }</textarea>
          </td>
        </tr>
        <tr>
          <td>Description</td>
          <td>
            <textarea rows="30">${ data['description'] || '---' }</textarea>
          </td>
        </tr>
      </tbody>
    </table>
  `;
}
```

## 3 Deploy it to the Real World
### 3.1 Deploy ƉApp within a Contract
Each application can be deployed together with a contract. This allows the contract to contain the information as it should be displayed. A little sample how to create and sample contract with your 'Hello World' ƉApp can be found within the `dapps-tutorial-angular/scripts/create-contract.js` file. Run the following commands:

1. Start IPFS client
```sh
./scripts/go-ipfs
```

2. Publish your files to the IPFS
```sh
ipfs add -r dapps/hello-world/src
```
[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/deploy-to-ipfs.png){:width="50%"}](/docs/4000_developers/4300_ui/img/deploy-to-ipfs.png)

3. Insert the deployed folder hash (e.g. "QmfZLwBPUT1n3DoJqpqnLCTcUKABLgUsgfE4KetkXdq8XK") to the correct origin to `dbcp.json` file.
[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/add-to-dbcp.png){:width="50%"}](/docs/4000_developers/4300_ui/img/add-to-dbcp.png)

4. Deploy it to the contract
```sh
npm run deploy-to-contract hello-world
```

You will get a console output similar to the following. Behind the log parameter `created contract`, you will find the newly created contract ID.

[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/deploy-to-contract.png){:width="50%"}](/docs/4000_developers/4300_ui/img/deploy-to-contract.png)

### 3.2 Deploy ƉApp to ENS
Have a look [ƉApp deployment](/docs/developers/tooling/deployment.html).

### 3.3 View it in the Real World
After you deployed the application within a contract or by using a ENS address, the ƉApp is available from everywhere, **globally**. To test this, you can use the evan.network dashboard. Open the following URL [https://dashboard.test.evan.network/index.html](https://dashboard.test.evan.network/index.html) and navigate to the `favorites ƉApp`. Before you can access your favorites, it is nessecary to create an evan.network identity. If you haven't created an identity before, have a look [here](/docs/first_steps.html).

Add the favorite using the following steps:
1. Open Dashboard:
[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/favorites-1.png){:width="50%"}](/docs/4000_developers/4300_ui/img/favorites-1.png)

2. Add the favorite:
[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/favorites-2.png){:width="50%"}](/docs/4000_developers/4300_ui/img/favorites-2.png)

3. Open the ƉApp:
[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/favorites-3.png){:width="50%"}](/docs/4000_developers/4300_ui/img/favorites-3.png)

4. Result:
[![js tutorial preview](/docs/4000_developers/4300_ui/img/hello-world-preview.png){:width="50%"}](/docs/4000_developers/4300_ui/img/hello-world-preview.png)

By having a look into the browser network tab, you will see that you data is loaded from the IPFS server:

[![dapps-tutorial - directory](/docs/4000_developers/4300_ui/img/dapp-from-contract.png){:width="400px"}](/docs/4000_developers/4300_ui/img/dapp-from-contract.png)
