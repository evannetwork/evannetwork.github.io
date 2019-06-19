---
title: "Event Hub"
parent: Developers
grand_parent: Concepts
nav_order: 4150
permalink: /docs/developers/concepts/event-hub.html
---

# Event Hub
The event hub is a smart contract deployed at `events.evan`, which is used by many contracts in the evan.network ecosystem for announcing status updates. Contracts that use the event hub include but are not limited to:
- Business Center
- [Mailbox](/docs/first_steps/core_apps/mailbox.html)
- [Data Contract](/docs/developers/concepts/data-contract.html)

It is a central contract, which other contracts locate via ENS lookup. The `EventHub` contract inherits from multiple base contracts which add events and event trigger functions to its functionality. Every contract, that uses the event hub, knows only a limited scope of its functions due to only knowing the event hub base class related to itself -e.g. the `MailBox` contract only knows the base class `EventHubMailBox` and can only trigger events for those.

![Event Hub inheritance](/docs/4000_developers/4100_concepts/img/eventhub_inheritance.png)