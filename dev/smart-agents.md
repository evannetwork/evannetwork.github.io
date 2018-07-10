---
title: "Smart Agents"
---

# Smart Agents

![Smart Agent](/public/dev/smart_agent.png){:width="100px"}

Smart Agents are services, that are connected to the blockchain and support on-chain actions with off-chain data and functionalities. This allows integrating external system into the blockchain. These Smart Agents can act also act as an [Oracle](https://cointelegraph.com/explained/blockchain-oracles-explained)<sup>[+]</sup>, to add complex decision logic to your Smart Contracts.

Examples for smart agents  are:
- **onboarding** smart agent<br>
  
  The onboarding smart agent acts as the entity that brings new users into evan network. It takes care of creating the user profile and infrastructure. It also handles invitation from users already in ev a bridge between users, that already have an evan.network account and people, they wish to invite. The agent takes care of sending them notifications and transferring starting [EVE](/dev/blockchain#eve---token)s to allow the new users to start working.<br>
  It also 
- **notification** smart agent<br>
  This agent watches for updates on the blockchain and sends users, that subscribed for those, notifications.
- *oracle* smart agents<br>
  These agents enrich blockchain data with off-chain data. An example is the "weather agent", that can be invited into a task contract. If this agent has been invited and a ToDo, that requests weather information, is added, it responds with the current weather at the requested location.

To learn how to create smart-agents, take a look at our [tutorial example](/dev/hello-agent).

## Edge Server
Smart Agents are implemented as plugins for the Edge Server, a `node.js` web application platform based on [ActionHero](http://actionherojs.com) that includes the [blockchain-core](blockchain-core-link) library to connect to `evan.network.

A [public repository exists for edge-server](https://github.com/evannetwork/edge-server-seed), as a seed for developers to implement their own smart agents on top of.
