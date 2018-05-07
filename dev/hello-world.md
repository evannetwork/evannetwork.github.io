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
  address public creator;
  uint public balance;

  function sayHi() returns (bool success) {
    balance = 1000;
    return true;
  }
}
```


## Deploying the Contract

## Testing the Contract

To make it easy in your first steps, [a simple Contract Viewer]() has been written for you that allows you to send messages to any contract and view the responses.





