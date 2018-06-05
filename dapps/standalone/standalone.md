---
title: "standalone Hello World"
---
# standalone Hello World
The goal of this tutorial is to interact with different functionalities of the evan.network blockchain with the help of DBCP or the evan.network blockchain-core. A simple HTML file is being produced, which is able to use all functionalities without any runtime environment. With the help of this small example, you can develop applications on the even.network blockchain that run completely independently.

After creating the DApp functionallities, you can use a "greater contract" sample to create a contract instance. Thats DBCP description will use your DApp as display possiblity.

[![standalone tutorial preview](/public/dapps/hello-world/standalone_preview.png){:width="50%"}](/public/dapps/hello-world/standalone_preview.png)

## 1. Get Tutorial Application
- [Download Tutorial Application](https://github.com/evannetwork/dapps-tutorial-standalone)

## 2. Tutorial applications
Within the dapps folder you wil find frontend hello world applications for "dbcp" and "blockchain-core" (in short bcc). This projects have the minimal setup for interacting with the evan.network framework. The DBCP / BCC libraries are bundled using browserify and published to the IPFS. So the application can require the dependencies directly from IPFS.

In this simple scenario, both examples look almost the same. This is because the blockchain core is an extension of the DBCP, including various encryption mechanisms and structures, such as the mailbox or the address book, that are not used for a Hello World example.

In the bcc example, the runtime is less encapsulated and can therefore be better adapted, but needs a bit more configuration parameters.

### 2.1 local development
For testing, you can simply open the "dapps/hello-world-bcc/src/index.html" / "dapps/hello-world-dbcp/src/index.html" file within you local browser.

If you want to test the application using a small web server, you can run the following command within your root lerne project:
```sh
npm run serve
```
The web server will be started at port 3000 and each dapps/\*\*/src folder is mapped for file serving. So you can open the following urls to view the application:
  - http://localhost:3000/hello-world-bcc/index.html
  - http://localhost:3000/hello-world-dbcp/index.html

### 2.2 index.html
The index.html is the entrypoint of the application that requires the necessary files to start the DBCP / blockchain-core. You can simply insert the origin of the library using an script tag. In addtion, the Web3 and Ipfs library needs to be loaded to.
This sample shows, how to load the DBCP using IPFS.

```html
<!-- Loading DBCP -->
<script src="http://ipfs.evan.network/ipfs/QmPCNLE794BCwsriAg9gYjCha3EPZHDxefB5GNwugoUgfh"></script>

<!-- Loading Web3 -->
<script src="http://ipfs.evan.network/ipfs/QmXVX173ygohnfg8rxzhynrNFHLTLKUqcBEKAFrEZGA9JN"></script>

<!-- Loading ipfs-api -->
<script src="http://ipfs.evan.network/ipfs/QmczFSf23jB7RhT5ptnkycCf57hTGdfUE1Pa2qbZe4pmEN"></script>
```

### 2.3 index.js DBCP
After all depdencies were loaded, you can start you application right now within the index.js file.
Use the "createRuntime" function to generate a new DBCP runtime. Using this runtime you can access all the functionallities that are exposed by DBCP / BCC.

```js
async function createRuntime() {
  const runtimeConfig = {
    accountMap: {
      '0x001De828935e8c7e4cb56Fe610495cAe63fb2612':
        '01734663843202e2245e5796cb120510506343c67915eb4f9348ac0d8c2cf22a',
    },
    ipfs: { host: 'ipfs.evan.network', port: '443', protocol: 'https' },
    web3Provider: 'wss://testcore.evan.network/ws',
  };

  // initialize dependencies
  const web3 = new Web3();
  web3.setProvider(new web3.providers.WebsocketProvider(runtimeConfig.web3Provider));
  const dfs = new dbcp.Ipfs({ remoteNode: new IpfsApi(runtimeConfig.ipfs), });

  // create runtime
  const runtime = await dbcp.createDefaultRuntime(web3, dfs, { accountMap: runtimeConfig.accountMap, });

  return runtime;
}
```

When we are running our application without any contract id, we are loading an test description from the "dashboard.evan" ens address to show, that it's also working without any contracts. After you deployed the hello-world sample into an contract, you can access several functions of the contract. The getContractId function shows, that the contract id that sould be loaded, can be parsed out of the window location. When you have deployed the application, append the following parameters to the applications url: "?contractid=0xB070f2e1FcbE4d01987E30a9DF9F6e22E69EA105".

```js
/**
 * Get the contract id from an url parameter or from last url hash value for iframe routing.
 * @param {string} url url that should be checked, default is window.location.href
 */
function getContractId(url) {
  // try to load contract id over url parameter
  const match = (url || window.location.href).match('[?&]contractid=([^&]+)');
  let contractId;

  if (match) {
    contractId = match[1];
  } else {
    // try to get contract id from url hash (#/.../0x00)
    contractId = (url || window.location.href).split('/').pop();
  }

  if (contractId.indexOf('0x') === 0) {
    return contractId;
  }
}

/**
 * Start Hello World sample.
 */
async function runHelloWorld() {
  window.runtime = runtime = await createRuntime();

  // get contract id from current url or from parent
  let contractId = getContractId();
  if (!contractId && window.parent) {
    contractId = getContractId(window.parent.location.href);
  }
  
  if (!contractId || contractId.indexOf('0x') !== 0) {
    contractId = '';

    document.getElementById('test-description').innerHTML = 'not set';
  } else {
    // load opened contract
    const contract = await runtime.description.loadContract(contractId);
    
    // load sample contract data
    document.getElementById('contract-id').innerHTML = contractId;
    document.getElementById('owner').innerHTML = await contract.methods.owner().call();
    document.getElementById('contract-methods').innerHTML = Object.keys(contract.methods).join(', ');
    document.getElementById('sample1').innerHTML = await contract.methods.greet().call();
    document.getElementById('sample2').innerHTML = await runtime.executor.executeContractCall(contract, 'greet');
  }
  
  // load contract description
  let description = await runtime.description.getDescription(
    contractId || 'dashboard.evan',
    '0x001De828935e8c7e4cb56Fe610495cAe63fb2612'
  );

  document.getElementById('test-description').value = JSON.stringify(
    description,
    null,
    2
  );
}
```

### 2.4 index.js BCC
In comparison, the createDefaultRuntime of the DBCP is replaced with the following code. By using this code you will be enabled to adjust the whole configuration and use the modular components as you want. This means that the frontend is able to put the individual components together as required. The result looks almost like the runtime of the DBCP, but with many more features. 

```js
// BCC core configuration
const config = {
  // web3Provider: 'ws://13.57.211.13:8546',
  web3Provider: 'ws://localhost:8546',
  nameResolver: {
    ensAddress: '0x937bbC1d3874961CA38726E9cD07317ba81eD2e1',
    ensResolver: '0xDC18774FA2E472D26aB91deCC4CDd20D9E82047e',
    labels: {
      businessCenterRoot: 'testbc.evan',
      ensRoot: 'evan',
      factory: 'factory',
      admin: 'admin',
      eventhub: 'eventhub',
      profile: 'profile',
      mailbox: 'mailbox'
    },
    domains: {
      root: ['ensRoot'],
      factory: ['factory', 'businessCenterRoot'],
      adminFactory: ['admin', 'factory', 'ensRoot'],
      businessCenter: ['businessCenterRoot'],
      eventhub: ['eventhub', 'ensRoot'],
      profile: ['profile', 'ensRoot'],
      profileFactory: ['profile', 'factory', 'ensRoot'],
      mailbox: ['mailbox', 'ensRoot'],
    },
  },
  smartAgents: {
    onboarding: {
      accountId: '0x063fB42cCe4CA5448D69b4418cb89E663E71A139',
    },
  },
  alwaysAutoGasLimit: 1.1,
}

// runtime configuration
const runtimeConfig = {
  accountMap: {
    '0x001De828935e8c7e4cb56Fe610495cAe63fb2612':
      '01734663843202e2245e5796cb120510506343c67915eb4f9348ac0d8c2cf22a',
  },
  ipfs: { host: 'ipfs.evan.network', port: '443', protocol: 'https' },
  web3Provider: 'wss://testcore.evan.network/ws',
};

/**
 * Smart contracts solc representation.
 */
Solc = function (SmartContracts) {
  this.SmartContracts = SmartContracts;
}

Solc.prototype.getContracts = function() {
  const shortenedContracts = {};

  Object.keys(this.SmartContracts).forEach((key) => {
    const contractKey = (key.indexOf(':') !== -1) ? key.split(':')[1] : key
    shortenedContracts[contractKey] = this.SmartContracts[key]
  })

  return shortenedContracts;
}

/**
 * Create DBCP runtime.
 */
async function createRuntime() {
  // initialize dependencies
  const web3 = new Web3();
  web3.setProvider(new web3.providers.WebsocketProvider(runtimeConfig.web3Provider));

  // load SmartContracts from ipfs externally
  const SmartContracts = await SystemJS.import('https://ipfs.evan.network/ipfs/QmdB15Kqy4Gwe1aSSS6grj5ftSaFbUktqVdB1G4wkBYP1G/compiled.js');
  const keyProvider = new bcc.KeyProvider(runtimeConfig.accountMap);
  keyProvider.origin = keyProvider;

  // initialize the bcc core runtime
  await bcc.createAndSet({
    accountId: Object.keys(runtimeConfig.accountMap)[0],
    coreOptions: {
      web3: web3,
      solc: new Solc(SmartContracts),
      dfsRemoteNode: bcc.IpfsRemoteConstructor(runtimeConfig.ipfs),
      config: config,
    },
    keyProvider: keyProvider,
    CoreBundle: bcc,
    SmartContracts
  });

  return bcc.CoreRuntime;
}
```

## 3 Deploy it to the real world
### 3.1 Deploy DApp within an contract
Each application can be deployed together with a contract. This allows the contract to contain the information as it should be displayed. A little sample, how to create and sample contract with your hello world app can be found within the dapps-tutorial-angular/scripts/create-contract.js file. Run the following command to start the script for your specific application.

```sh
./scripts/go-ipfs
```

```sh
npm run deploy-to-contract hello-world-dbcp
```
```sh
npm run deploy-to-contract hello-world-bcc
```

After the contract id of the created contract was logged to your console, you can open this contract like the ens path before. Just replace your DApp ens path, with the id of your contract (#/dashboard/helloworld.evan => #/dashboard/0x65dCf129E612d4e40bEA8866029e0595BC1Ba5EC). Within the network tab you will see, that the sources for your contract are now loaded from the contract address. 

[![dapps-tutorial - directory](/public/dapps/hello-world/dapp-from-contract.png){:width="200px"}](/public/dapps/hello-world/dapp-from-contract.png)

### 3.2 Deploy DApp to ENS
Have a look [dapp-browser deployment](https://github.com/evannetwork/dapp-browser#ens-deployment).

### 3.3 DApp browser
After you deployed your application using as a ENS entry or within a contract, you will be able to load your DApp's DBCP description via the DBCP / blockchain-core. You can also your DApp using the evan.network dapp-browser. Open [dashboard.evan.network](https://dashboard.evan.network/index.html) and add your DApp to your [favorites](/tutorial/dashboard).