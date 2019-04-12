title: "HowTos"


If you just want to do quick tests, it is best to just use the [evan.prompt](/docs/developers/tooling/evan.prompt.html). You will also find a small example of how to compile and deploy contracts to evan.network there.


# Load and Connect to a Contract Instance

This happens unsurprisingly with the conract loader. Open `bccc.js`

```js
> var interface_definition = cc('Hello').contracts[0].interface
> bcc.contractLoader.contracts['HelloWorld']({ interface: interface_definition })
> var hello = bcc.contractLoader.loadContract('HelloWorld', '0xACC07...1D')
```

Now you have a usable Web3 contract instance object to work with. You do always need the interface, but of course you don't need to compile the source code every time you get to the interface. You only need to do this once and then save the string and reuse it. Or even better, put it into the [DBCP](/docs/developers/concepts/dbcp.html) and let this take care of everything.

Of course, you also have to say which instance of this contract on the blockchain you want to interact with, that's why you need to know the account ID and pass it to `loadContract`.


# Call Readonly Contract Methods

There is a fundamental difference between reading and writing accesses on the blockchain. Reading is free and everyone can read everything, writing costs gas and is usually restricted. That's why there are two different methods to read from and write to the blockchain. In either case, it is an ansynchronous operation running over the net.
You can't use `await` on the REPL though. But this shouldn't be too much of a problem, since on the REPL you can always wait for it to finish and on evan.network transactions shouldn't take more than 4 seconds anyway.

The downside is you have to write callbacks, if you want to get to the values.


```js
>
```

# Execute Transactions

# Deploy Public Documents

Public documents are just documents stored in the distributed file system, accessible by anyone,
and the hashes of those documents are used in a DBCP file or a contract somewhere.

# Deploy Private Documents: Envelopes

Since the data in distributed file systems is accessible to anyone, the only way to have private data is to encrypt the data. In the standard evan.network DataContracts, the links/ hashes to the documents that are stored in them are also encrypted, to prevent external data miners from connecting specific datasets with specific contracts.

All this is handled automatically by the blockchain core library with envelopes.

```js
bcc.dfs.
```

# Publish Documents with ENS

# Exchange Communication Keys with other User

# Creating and using DBCP API Files
A main feature of evan.network is to be able to streamline the interaction between applications running outside the blockchain while using it and the contracts on the blockchain with a specification file.

One of the things that is made possible by this feature is the automatic updating and redeploying of contracts belonging to an application. The format is a normal JSON file.

```json
{
  "public": {
    "name": "Hello",
    "dapp": {
      "entrypoint": "task.js",
      "files": [ "testContract.js" ],
      "origin": "Qm...",
      "standalone": true,
      "type": "dapp"
    },
    "description": "Create todos and manage updates.",
    "dbcpVersion": 1,
    "i18n": {
      "description": {
        "de": "Erstelle Aufgaben oder zeige sie an",
        "en": "Create tasks or show them"
      },
      "name": {
        "de": "Task",
        "en": "Task"
      }
    },
    "imgSquare": "data:image/png;base64,...",
    "dataSchema": {
      "list_settable_by_member": {
        "$id": "list_settable_by_member_schema",
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "foo": { "type": "string" },
          "bar": { "type": "integer" }
        }
      },
      "entry_settable_by_member": {
        "$id": "entry_settable_by_member_schema",
        "type": "integer",
      }
    },
    "abis": {
      "own": [
        "contract abi..."
      ]
    },
    "source": "Qm...",
    "version": "1.0.0",
  }
}
```


