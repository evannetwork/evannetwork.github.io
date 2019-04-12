---
title: "Queue DApp"
parent: Developers
nav_order: 4394
permalink: /docs/developers/ui/dapps/queue.html
---

# Queue DApp

The queue DApp is the management point of the general data storage logic. Each DApp uses queues to
store data asynchronously, listen for updates and persist statuses of different storage steps. This
creates a non-blocking and stateful application.

Within the queue DApp, you can view several task that are running. You also can stop and delete
broken or unwanted jobs.

[![Queue DApp](/docs/4000_developers/4300_ui/4390_dapps/img/queue-2.png){:width="80%"}](/docs/4000_developers/4300_ui/4390_dapps/img/queue-2.png)

To open the DApp, wait until you see the queue working symbol in the top right of the screen and use
the "synchronization details" button at the bottom of the screen.

[![Side Panel loading](/docs/4000_developers/4300_ui/4390_dapps/img/queue-1.png){:width="30%"}](/docs/4000_developers/4300_ui/4390_dapps/img/queue-1.png)

In the case of an error, an red banner symbol is shown in the top right corner. Their you can retry
the data saving or send error logs to the evan.network management team.

[![Side Panel error](/docs/4000_developers/4300_ui/4390_dapps/img/queue-3.png){:width="30%"}](/docs/4000_developers/4300_ui/4390_dapps/img/queue-3.png)
