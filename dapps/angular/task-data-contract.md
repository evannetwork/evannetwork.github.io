---
title: "Angular - Task DApp Data-Contract"
---
# Angular - Task DApp Data-Contract
In this section you will create contracts, read from them and handle several data interactions with the contract by using the evan.network DataContract and the blockchain-core. So each data that is currently cached within the local storage will be moved into an contract.

For how to write the task dapp using your own contract implementation have a look at this: [Angular - Task DApp Custom Contract](/dapps/angular/task-custom).

If you dont want to code by yourself, you can simply read the docs and copy the final resulting src folder from [dapps/task-data-contract/src](https://github.com/evannetwork/dapps-tutorial-angular/tree/master/dapps/task-data-contract) to the [dapps/task/src](https://github.com/evannetwork/dapps-tutorial-angular/tree/master/dapps/task) folder.

# 1. Contract Implementation
Before your start your implementation, its important to decide what functionallities you need. You need to think about data parameters, user roles inclusive security restrictions and so on...

For this example we need a contract that handles some contract metadata and a list of todos. This is the perfect case for the [evan.network data contract](https://evannetwork.github.io/dev/data-contract) / [data contract wiki](https://github.com/evannetwork/blockchain-core/blob/feature/readthedocs-test/docs/data-contract.rst).

When you use a self implemented contract, its important to add the contract implementation abi to our dbcp.json definition file. In this case we can simply use the blockchain-core data-contract wrapper implementation to handle our contract calls. For documentation reasons, you should still put the abi definition of the data contract into the DBCP definition. So other people that read the DBCP definition of the created contract, automaticaly gets your contract definition and functions. So you can program against the contract from anywhere, also outside of your application.

So insert the abi definition into your dbcp.json file from the following [dbcp.json](https://github.com/evannetwork/dapps-tutorial-angular/blob/master/dapps/task-complete/dbcp.json) (its a bit large to insert the full abi here in the documentation).

```json
{
  "public": {
    ...
    "abis": {
      "own": [
        {
          "constant": true,
          "inputs": [
            {
              "name": "key",
              "type": "bytes32"
            }
          ],
          "name": "getListEntryCount",
          ... 
        }
    }
    ...
  }
}
```

## 2. Data Scheme

