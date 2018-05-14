---
title: "Hello Agent"
---

# Hello Agent

Lets write a smart agent, so we can interact with the blockchain via a normal web service without installing all the blockchain services and libraries on every computer.

## Prerequisites

In the evan.network the established way to write web services is to use the [`edge-server`](https://github.com/evannetwork/edge-server), which is just an [ActionHero](https://www.actionherojs.com/) with some added infrastructure. It also uses the version "^18.0", so asynchronous programming with callbacks is discouraged now.

Installation is rather straightforward.

```sh
$ git clone git@github.com:evannetwork/edge-server.git
$ cd edge-server
$ nvm i
```

This should also automativally install the blockchain-core libraries and all other dependencies in `node_modules/`, which can take a while. 

If all is done test it and start it with 

```sh
$ npm start
```

You should now be able to see the action-hero admin interface on `https://localhost:8080`.

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
    }
  }
}
```

You need the account id, because you want to be able to change the contract data, and by default only the owner/creator can do writes on contracts.

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

  api.smartAgentHello = {
    setMessage: (msg) => {

      // you not only "export" through the api object
      // you also import through it, the configuration for example
      const account = api.config.smartAgentHello.account
      
      // but also the blockchain core library
      const result = api.bcc.executor.executeContractCall({
        'from': account,
        'msg': msg,
      }, (error,receipt) => {
        if(error) return reject(error)
        else return resolve(receipt)
      })
      
      // as you can see, the bcc functions generally implement the usual
      // asynchronous callback interface
      // its easy to turn them into promises
      
    }
  }

  async initialize() {
  
    if (config.disabled) return
    
  }
  
  async stop() {}

}

```
