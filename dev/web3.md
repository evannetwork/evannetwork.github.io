---
title: "Web3"
---

# Web3
Web3 is a collection of Ethereum API modules to interact with a remote Ethereum node and so directly with the evan.network. You can create your own web3 instance or use a browser plugin like [MetaMask](https://metamask.io/)<sup>[+]</sup> to manage your connection.


## With an own web3 instance
You can create a web3 instance and perform your calls against evan.network via HTTPS and WebSocket providers. Throughout the web3 1.x API is used, you can find the detailed [official API documentation here](https://web3js.readthedocs.io/en/1.0/index.html)<sup>[+]</sup>.

{% include jsfiddle.html fiddle="wulfraem/L26tzuhq" tabs="js,result" %}

Contract calls can of course be executed in the same way.

{% include jsfiddle.html fiddle="wulfraem/7qqvkffg" tabs="js,result" %}

Although this is a possible way to interact with the network, it is recommended to rely on the API framework, as it acts as an abstraction layer for interacting with the evan network and makes complex operations far easier.


## With MetaMask
If you want to use MetaMask for connnecting to evan.network, you can do this by adding the custom RPC endpoint `https://testcore.evan.network` to your endpoints.

MetaMask uses the 0.x version of web3, you can find documentation for it in the [Ethereum wiki](https://github.com/ethereum/wiki/wiki/JavaScript-API)<sup>[+]</sup>

If you have MetaMask installed and added the custom RPC endpoint to your MetaMask, the following samples work the same way as the previous ones:

{% include jsfiddle.html fiddle="wulfraem/f1deLs3j" tabs="js,result" %}

{% include jsfiddle.html fiddle="wulfraem/qg9o0b8k" tabs="js,result" %}
