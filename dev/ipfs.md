---
title: "IPFS"
---
# IPFS - Storage Service

To give evan.network applications the the possibility to run decentralized applications ([ÐAPPs](/dev/dapps)) and store complex and unstructured content, we provide a distributed file system based on [IPFS](https://ipfs.io)<sup>[+]</sup>.
The evan.network IPFS service is not connected to the public IPFS network so that you content isn't spread on other IPFS hosts outside our network. We provide a [private IPFS cluster](https://github.com/ipfs/go-ipfs/blob/master/docs/experimental-features.md#private-networks)<sup>[+]</sup> where each MasterNode provider spends instances to these IPFS network.

The storage service keeps care that a content asset is replicated 2 times in the cluster and that stored data cant be deleted anymore like in the blockchain.

You can reach the IPFS service at `https://ipfs.evan.network`. The service is shared between the **testcore** and **core** blockchain. There are several different APIs available to interact with IPFS, for JavaScript/NodeJS you can use [https://github.com/ipfs/js-ipfs-api](https://github.com/ipfs/js-ipfs-api)

If you store data to the evan.network IPFS storage, **you must** take care that you encrypt these data in a proper way, so that third parties can't read your data. To encrypt your data, you can use the evan.network [security APIs](/dev/security) or implement a custom way.

You can also use a custom IPFS or other datastore to persist your data. In the [DBCP](/dev/dbcp) guide is the possibility to specify alternative storage providers or you can write custom storage handlers in your ÐAPPs.
