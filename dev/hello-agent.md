---
title: "Hello Agent"
---

# Hello Agent

Lets write a smart agent, so we can interact with the blockchain via a normal web service without installing all the blockchain services and libraries on every computer.

If you wanna cheat, just pull it from https://github.com/evannetwork/smart-agent-hello .
You will still have to do some setup though.

## Prerequisites

In the evan.network the established way to write web services is to use the [`edge-server`](https://github.com/evannetwork/edge-server), which is just an [ActionHero](https://www.actionherojs.com/) with some added infrastructure. It also uses the version "^18.0", so asynchronous programming with callbacks is discouraged now.

Installation is rather straightforward.

```sh
$ git clone git@github.com:evannetwork/edge-server.git
$ cd edge-server
$ nvm i
```

This should also automativally install the blockchain-core libraries and all other dependencies in `node_modules/`, which can take a while.

Sadly, since we are still in early development and don't have real releases yet, so it often is necessary to install dependencies by hand. So if you get errors:

```sh
$ cd node_modules
$ git clone  git@github.com:evannetwork/blockchain-core.git
$ git clone  git@github.com:evannetwork/dbcp.git
$ git clone  git@github.com:evannetwork/smart-contracts.git
$ cd smart-contracts; npm i
$ cd ../dbco; npm i
$ cd ../blockchain-core; npm i
$ cd ../..; npm i
```

If there are still errors, wait for a proper release that installs without problems, which will come soon.

If all is done test it and start it with 

```sh
$ npm start
```

You should now be able to see the action-hero admin interface on `https://localhost:8080`.

## Getting the API
Contracts are just bytecode blobs with no real meta-information attached to them. So without
a defined protocol things can get really messy real fast when people don't know what
methods are in a contract, and what parameters they need.

In evan.network the encouraged way to take care of this is [DBCP](/dev/dbcp).
But this is not always available, and a little too complex for a quick tutorial.
So we just deployed our `HelloWorld` contract via truffle, and to use those contracts
in an evan.network application, we need to import the API of the contract separately.

Which means we first have to export it:

```sh
$ cd hello-world/contracts
$ solc --abi hello.sol
```

Depending on what version of the solidity compiler you have, you get either a file or stdout output.

Either way, you will find an array with the interface definition in the output.

Copy it somewhere for safekeeping.


## Setting up the Project

It is possible to create a project directory and develop a SmartAgent, which is an ActionHero-Plugin, directly in the `node_modules/` of the EdgeServer. But better is, to have a separate directory, that can be source controlled separately, and just link it into the edge-server with a symbolic link.

```sh
$ mkdir ../smart-agent-hello
$ ln -s ../smart-agent-hello node_modules/smart-agent-hello
$ cd ../smart-agent-hello
```

Usually you can have actionhero create the plugin directory structure. But this doesn't really work anymore in recent versions. Maybe it will again in the future, but for now we do it manually, which isn't too hard either.

```sh
$ mkdir config initializers  # this is the minimum of subdirectories needed
$ mkdir actions              # we also need this
$ edit package.json
```

This can be very small for simple agents. Since we access the blockchain-core libraries via the edge-server, most of the things we need are already available.

```json
{
    "author": "Me Myself",
    "name": "smart-agent-hello",
    "description": "Changes the string from the hello-world contract",
    "version": "0.0.1",
    "engines": {
        "node": ">=8.0.0"
    },
}
```

```sh
$ edit config/smart-agent-hello.js
```

This can be rather simple too.

```javascript
exports['default'] = {
  smartAgentHello: (api) => {
    return {
      disabled: false,  // a simple way to disable specific smart-agent plugins
      // if you want more control over this without having to edit the config file try this
      // disabled: process.env.SMART_AGENT_HELLO_DISABLED ?  JSON.parse(process.env.SMART_AGENT_DISABLED_DISABLED) : true,
      name: 'HelloAgent',
      account: "the account/identity you have created and created the hello-world contract with",
      contract: 'the contract hash returned in the deploy operation earlier',
      helloAPI: '[{"constant": ..... "constructor"}]'
    }
  }
}
```

You need the account id, because you want to be able to change the contract data, and by default only the owner/creator can do writes on contracts.

Here is also the place where we store the generated API object from earlier, in the `helloAPI` property.

A thing to remember: ActionHero, and thus edge-server, doesn't read the plugin configs from the plugin directories, it needs the config to be in its own config directory. The simplest way to do this is this:

```sh
$ ln config/smart-agent-hello.js ../edge-server/config/smart-agent-hello.js
```

You can copy it of course ,too. The config that is used is the one in the edge-server config directory, though.

You still have to tell edge-server that there is a plugin.

```sh
$ edit ../edge-server/config/plugins.js

```

```javascript
exports['default'] = {
  plugins: (api) => {
    return {
      'smart-contracts': { path: __dirname + '/../node_modules/smart-contracts' },
      'edge-server-admin-module': { path: __dirname + '/../node_modules/edge-server-admin-module' },
      // ...
      'smart-agent-hello': { path: __dirname + '/../node_modules/smart-agent-hello },
    }
  }
}
```

## The Initializer
Every plugin needs an initializer. This is usually where most of the code of your smart-agent resides, especially if there are no actions.

ActionHero is a little sensitive about semicolons to end lines for some reasons, so it is recommended
to no use them in SmartAgents.

```sh
$ edit initializers/hello.js
```

```javascript
'use strict'

const { Initializer, api } = require('actionhero')


module.exports = class SmartAgentHello extends Initializer {
  constructor() {
    super()
    this.name = 'HelloAgent'
    this.loadPriority = 7000
    this.startPriority = 7000
    this.stopPriority = 7000
  }


  // put anything you need outside of this file, in here
  // this happens if you need to share functionality
  // between initializer and action (or commands) for example
  // common external dependencies are resolved 
  // through the api object as well

  
  async initialize() {
    
    if (api.config.smartAgentHello.disabled) return

    api.bcc.contractLoader.contracts['HelloWorld'] = {
      "interface": api.config.smartAgentHello.helloAPI
    };

    const account = api.config.smartAgentHello.account
    const hello = api.bcc.contractLoader.loadContract('HelloWorld', api.config.smartAgentHello.contract)
    
    api.smartAgentHello = {
      setMessage: async function (msg){
        
        // you not only "export" through the api object
        // you also import through it, the configuration for example
        
        // but also the blockchain core library
        // here a writing contract method call
        return await api.bcc.executor.executeContractTransaction(
          hello, 'setPrompt', { from: account }, msg);
      },

      // here a non-writing call, no need for accountIDs here, because everyone can read everything
      hello: async function (salut) {
        var r = api.bcc.signer.web3.utils.toAscii(
          await api.bcc.executor.executeContractCall(hello, 'hello',  salut ))
        console.log(r)
        return r
      }
    }
    
  }
  
  async stop() {}

}

```

## An Action

Writing actions is easy too. See how the action uses the `smartAgentHello` object that was created in
the initializer to import objects it needs.

```sh
$ edit actions/hello.js
```

```javascript
'use strict'
const { Action, api } = require('actionhero')

class SmartAgentHelloHello extends Action {
  constructor() {
    super()
    this.name = 'smart-agents/hello/hello'
    this.description = 'Returns a greeting.'
    this.inputs = {
      salut: {
        required: true,
      },
    }
    this.outputExample = { greeting: "greeting" }
  }

  async run({ params, response }) {
    try {
      response.greeting = await api.smartAgentHello.hello(params.salut)
      response.status = 'success'
    } catch (ex) {
      api.log(ex)
      response.status = 'error'
      response.error = ex
    }
  }
}

module.exports = {
  SmartAgentHelloHello
}
```

## Testing

The easiest way to test is just to go to http://localhost:8080, and see if the new `hello` action is to be found.

The easiest way to test an actual request is with `curl`

```sh
$ curl -X POST -d "salut=Ciao!" "http://localhost:8080/api/smart-agents/hello/hello?apiVersion=1"

{
  "greeting": "Grüetzi, Ciao!",
  "status": "success",
  "serverInformation": {
    "serverName": "edge-server",
    "apiVersion": "0.9.0",
    "requestDuration": 33,
    "currentTime": 1526396750067
  },
  "requesterInformation": {
    "id": "ce8131e53aa7e38cd6feb54a83d8afb995876738-28650a51-f53f-4484-a015-ca89fa592166",
    "fingerprint": "ce8131e53aa7e38cd6feb54a83d8afb995876738",
    "remoteIP": "127.0.0.1",
    "receivedParams": {
      "apiVersion": "1",
      "salut": "Ciao!",
      "action": "smart-agents/hello/hello"
    }
  }

```
