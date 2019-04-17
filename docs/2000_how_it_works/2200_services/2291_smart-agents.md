---
title: "Smart Agents"
parent: How it works
grand_parent: Services
nav_order: 2291
permalink: /docs/how_it_works/services/smart-agents.html
---


# Smart Agents

![Smart Agent](/docs/2000_how_it_works/img/smart_agent.png){:width="100px"}

Smart Agents are services that are connected to the blockchain and support on-chain actions with off-chain data and functionalities. This allows integrating external system into the blockchain. These Smart Agents can also act as an [Oracle](https://cointelegraph.com/explained/blockchain-oracles-explained), to add complex decision logics to your Smart Contracts.

Examples for Smart Agents are:
- **onboarding** Smart Agent<br>

  The onboarding Smart Agent acts as the entity that brings new users into evan.network. It takes care of creating the user profile and infrastructure. It also handles invitations from users already in evan.network and a bridge between users, who already have an evan.network account and people they wish to invite. The agent takes care of sending them notifications and transferring starting-EVEs to allow the new users to start working.<br>

- **notification** Smart Agent<br>
  This agent watches for updates on the blockchain and sends users, who are subscribed for, notifications.
- **oracle** Smart Agents<br>
  These agents enrich blockchain data with off-chain data. An example is the "weather agent" that can be invited into a task contract. If this agent has been invited and a ToDo requesting weather information is added, it responds with the current weather at the requested location.


## Edge Server
Smart Agents are implemented as plugins for the Edge Server, a `node.js` web application platform based on [ActionHero](http://actionherojs.com) that includes the [blockchain-core](/docs/developers/api/blockchain-core.html) library to connect to `evan.network`.

A [public repository](https://github.com/evannetwork/edge-server-seed) exists for Edge Server as a seed for developers to implement their own Smart Agents on top of.
