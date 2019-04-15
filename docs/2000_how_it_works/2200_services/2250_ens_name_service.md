---
title: "ENS name service"
parent: How it works
grand_parent: Services
nav_order: 2250
permalink: /docs/how_it_works/services/ensnameservice.html
---

# Namespaces

The blockchain consists of a large amount of hashes ... of profiles ... smart contracts ... or DApps. When someone deploys a smart contract on evan.network, the contract gets a unique hash/id where the new contract can be called.

On the internet we have the same scheme with ip addresses. When you call www.google.de the browser calls the DNS server for the ip address of the url. and you browser calls the ip of the dns entry

On evan.network we have deployed the derivat of the DNS ... the Ethereum Name Service (ENS). With this service we can provide unique namespaces for DApps and identities on the platform. With the help of unique namespaces your blockchain applications and identities receive a human-readable address.

Just as with normal URLs this makes it possible for your DApps to be reachable from the WWW without any additional tools needed.

You don’t need to get used to complex new addresses, such as ‘0x2910543' when you want to call an application.
Instead, you can make use of the more straightforward Ethereum Name System, enabling addresses such as for example 'nodeone.evan'.

The namespaces on evan.network lay on top of the ENS, the Ethereum Name System. The ENS itself is built on smart contracts, removing all the insecurities of the normal DNS system in the process.

On a technical level that means for you that your security is going to be improved by an additional built-in platform layer, as DNS hijacking is a concern of the past – domain names will always work as they are intended to. This fact eliminates even one of the most subtle of all hijacking techniques.

Platform users can register their own domains through a DApp. Registering a domain on the evan network requires a one time fee, mainly to discourage from submitting spam to the registrar.

For testing purposes you may use the network's demo subdomain *.fifs.registrar.test.evan.

Using the subdomain doesn't come at any cost. [Follow this guide to claim a demo domain.](https://medium.com/evan-network/dev-series-deploy-your-%C3%B0app-on-the-evan-network-4f4232861249)
