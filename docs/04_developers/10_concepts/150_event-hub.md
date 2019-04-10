---
title: "Event Hub"
parent: Developers
nav_order: 150
permalink: /docs/04_developers/event-hub.html
---

# Event Hub
The event hub is a smart contract deployed at `events.evan`, which is used by many contracts in the evan.network ecosystem for announcing status updates. Contracts that use the event hub include but are not limited to:
- [Business Center](/dev/business-center)
- [Mailbox](/tutorial/mailbox)
- [Data Contract](/dev/data-contract)

It is a central contract, which other contracts locate via ENS lookup. The `EventHub` contract inherits from multiple base contracts which add events and event trigger functions to its functionality. Every contract, that uses the event hub, knows only a limited scope of its functions due to only knowing the event hub base class related to itself -e.g. the `MailBox` contract only knows the base class `EventHubMailBox` and can only trigger events for those.

![Event Hub inheritance](/public/dev/eventhub_inheritance.png)