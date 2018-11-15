---
title: "IoT Security"
---
# IoT Security 

In the age of interconnectivity in which not only people but thousands of devices, small to large, are always connected and communicate with each other, security becomes ever more critical. 
To avoid coming up with or implementing secure measures on your own, you can rely on the secure IoT connectivity aspect of evan.network. 
Built-in IoT security is a crucial feature of the platform's holistic approach.

As an example of how this is done, let’s take a look at how on a technical level, you would unlock your car that is part of the evan.network:

When you hit the unlock button on your remote, the signal is processed by a masternode. The masternode is the endpoint receiving the request to unlock your car. Once the masternode verifies that it is you, it will allow for the vehicle to be opened.

However, it could be the case that someone might attempt to compromise a masternode they have control over and try to open your car without your consent. 


IoT devices, in our case a car remote control, send an RPC request to an AuthorityNode.

To verify that the response is valid, the device has to examine three factors:

*	[The merkle proof](https://medium.com/byzantine-studio/blockchain-fundamentals-what-is-a-merkle-tree-d44c529391d7)
*	The current blockheader
*	A signed blockhash from the same blockheader from multiple Authority nodes 

Authority nodes themselves are discouraged from becoming malicious by a deposit each node operator has to consign. If one of those nodes were to sign a wrong or fraudulent request, the deposit of that node is consumed as a penalty. 
The IoT device can publish the information to put it up for verification by the network, in which case the deposit would be transferred to the watchdog that caught the error.
However, since the IoT device asks multiple nodes to sign the blockhash, it is possible for the device to verify the response and even claim the deposit in case a blockhash was falsely signed.



