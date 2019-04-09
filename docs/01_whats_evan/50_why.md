---
title: "Why evan.network"
parent: What's evan?
nav_order: 5
permalink: /docs/01_whats_evan/why
---

# Why evan.network?

Good Question.
Why not use any other well-established and well-proven technology to implement the applications and software you need?
Why use a blockchain at all?
Why use ethereum?
And why not use any other ethereum framework?

Well, those are three questions, and they need three separate answers.

## Why use Blockchains?

[Blockchains](https://en.wikipedia.org/wiki/Blockchain) are slow, can't hold a lot of data, and anything you do and change needs to be paid for in hard cryptocurrency. Why would anyone do anything with this?

All this is true, but in exchange you gain capabilities that sufficiently address and even solve quite a few long-standing and nagging problems inherent in all computing.

All of computing is based on the fact, that copies are cheap and changes are cheap and that bits are just bits. For this reason, historically it has proven an intractable problem to establish any kind of trust and authoritative consensus on any kind of data.

Blockchain technology changes this. It gets rid of mutable copies, because there is only one consensus record, and any change to it can only happen by consensus. Maintaining competing copies and versions within a blockchain becomes prohibitively expensive, via cryptographic means, and as a result there is an authoritative consensus on the data in the blockchain.

### Trust without the Blockchain
Establishing trust in data in any traditional environment is ultimately always done via real world social side channels. You exchange access points and credentials in person, or via digital channels that have trust from real world context. Still, every new access of data over any such traditional digital channels is a leap of faith that the chain of trust that led you to accessing this data at that specific access point with those specific credentials is still valid, that nothing has been compromised on either end or any link on the chain.

### Trust with the Blockchain
With the blockchain, there is only one real leap of faith: the leap to join the blockchain.
Once you are in you can trust that everyone who participates in it, whether you know them or not, agrees on the global state, and agrees on the process to change it.

Mistakes can of course still happen, but it is impossible to cover them up, or hide anything. They can only be corrected after the fact, if first everyone affected agrees on a chain of transactions to correct it, and then everyone else in the blockchain gives their blessing by validating the transactions.

## Why use Ethereum

[Ethereum](https://ethereum.org/) is the programmable blockchain. This means you get all the advantages (and disadvantages) of the block chain, but you are not restricted to a predefined set of possible transactions, you can freely define and program your own transactions, and are free to implement anything that is feasible within the computational and storage restrictions of a blockchain.

So as the basis of a truly distributed and trusted application framework with open scope, ethereum is the best available candidate.

## Why use evan.network specifically?
There are many instances of ethereum blockchains, each for their own specific purposes. This is even encouraged by the ethereum foundation. And it is safe to say that there are a few distributed application frameworks among them.

What makes the evan.network unique among them, and especially useful for distributed business relations of independent partners?

**First**, it establishes a blockchain where participation is exclusive to vetted business entities. This drastically reduces the transaction overhead and noise that is inherent in anything that is accessible to the general public. It is ensured that all participants provide a minimum level of infrastructure and resources and have a minimum level of competence and experience. This is ensured by the [AuthorityNodes](/doc/authoritynode). As a result evan.network has ~4s transaction times in contrast to the ~15s of the standard ethereum chain.

**Second**, there is a standardized dedicated protocol for business transactions. Anyone can do anything within an ethereum blockchain, but if everyone does their own thing and implement their own protocols, interactions between different mutually unknown parties still become problematic, if they don't understand each other, even if there is a basic mutual trust. Because everyone in the evan-network uses [DBCP](/dev/dbcp) to describe their contracts and messages, you can know what they do before actually running them or examining the byte code. You have a common human-readable language.

**Most importantly**, evan.network provides libraries and APIs and services that seamlessly integrate all the different components to allow developers to write their services and applications quickly and safely.
As an example, not all data can be stored directly in the blockchain for space reasons. But we provide an easy to use API to securely reference large data objects in a distributed storage with multiple levels of encryption. No need to reinvent the wheel every time this requirement inevitably comes up again.

