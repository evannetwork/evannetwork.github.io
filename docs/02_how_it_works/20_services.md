---
title: "Services"
parent: How it works
nav_order: 20
permalink: /docs/02_how_it_works/services.html
---

# Services

evan.network services offer users and developers features to work with the blockchain, Smart Contracts and ÐAPPs in a familiar and accessible way.

To learn more about these services you should read the following guides:
  * [ENS](/docs/04_developers/ens.html) - evan.network names services
  * [ENS2DNS](/dev/ens2dns) - service to map ENS names to DNS names
  * [Identity Claim](/dev/identity-claims) - service to create trust claims at blockchain accounts

## ENS

ENS is the [Ethereum Name Service](https://github.com/ethereum/ens)<sup>[+]</sup>, adapted to the needs of evan.network. Normally a contract has a 32 byte hex ID, e.g. `0x06012c8cf97bead5deae237070f9587f8e7a266d`. The work with such IDs is not very convenient for users, especially if your system is based on ÐAPPs, where everything is a contract.

The ENS allows developers to give real/ speaking names to contract IDs like DNS does for IP Adresses in the Web.

The top level domain (TLD) for every name you can register is fixed to `.evan`

You can register custom ENS domainnames for your company or application and can register custom subdomains below your domain. We offer an ENS ÐAPP to register custom domains later, in the meantime you can contact the developers on [Gitter ENS](https://gitter.im/evannetwork/ens)<sup>[+]</sup>.

**NOTE:** All names you have registered in the public Ethereum blockchain are not available in evan.network.

## ENS2DNS

This gives you the possibility to reach every ENS name through a normal [DNS](https://en.wikipedia.org/wiki/Domain_Name_System)<sup>[+]</sup> resolution e.g. from the browser.

If you have registered an ENS name, e.g. `4711.digitaltwin.mydomain.evan`, and you have provided a [DBCP](/docs/04_developers/dbcp.html) spec with a working ÐAPP, then you can access this ÐAPP in the browser via `https://4711.digitaltwin.mydomain.evan`

The ENS2DNS service is in testing currently.

## Identity Claim

Trust in the integrity and identity of a business partner is one of the most important factors in digital communication. Today, we trust that, for example, the Email address of a recipient also belongs to the employee of a certain company, but this cannot be verified. In the evan.network users should be able to ensure that the account with which they conclude a Smart Contract also belongs to the respective network partner with whom they want to do business.

This function is provided by the identity service. In general, different proofs of identity, so-called claims, can be assigned to an account. For example, a claim is an entry of a company in the commercial register. Claims are managed by the owner of the respective account, but they are initially unconfirmed and not trustworthy. Therefore, there are trustworthy instances (so-called trusties) that can confirm specific claims. This enables an user to see, who confirmed the claim and whether it is trustworthy. Different claims can be deposited and confirmed for each account. For example, ISO certificates, supplier proofs, quality certificates, etc. can be specified.

The identity service itself does not store any data and content such as trade licenses or ISO certificates, but only confirms them. It is also not possible to trace which claims an account has. Proofs are only selectively released by the respective account upon request. This strengthens the confidence of a business relationship and at the same time safeguards data protection.
