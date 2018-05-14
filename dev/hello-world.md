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
      port: 8545,        // parity rpc port
      network_id: "evan.network testcore",
      from: "your accountID from from creating an identity earlier"
      gas: 3000000,
      gasPrice: 20000000000,
    }
  }
};

```
The gas and gas prices are a minimum. Make sure your account/profile has enough funds. This should be
the case after normal onboarding. If not, visit http://gitter.im/evannetwork/faucet .

### Unlocking the Account for Migration
You have created an identity earlier.
To be able to deploy contracts with it, you need to be able to confirm transaction in the parity user interface.

To do this login with your account and go into your profile.

![Profile](/public/dev/profile.png)

There you copy the private key.

Then open http://localhost:8180 (make sure you have started parity with `--force-ui`) and go into the wallet, from there into "Accounts" and from there to "+ Account".

![Profile](/public/dev/parity_private_key_import.png)

Click on this and do the import, you need to enter your password.

That's it for now, but leave the browser tab open.


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

Something to keep in mind is, that every time you start `truffle develop` a fresh and new network is created, so you need to clear the `build/` directory and recompile and redeploy (migrate) the contracts whenever you restart it, or the accounts won't match.

## Deploying the Contract
If you are ready to test your contract in a wider context and share it start the console,

```sh
$ truffle console --network dev
```

or still used the local development network with `truffle develop`

```
truffle(dev)> create migration HelloWorld
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

### Confirming the Deploy Transaction

The migration should start and you get some output but then becomes stuck. This is because parity requires confirmation for the transaction. Go into the parity web-admin browser tab, and there should be a popup asking for confirmation. 

![Profile](/public/dev/confirm_request.png)

Click confirm request to finish deployment.


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

Here we have called the automatically created getter of the public `creator` property.
Let's call the `hello` method we have written ourselves:

```
truffle(dev)> hello.then(async (hi) => { return hi.hello.call("Hallihallo") }).then(async (result) => { console.log(result)} )
Hallihallo
```

It just prints the string we have passed into it. That's because the private `prompt` property hasn't been set yet. So let's do that.

```
truffle(dev)> hello.then(async (hi) => { return hi.setPrompt("Grüetzi, ") }).then(async (result) => { console.log(result)} )
{ tx: '0xa447347f1f64396b7da270f7bc683d928f9bccb6f0f9c6e5e459c8eb6edb9572',
  receipt: 
   { transactionHash: '0xa447347f1f64396b7da270f7bc683d928f9bccb6f0f9c6e5e459c8eb6edb9572',
     transactionIndex: 0,
     blockHash: '0x098a843136533af93b258b066c77c2aa883a884f848043b029ce0dd702d94993',
     blockNumber: 5,
     gasUsed: 43508,
     cumulativeGasUsed: 43508,
     contractAddress: null,
     logs: [],
     status: '0x01',
     logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000' },
  logs: [] }
undefined

```

This was a changeing action, no `call` necessary.
First you get the transaction hash under `tx` as the immediate confirmation that the message was received and is in processing.

Once processing is finished you get the transaction `receipt` and the data is entered into the blockchain. Since we work with a private developer blockchain, and the transaction is really simple, the processing is really fast here.


```
truffle(dev)> hello.then(async (hi) => { return hi.hello.call("Hallihallo") }).then(async (result) => { console.log(result)} )
Grüetzi, Hallihallo
undefined

```

Now the `prompt` has been set, and the `hello` call has something to append, and we get the full message.


## Finalizing

You can access the source code for the project on https://github.com/evannetwork/hello-world-contract.

Before moving on to the [hello-agent](/dev/hello-agent) tutorial, make sure you have deployed the
hello-world smart contract on the `dev` network (i.e. evan.network testcore).
If unsure run the command

```sh
$ truffle deploy  --reset --compile-all --network dev
```

And make sure to confirm the transactions in the parity web-admin.
