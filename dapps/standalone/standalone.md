---
title: "standalone Hello World"
---
# standalone Hello World

## 1. Get Tutorial Application
- [Download Tutorial Application](https://github.com/evannetwork/dapps-tutorial-standalone)

## 2. Tutorial applications
Within the dapps folder you wil find frontend hello world applications for "dbcp" and "blockchain-core" (in short bcc). This projects have the minimal setup for interacting with the evan.network framework. The DBCP / BCC libraries are bundled using browserify and published to the IPFS. So the application can require the dependencies directly from IPFS.

In this simple scenario, both examples look almost the same. This is because the blockchain core is an extension of the DBCP, including various encryption mechanisms and structures, such as the mailbox or the address book, that are not used for a Hello World example.

In the bcc example, the runtime is less encapsulated and can therefore be better adapted, but needs a bit more configuration parameters.

### 2.1 index.html
The index.html requires the necessary files to start the DBCP / blockchain-core. You can simply insert the origin of the library using an script tag. In addtion, the Web3 and Ipfs library needs to be loaded to.
This sample shows, how to load the DBCP using IPFS.

```html
<!-- Loading DBCP -->
<script src="http://ipfs.evan.network/ipfs/QmPCNLE794BCwsriAg9gYjCha3EPZHDxefB5GNwugoUgfh"></script>

<!-- Loading Web3 -->
<script src="http://ipfs.evan.network/ipfs/QmXVX173ygohnfg8rxzhynrNFHLTLKUqcBEKAFrEZGA9JN"></script>

<!-- Loading ipfs-api -->
<script src="http://ipfs.evan.network/ipfs/QmczFSf23jB7RhT5ptnkycCf57hTGdfUE1Pa2qbZe4pmEN"></script>
```

### 2.2 index.js DBCP
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

When we are running our application without any contract id, we are loading an test description from the "dashboard.evan" ens address to show, that it's also working without any contracts. After you deployed the hello-world sample into an contract, you can access several functions of the contract.

```js
window.runtime = runtime = await createRuntime();

let contractId = window.location.href.split('/');
contractId = contractId[contractId.length - 1];

if (contractId.indexOf('0x') !== 0) {
  contractId = '';

  document.getElementById('test-description').text = 'not set';
} else {
  const contract = await runtime.description.loadContract(contractId);
  
  document.getElementById('owner').text = contractId;
  document.getElementById('contract-methods').text = Object.keys(contract.methods).join(', ');
  document.getElementById('sample1').text = await contract.methods.greet().call();
  document.getElementById('sample2').text = await runtime.executor.executeContractCall(contract, 'greet');
}

let description = await runtime.description.getDescription(contractId || 'dashboard.evan');

document.getElementById('test-description').value = JSON.stringify(
  description,
  null,
  2
);
```

### 2.2 index.js BCC
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
  const keyProvider = new bccCore.KeyProvider(runtimeConfig.accountMap);
  keyProvider.origin = keyProvider;

  // initialize the bcc core runtime
  await bccCore.createAndSet({
    accountId: Object.keys(runtimeConfig.accountMap)[0],
    coreOptions: {
      web3: web3,
      solc: new Solc(SmartContracts),
      dfsRemoteNode: bccCore.IpfsRemoteConstructor(runtimeConfig.ipfs),
      config: config,
    },
    keyProvider: keyProvider,
    CoreBundle: bccCore,
    SmartContracts
  });

  return bccCore.BCCCore;
}
```


## 4 Deploy it to the real world
### 4.1 Deploy DApp within an contract
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


### 4.2 Deploy DApp to ENS
Have a look [dapp-browser deployment](https://github.com/evannetwork/dapp-browser#ens-deployment).