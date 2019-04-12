---
title: "Developer Cheat Sheet"
parent: Developers
grand_parent: Tooling
nav_order: 4650
permalink: /docs/developers/tooling/cheatsheet.html
---

# evan.network Developer Cheat Sheet

## node.js Commands and Tricks

### Q: Which node.js version you have to use?

It is highly recommended to use a nodejs version 9.x.
Unfortunately, due to a 3rd party dependency, version 10.x is not usable, yet.

Most linux distributions allow you to install older versions via their normal package system.

If not, take your installation package from here:

https://nodejs.org/download/release/v9.11.2/

### Q: What dependencies are there?
Depends on whether you are in the browser or the nodejs backend. In either case, you usually need:

- api-blockchain-core
- dbcp
- smart-contracts-core

Luckily, if you are using their respective public `npm` packages, as is recommended this is all taken care of for you.

### Q: How do I install `npm` ?

If you just need to use normal npm public packages, you can install it in whatever is the default for your system.

If work on linux and you expect you have to use the development branch of some packages, which is not unlikely if you need new features,
you should re-configure your npm global package directory like this https://docs.npmjs.com/getting-started/fixing-npm-permissions , because you will have to link dependencies manually.

### Q: How do I link development branches of core libraries?
If you do need to use development branches of core libraries, you need to create a separate local directory for it outside your project, and check out the needed library from github, and then install it, build it and link it,

Let's do it with api-blockchain-core as an example.

```sh
$ cd devlibs
$ git clone @evan.network/api-blockchain-core
$ cd api-blockchain-core
$ npm i
...

# this step can be slightly different for different core libraries, but is described in their READMEs
$ npm run build
...

$ npm link
$ cd my-project-dir
$ npm link @evan.network/api-blockchain-core
```

### How do I set up a Project?
It is strongly recommended to use the https://github.com/evannetwork/generator-evan
generator to set up your projects. Follow the readme there to install it.


### Q: How do I start a smart-agent?
If you have used the `generator-evan` setup tool, as is recommended, all you need to do is run the following commands
in your project directory.

```sh
# only needs to be run once whenever you add a new agent
$ gulp link-agents

$ npm start
```

This assumes you either have a parity running locally, or you have changed your `node_modules/@evan-network/edge-server-seed/config/eth.js` file to point to any non-local reachable ethereum access point.

If you didn't, you just can pass it the evan.netwirk default access point via environment variable.

```sh
$ ETH_WS_ADDRESS='wss://testcore.evan.network/ws' npm start
```

Be careful to only ever have one edge-server process running, or there will be port conflicts.


### Q: How can I debug?

In the browser, debugging is just done with the normal browser development tools, usually Chrome or Firefox.
Since the used default-framework is angular-5, you debug with generated .js code though, which can be tedious.

The generator also provides a debug script, in your project, just run

```sh
$ npm run debug
```

The same `ETH_WS_ADDRESS` may have to be passed as in normal starts.

Once your agent is running in debug mode, you can attach to it with any nodejs debug listener. Almost always
this is the Chrome browser debugger. You open development tools with F12, and then you can see the green nodejs debug icon in the toolbar.

Setting breakpoints can be done in the debugger UI, or it can be done in the source code with a "debugger" statement.


### Q: How do I test my Frontend locally?

Assuming you are using the `evan:dapp` generator module, all you need to do is go to you project directory and

```sh
$ npm run serve
```

And then you can access it under `http://localhost:3000/dev.html#`.


## Working with Contracts

### Q: How do I compile contracts derived from core contracts in my project?
If the project has been initialized with the generator and has the `evan:contracts` module, you have a `compile-contracts` gulp task. It will compile all the .sol files in your `contracts/` projetc directory and provide access to the core contracts to be imported and referenced during compilation.

### Q: How do I get more development funds?
On our EVE faucet channel here: https://gitter.im/evannetwork/faucet.

Just enter your destination contract account ID in the chat. You can get 5EVEs every day.
There is a bot protection active that gives you increasingly larger timeouts if you try too often.

### Q: How do you tinker with the blockchain using my accounts?

The easiest way is to install the https://github.com/evannetwork/evan.prompt package and then run it in your project directory.



