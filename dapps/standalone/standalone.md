---
title: "standalone Hello World"
---
# standalone Hello World

## 1. Get Tutorial Application
- [Download Tutorial Application](https://github.com/evannetwork/dapps-tutorial-standalone)

## 2. ÐApp Wrapper application
The downloaded folder "dapps-tutorial-standalone" looks like this on the top level.

[![dapps-tutorial - directory](/public/dapps/hello-world/dapps-tutorial-dir-structure.png){:width="150px"}](/public/dapps/hello-world/dapps-tutorial-dir-structure.png)

In order to be able to work in ordered and staked projects, it is necessary to split the project into several projects (e.g. dashboard-dapp, list-dapp, contract1-dapp, contract2-dapp) after a short time. To anticipate this problem and different building jobs, each project uses a [lerna](https://github.com/lerna/lerna) project structure to handle multiple repositories as easily as possible.

## 3. Tutorial applications
Within the dapps folder you wil find frontend hello world applications for "dbcp" and "blockchain-core" (in short bcc). This projects have the minimal setup for interacting with the evan.network framework. The DBCP / BCC libraries are bundled using browserify and published to the IPFS. So the application can require the dependencies directly from IPFS.

In this simple scenario, both examples look almost exactly the same. This is because the blockchain core is an extension of the DBCP, including various encryption mechanisms and structures, such as the mailbox or the address book, that are not used for a Hello World example. The only difference is the code for the runtime creation. In the bcc example, the runtime is less encapsulated and can therefore be better adapted.

### 3.1 index.html
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

### 3.2 index.js
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

## 4. Deploy DApp within an contract
Each application can be deployed together with a contract. This allows the contract to contain the information as it should be displayed. A little sample, how to create and sample contract with your hello world app can be found within the dapps-tutorial-standalone/scripts/create-contract.js file. Run the following command to start the script for your specific application.

```sh
npm run ipfs deamon
```

```sh
npm run deploy-to-contract hello-world-dbcp
```

After the contract id of the created contract was logged to your console, you can open this contract using DBCP / BCC. Open your index.html file and apply the contract id as an url parameter: "/index.html?contractid=0x000...".

The contract can also be loaded by the evan.network dashboard application loader by using the following url: "https://dashboard.evan.network/#/0x000..."

[![dapps-tutorial - directory](/public/dapps/hello-world/dapp-from-contract.png){:width="200px"}]
