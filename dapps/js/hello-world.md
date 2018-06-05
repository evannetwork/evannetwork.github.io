---
title: "evan.network framework Hello World"
---
# evan.network framework Hello World
The goal of this tutorial is to interact with different functionalities of the evan.network blockchain with the help of DBCP or the evan.network blockchain-core. Only simple javascript is used, to create an evan.network dapp-browser embedded application.

After creating the DApp functionallities, you can use a "greater contract" sample to create a contract instance. Thats DBCP description will use your DApp as display possiblity.

[![js tutorial preview](/public/dapps/js/hello-world-preview.png){:width="50%"}](/public/dapps/js/hello-world-preview.png)

## 1. Get Tutorial Application
- [Download Tutorial Application](https://github.com/evannetwork/dapps-tutorial-js)

## 2. Tutorial applications
Within the dapps folder you will find the "Hello World" application. Compared to the standalone example, you will quickly realize that the initialization of a runtime environment is omitted and the existing bcc instance can be used. This instance is enriched with all necessary configurations and information about the logged on user. This makes it possible to load and write data in the user's context.

## 2.1 Build Jobs
Due to the development for the evan.network framework, it becomes necessary to use an existing development runtime, which brings with it all different prerequisites. This is installed via lerna. To be able to open this application in the framework, the index.js file is made AMD-enabled via a rollup.js construction job and copied into the development runtime. This means that the applications can also be tested locally on your own computer.

The build job is defined here: [daps-tutorial-js/scripts/dapps-serve.js](https://github.com/evannetwork/dapps-tutorial-js/blob/master/scripts/dapps-serve.js).

To start your application open two command lines and run the following two commands:

To start the local file server and development runtime:
```js
npm run serve
```

To build and watch the dapps and copy them into the development runtime:
```js
npm run dapps-serve
```

When you started both scripts, your DApp files were copied into your local runtime and you can open the following url: "http://localhost:3000/dev.html#/dashboard.evan/helloworldjs.evan". Their you will find the current representation of your DApp. You can also add your DApp to your [favorites](/tutorial/dashboard).

## 2.2 index.js
The index.js file is the main entrypoint of the application, that is configured by the dbcp.json in the "dapps/hello-world" folder. This file needs and startDApp function, so the evan.network wrapper application can run the entrypoint function for DApp.

The loadData function shows, how to access the current blockchain-core instance to access blockchain data.

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
In this case, we need the startDApp function as entrypoint. As a result of this we could not work with a index.html file. However, this has the disadvantage that no HTML files can be loaded directly (due to [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)). HTML files must be compiled into strings via building jobs or anchored directly as strings in the application. In this simple example, an extra construction job was not needed and the template was anchored directly in the index.js file.

Initially, the data is loaded and then written to the container using a simple innerHTML call.

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

## 3 Deploy it to the real world
### 3.1 Deploy DApp within an contract
Each application can be deployed together with a contract. This allows the contract to contain the information as it should be displayed. A little sample, how to create and sample contract with your hello world app can be found within the dapps-tutorial-angular/scripts/create-contract.js file. Run the following command to start the script for your specific application.

```sh
./scripts/go-ipfs
```

```sh
npm run deploy-to-contract hello-world
```

After the contract id of the created contract was logged to your console, you can open this contract like the ens path before. Just replace your DApp ens path, with the id of your contract (#/dashboard/helloworld.evan => #/dashboard/0x65dCf129E612d4e40bEA8866029e0595BC1Ba5EC). Within the network tab you will see, that the sources for your contract are now loaded from the contract address. 

[![dapps-tutorial - directory](/public/dapps/hello-world/dapp-from-contract.png){:width="200px"}](/public/dapps/hello-world/dapp-from-contract.png)

### 3.2 Deploy DApp to ENS
Have a look [dapp-browser deployment](https://github.com/evannetwork/dapp-browser#ens-deployment).

### 3.3 DApp browser
After you deployed your application using as a ENS entry or within a contract, you will be able to load your DApp's DBCP description via the DBCP / blockchain-core. You can also your DApp using the evan.network dapp-browser. Open [dashboard.evan.network](https://dashboard.evan.network/index.html) and add your DApp to your [favorites](/tutorial/dashboard).