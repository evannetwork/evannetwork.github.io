---
title: "Angular - Task DApp Data-Contract"
---
# Angular - Task DApp Data-Contract
**Before performing this example, please go through the [Task DApp setup](/dapps/angular/task) tutorial, as this tutorial is based on this example.**

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

# 2. Data Schema
The data schema is also a property of the dbcp.json, that describes the data structure of our contract in deep. In our case, the data schema will describe the data that is saved within our data contract's todo list.

```json
{
  ...
  "dataSchema": {
    "todo_list": {
      "$id": "todo_list_schema",
      "type": "array",
      "additionalProperties": false,
      "items": {
        "type": "object",
        "properties": {
          "completed": {
            "type": "boolean"
          },
          "_title": {
            "type": "string"
          }
        }
      }
    }
  }
  ...
}
```

# 3. Create and Read the Data Contract
The DApp will be designed to handle both side, the contract creation and the data consuming. The evan.network dashboard includes a dynamic parameter routing to open unregistered ens and contract addresses. So the DApp can check the current opened url, if a contract id or the normal ens address is opened. When the ens address is opened, we will redirect to an contract creation page. When a contract id is opened, the user gets redirected to the TodoMVC component.

## 3.1 Contract creation component
At first, we need to add a contract creation component. Navigate to the "task/src/components" folder and create the "create-task" folder, with the following structure:
- create-task
  - create-task.ts
  - create-task.html
  - create-task.scss

create-task.ts
```ts
```

create-task.html
```ts
```

create-task.scss
```ts
```