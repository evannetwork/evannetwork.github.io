---
title: "evan.prompt"
---
# evan.prompt

The simplest way to just start playing with evan network is to install the `evan.prompt`.

It connects you to evan.network and allows you to interact with the [programmers API](https://github.com/evannetwork/blockchain-core)

Don't let the name fool you, this is not just for working with blockchain contracts, the `bccc` can be used to interact with all components of the evan.network, i.e. also the [IPFS](/dev/ipfs) file stores, the [ENS](/dev/ens).

# Installing

Installing the `evan.prompt` is as simple as 

```sh
$ npm i evan.prompt
$ cd evan.prompt
$ chmod a+x evan
```

# Configuration

You will have to configure `bccc.js` at least with your evan.network account information.
So once you have [created a profile](/tutorial/create-identity), you will need to copy your account ID, your private key and profile encryption key from the [dashboard](/tutorial/dashboard), and put them into your `$HOME/.bccc.json`.

```json
{
  "accounts" : {
    "0x0d...32d": {
      "private_key": "cf...d21fd",
      "profile_key": "7a...b56"
    }
  },
  "dfs": { "host" : "localhost", "port" : "8080", "protocol" : "http" },
  "web3" : "ws://localhost:8546",
  "sourceFiles" : [ "contracts" ]
}
```

There are additional configuration options outside the accounts, but they are optional.
You can overwrite the default `dfs` (distributed file system server) and `web3` (web3/ethereum client) options,
usually if you have instances running on your local machine or network.

You can also set a list of directories to search for solidity files in for compilation.
If you don't set any absolute or relative paths there, the compiler will only look in the current directory.
Absolute paths are searched as is, relative paths are resolved first relative to the home directory, then relative to the current directory.

# Exploring with the REPL

Just start the console:

```sh
$ ./bccc.js
```
you then have a `nodejs` REPL with a configured [blockchain-core](https://github.com/evannetwork/blockchain-core) library under `bcc`, also an `Ipfs` and `Web3` object and some more, which can be explored with tab completion.

You can also directly pass code on the command line to eval, although with a slightly less defined environement.

```sh
$ ./bccc.js 'bcc.accounts'
['0xDE56...235aC' ...]

```


# Compiling and Deploying Contracts

Now that this is installed and configured, let's take our [hello world contract](/dev/hello-world) and deploy it with the evan.network toolchain instead of truffle.

bccc.js privides a `cc` function to compile a contract, and a `ccup` function to compile and deploy a contract onto the blockchain. 

Run `bccc.js` for the REPL.

```javascript

// looks for 'hello.sol' file in the search directories, and then current directory
// and compiles it
> cc('hello.sol')

// compiles the given file, and then uploads it to the blockchain, returns new contractID
> let hello = ccup('hello.sol')
Found  /home/myusername/contracts/hello.sol
Uploading  HelloWorld to evan.network

// hello is now a normal web3 contract instance
// you can additionally pass a new gas limit if the default is not enough
// and arguments for the contract creation
> let hello = ccup('hello.sol', 200000, 'zzzzzz')
Found  /home/myusername/contracts/hello.sol
Uploading  HelloWorld to evan.network
```

It is equally possible to do it directly from the command line, but here it doesn't return a complete contract instance, you couldn't do anything with it anyway, but just the new contract ID is printed.

```sh
$ ./bccc.js 'cc("hello.sol")' 'cc("another_contract.sol")'
Found  /home/myusername/contracts/hello.sol
Uploading  HelloWorld to evan.network
0x12....3214af23
Found  /home/myusername/contracts/another_contract.sol
Uploading  TestContract to evan.network
0x12....32888f23
```

To 
To use proper evan.network DataContracts and [DBCP](/dev/dbcp) take a look at the [HowTos](/dev/howtos)
