---
title: "Smart Agents"
---

# Smart Agents

![Smart Agent](/public/dev/smart_agent.png){:width="100px"}

Smart Agents are services, that are connected to the blockchain and support on-chain actions with off-chain data and functionalities. This allows integrating external system into the blockchain. 

Examples for smart agents  are:
- onboarding smart agent<br>
  The onboarding smart agent acts as a bridge between users, that already have an evan.network account and people, they wish to invite. The agent takes care of sending them notifications and transferring starting EVEs to allow the new users to start working.
- notification smart agent<br>
  This agent watches for updates on the blockchain and sends users, that subscribed for those, notifications.
- oracle smart agents<br>
  These agents enrich blockchain data with off-chain data. An example is the "weather agent", that can be invited into a task contract. If this agent has been invited and a ToDo, that requests weather information, is added, it responds with the current weather at the requested location.