---
title: "Hello World"
---

# Hello World

Write your first blockchain contract and access it.

## Prerequisites

We work on a unix command line.

You have installed parity, solidity and nodejs as described [here](/doc/first-steps).

You have installed truffle, as described [here](http://truffleframework.com/docs/getting_started/installation)<sup>[+]</sup>.

## Setting up the Project

```sh
$ mkdir hello-world
$ cd hello-world
$ truffle init
$ truffle compile
```

This has created your inial truffle project.

## Configuring the Network
You have already started `parity` locally, as linked in the prerequisites, but for the application to know
to know to connect to the local ethereum node, you need to configure it to do so.

```sh
$ edit truffle.js
```

```javascript
module.exports = {
  // See <http://truffleframework.com/docs/advanced/configuration>
  // to customize your Truffle configuration!
  networks: {
    dev: {
      host: "127.0.0.1",
      port: 30303,        // parity default port
      network_id: "evan.network testcore",
      from: "your accountID from from creating an identity earlier"
    }
  }
};

```

## Test Connection
The easiest way is to just attempt a migration, even if nothing new is to deploy.

```sh
$ truffle migrate --network dev
Using Network 'dev'.

Network up to date.

```

## Writing the Contract

It's just a simple echo application.

```sh
$ edit contracts/hello_world.sol
```

```solidity
pragma solidity ^0.4.20;

contract HelloWorld {
  // all data and code is visible to everyone, that's the point of the blockchain
  // the accessability indicators only affect writing changes and access syntax
  address public creator;
  string prompt;

  constructor() public {
    creator = tx.origin;
  }
  
  function setPrompt(string value) external {
    // the most basic form of access control
    // it just silently ignores any invalid access
    // proper exceptions would be better
    if (msg.sender == address(creator)) prompt = value;
  }

  // anything that is done in the blockchain costs gas (i.e. currency)
  // this function concatenates strings, which can be rather expensive
  // so whenever possible such utility functionality should be done outside the chain
  // the view modifier indicates that state is read, but not changed
  function hello(string salut) external view returns (string greeting) {
    bytes memory tmp0 = bytes(prompt);
    bytes memory tmp1 = bytes(salut);
    greeting =  new string(tmp0.length + tmp1.length);
    bytes memory buffer = bytes(greeting);
    uint k = 0;
    for(uint i = 0; i < tmp0.length;) buffer[k++] = tmp0[i++];
    for(i = 0; i < tmp1.length;) buffer[k++] = tmp1[i++];
    return greeting;
  }
}
```
Anything that is done in the blockchain costs gas (i.e. currency). The `hello()` function concatenates strings, which can be rather expensive, so whenever possible such utility functionality should be done outside the chain.

## Compiling the Contract



```sh
$ truffle compile contracts/hello.sol
```
or just 

```sh
$ truffle compile
```

to compile all changed contracts.

This creates the file build/contracts/HelloWorld.json, which contains administrative data structures used by the truffle framework, but most importantly also contains a byte array containing the byte code that can be executed in the blockchain, once it is deployed there.


## A Local Development Network
Above we have configured the "dev" network. While this is a development network, and uses a local ethereum client, it is still a shared network and blockchain, so everything you do there is visible to everyone and will be in there forever. This isn't too much of a problem normally, but still should be avoided when it is easily possible.

With this simple hello-world contract that doesn't depend on any existing contract infrastructure in the blockchain this is possible.

So just start

```sh
$ truffle develop
```

And it will start an isolated development blockchain with the  [ truffle development console](http://truffleframework.com/docs/advanced/commands)<sup>[+]</sup> for you.
You can compile, deploy, test and debug your contracts there, and only when you are satisfied with that,
you deploy it on the shared blockchain.

Something to keep in mind is, that every time you start `truffle develop` a fresh and new network is created, so you need to clear the `build/` directory an recompile and re-deploy (migrate) the contracts whenever you restart it, or the accounts won't match.


## Deploying the Contract
If you are ready to test your contract in a wider context and share it start the console,

```sh
$ truffle console --network dev
```

or still used the local development network with `truffle develop`

```
truffle(dev)> create migration
```

```sh
$ edit migrations *_hello_world.js
```

```javascript
var hello = artifacts.require("HelloWorld");

module.exports = function(deployer) {
  deployer.deploy(hello);
};

```

```
truffle(dev)> migrate
```

When you are still in the development process and use the local developing network, the simplest way to always deploy all changes in your local files is to always run this command

```
truffle(develop)> deploy --reset --compile-all
```

`deploy` is just an alias for `migrate`.

## Using the Contract

You will be either using your identity account you have created earlier, or one of the accounts listed from the truffle developer console.
```
truffle(dev)> var hello = HelloWorld.deployed()
undefined
truffle(dev)> hello.then(async (hi) => { return hi.creator.call() }).then(async (result) => { console.log(result)} )
0xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
undefined
```

Yes, it's usually all asynchronous code, which means either callbacks or promises. In this short example it is ok to use callbacks, but once it gets more complicated, it's usually better to use promises for clarity.






