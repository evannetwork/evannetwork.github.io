---
title: "IPFS file handling"
parent: How it works
grand_parent: Services
nav_order: 2260
permalink: /docs/how_it_works/services/ipfsfilehandling.html
---

# IPFS file handling

## Storage Service

To give evan.network applications the possibility to run decentralized applications ([ÐAPPs](/docs/developers/ui/basics.html)) and store complex and unstructured content, we provide a distributed file system based on [IPFS](https://ipfs.io).
The evan.network IPFS service is not connected to the public IPFS network, so that your content isn't spread on other IPFS hosts outside our network. We provide a [private IPFS cluster](https://github.com/ipfs/go-ipfs/blob/master/docs/experimental-features.md#private-networks) where each AuthorityNode provider spends instances to this IPFS network.

The storage service keeps care that a content asset is replicated up to five times in the cluster.

You can reach the IPFS service for the **testcore** at `https://ipfs.test.evan.network` and if you want to reach the public IPFS service for the **core** blockchain, please got to `https://ipfs.evan.network`. There are several different APIs available to interact with IPFS, for JavaScript/NodeJS you can use [https://github.com/ipfs/js-ipfs-api](https://github.com/ipfs/js-ipfs-api)

If you store data to the evan.network IPFS storage, **you must** take care that you encrypt these data in a proper way, so that third parties can't read your data. To encrypt your data, you can use the evan.network [security APIs](/docs/developers/concepts/smart-contract-permissioning.html) or implement a custom way.

You can also use a custom IPFS or other datastore to persist your data. In the [DBCP](/docs/how_it_works/services/dbcp.html) guide is the possibility to specify alternative storage providers or you can write custom storage handlers in your ÐAPPs.


## Hybrid Storage
Storing large amount of data becomes rather expensive and difficult to execute due to blocksize limitations, so "contents" of contracts are uploaded to the IPFS and only the reference to the file is stored in the contract.

This keeps the amount of data quite small, but allows adding arbitrary large files to contracts without exceeding blockchain limitations or making the transactions too expensive.

ENS addresses can point to a description as well, they keep a reference to a [DBCP](/docs/how_it_works/services/dbcp.html) description, which may point to [ÐAPPs](/docs/developers/ui/basics.html) and contract data, assets, etc. related to the contract.

The _DBCP descriptions_ are hosted to evan.network IPFS storage, _assets_ can be stored in a custom IPFS or datastore. _ÐAPPs_ may be hosted in a custom location as well, but it is recommended to host these in the evan.network IPFS storage to keep the user experience fluent without having the user switch servers during navigation.
