---
title: "evan.prompt"
---
# evan.prompt

The simplest way to just start playing with evan network is to install the `evan.prompt`.

It connects you to evan.network and allows you to interact with the [programmers API](https://github.com/evannetwork/blockchain-core)

Don't let the name fool you, this is not just for working with blockchain contracts, the `evan` command line tool can be used to interact with all components of `evan.network`, i.e. also the [IPFS](/dev/ipfs) file stores, the [ENS](/dev/ens) etc.

# Installing

Installing the `evan.prompt` is as simple as 

```sh
$ npm i evan.prompt
$ cd evan.prompt
$ chmod a+x evan
```

# Configuration

You will have to configure `evan` at least with your evan.network account information.
So once you have [created a profile](/tutorial/create-identity), you will need to copy your account ID, your private key and profile encryption key from the [dashboard](/tutorial/dashboard), and put them into your `$HOME/.evan.json`.

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

You can configure more than one account with its keys, but the default that will be used will always be the first one.

There are additional configuration options outside the accounts, but they are optional.
You can overwrite the default `dfs` (distributed file system server) and `web3` (web3/ethereum client) options,
if you have instances running on your local machine or network.

You can also set a list of directories to search for solidity files for compilation or DBCP files for uploading them.
If you don't set any absolute or relative paths there, the compiler will only look in the current directory.
Absolute paths are searched as is, relative paths are resolved first relative to the home directory, then relative to the current directory.

# Starting the program

You will need to have configured your accounts and you will need to have conncectivity to your configured web3 and IPFS endpoints.

A quick look at the options:

```sh
$ ./evan --help

  Usage: evan [options]

  Options:

    -V, --version                                 output the version number
    -C, --Contracts                               list known contracts
    -c, --compile <files.sol>                     compile contracts from comma separated list of files
    -n, --new <file.sol>[;args[;gas]]             compile and create new contracts
    -f, --fabricate <factory>[;args;gas;invites]  create a new contract with a factory
    -d, --dbcp <file.json>;<file.sol>             deploy a whole dbcp application
    -u, --update <ens>=<file.sol>                 update a dbcp application
    -U, --Upload <files>                          upload file to dfs and give contract friendly hash
    -l, --load <accountID or ENS>                 load contracts that have DBCP descriptions
    -L, --Load <accountID or ENS>[=file.sol]      load contracts that have no dbcp descriptions
    -r, --require [name=]<file>                   load module from file into table M
    -e, --eval <script>                           evaluate script, can use await
    -a, --account <int>                           select account to use by index (default: 0)
    -i, --interactive                             start interactive console, cannot use await, default
    -h, --help                                    output usage information
```

It provides an easy command line interface to a lot of tasks developers will have to do quite often when developing for `evan.network`. Among them are activities like compiling, creating and loading contracts, in all the different ways that are available. But it also allows you to evaluate commands directly from the command line, or to load and execute ECMAScript files.

Or just start an interactive prompt and start exploring.

It starts  a `nodejs` REPL with a configured [blockchain-core](https://github.com/evannetwork/blockchain-core) library under `bcc`, also an `IPFS` and `Web3` object and some more, which can be explored with tab completion.

You can also directly pass code on the command line to eval, although with a slightly less defined environement.

```sh
$ ./evan -e 'bcc.accounts'
['0xDE56...235aC' ...]

```
## Work Order

All options are executed in the specific order in which they appear in the help message. This means later options can utilize the work done by earlier commands. This is primarily interesting for the `-r` and `-e` and `-i` options, and it's the reason the contract loading options are useful. This is because it means contracts created or loaded earlier are available to use in eval and requires commands as well as in the prompt when it starts. Requires are available for evals and the prompt, and evals have been executed before the prompt starts.


## Hashing Lookup Keys

A task that can be quite annoying when setting up new applications that don't run in the browser and that need to be run under specific accounts and have to commununicate with other users, profiles and contracts is the configuration of the encryption and communication keys needed to do this. You need to make sha3 hashes of account IDs and you need to make combined hashes of account IDs as lookup key for the edge keys of two partners to access each others data.

```js
// normal sha3 hashes to look up your private profile access key / identity key
> sha3('0x20a6E2feD0e1243895761Badfebce9D064aB1777')
'0xd4c0f23fa26fb73f41a10e5824f894841354fdaf1de360303e2c8237a35e896e'

// the lookup key to get the shared porfile encryption key of two users (or for reading your own encrypted data)
// is generated with the 'special' sha9 function

// two accounts can read each others data with the key saved under this lookup key
> sha9('0x20a6E2feD0e1243895761Badfebce9D064aB1777','0x20a6E2feD0e1243895761Badfebce9D064aB1111')
'0x19cd2bd638f8f9e1148bf2539a5bbc7dd3e52ed2f440ee9f30f83815982a4ab2'

// to read your own encrypted profile data, save the normal profile encryption key
// that is generated on profile creation under a lookup key with yourself
> sha9('0x20a6E2feD0e1243895761Badfebce9D064aB1777','0x20a6E2feD0e1243895761Badfebce9D064aB1777')
'0xbe40ae99253d7183c9fbee72ebaddc0604b77116e0dd6ee29c8538314330301d'
```

## Key Exchange: Generating Communication Keys
Usually this is done for you in the `evan.network` dashboard and contacts application. There are also APIs available to do key exchanges dynamically at runtime.

It is also a common use case to have rarely changing group peers that need to communicate. In this case you need to be able to generate the necessary keys to enable this. Therefore, you can put them in config files to iniate key providers with them.

```ja
>
```

# Compiling and Creating Contracts

Now that everything is installed and configured, let's take our [Hello World contract](/dev/hello-world) and deploy it with the evan.network toolchain instead of truffle.

The option to compile solidity files is `-c`. It will search your included paths and compile all the files it finds.


```sh
$ .evan -c hello.sol,hola.sol -c hello.sol
```

All files that are given at the command line, either from a compile or any other option that can have solidity files, will only be compiled once at initial start and then cached, even if they are given multiple times.

Compiled contracts are also put into the `CC` dictionary, as well as into the `bcc.contractLoader` dictionary.

When you start a compile from the prompt, it will always be compiled. The main options are available from the option object `o`, so all you have to do is:

```javascript

> let compiled_contracts = o.c([ 'hello.sol', 'hola.sol'])
Found  /home/myusername/contracts/hello.sol
Found  /home/myusername/contracts/hola.sol

```

If you just compile files, nothing happens yet on the blockchain and you could use any other `solc` command line tool just in the same way.

What the other tools can't do is to directly pass the compiled bytecode and interface definitions to the blockchain-core API for you.

The simplest example for this is to compile a contract and create a new instance of it on the `evan.network` blockchain.

```sh
$ ./evan -n hello.sol -n another_contract.sol
Found  /home/myusername/contracts/hello.sol
Found  /home/myusername/contracts/another_contract.sol
Created new instance of HelloWorld: 0xad344e3454b23...4229
Created new instance of TestContract: 0x12....3214af23
```
No matter by which option you create or load a contract, it will be put into the `C` dictionary under its account ID and/ or ENS.

Some contracts may require additional arguments or more gas to deploy than is given by default. These additional parameters are appended after semicolons, which means you have to enclose the whole parameter's string in quotes. Since contract arguments are given as JSON objects, this is necessary anyway.

```sh
$ ./evan -n 'some_contract.sol;{ "value": "0" };200000'
Found  /home/myusername/contracts/some_contract.sol
Created new instance of Something: 0xad37774e3454b23...4229
```

## Contract Factories

## DBCP

# Loading Contracts

Whenever possible you should use and load contracts that have DBCP descriptions. So when you know a contract has
a DBCP description, then all you need to do is pass its address/ ID or if it has, its ENS address.

```sh
$ ./evan -l 0x54abc....324514af23

```

This loads the contract and puts it into `C['0x54abc....324514af23']`. It also loads the DBCP description and puts it into `D['0x54abc....324514af23']`.

You can also load contracts without DBCP description. But to do so and have them be usable you have to get the ABI
by other means. For default contracts and contracts you have compiled previously this is already the case.

```sh
$ ./evan -L 0x579492375bc...947ae=DataContract

```

Here only the contract is loaded into `C['0x579492375bc...947ae']`. The `-C` option shows you all available contract ABIs that can be used this way.

If you don't have this you can pass a solidity filename, which will be compiled normally (unless it has been compiled in an earlier command option already), and then the ABI is extracted from the compile result and used.

```sh
$ ./evan -L 0x5794fff75bc...947ae=mycontract.sol
```

# File Upload and Download
IPFS is heavily used in `evan.network`. Not just to store data too big to be stored directly in contracts, the ÐApps themselves or the descriptions. So the necessity to quickly upload files arises only occasionally.

```sh
$ ./evan -U file0.txt,file1.png -U directory/file2.json
```
The files are searched for in the configured included paths in the same way as in solidity files for compilation.
The returned hashes are not the normal IPFS hashes, but the ones used internally in contracts.

By default the files are uploaded unencrypted. If you want to encrypt them before uploading them, use the `-a` option, and they will be encrypted with the private key of the given account.
