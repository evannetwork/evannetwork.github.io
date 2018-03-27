---
title: "IPFS"
---
# IPFS - Storage Service

To give evan.network applications the the possibility to run decentralized applications ([DAPPs](/dev/dapps)) and store complex and unstructured content, we provide a distributed file system based on [IPFS](https://ipfs.io)<sup>[+]</sup>.
The evan.network IPFS service is not connected to the public IPFS network so that you content isn't spread on other IPFS hosts. We provide a [private IPFS cluster](https://github.com/ipfs/go-ipfs/blob/master/docs/experimental-features.md#private-networks)<sup>[+]</sup> where each MasterNode provider spends instances to the network.

You can reach the IPFS service at `https://ipfs.evan.network`. The service is shared between the **testcore** and **core** blockchain. 

If you store own data to the evan.network IPFS service, **You** should take care that you encrypt this data in a proper way, so that third parties can't read your data. To encrypt data you can use the evan.network APIs or implement a custom way.

You can also use a custom IPFS or other datastore to persist your data. In the [DBCP](/dev/dbcp) guide is the possibility to specify alternative storage providers or you can write custom data handlers.  
