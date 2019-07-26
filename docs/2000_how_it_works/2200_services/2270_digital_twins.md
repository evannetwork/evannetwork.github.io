---
title: "Digital Twins"
parent: How it works
grand_parent: Services
nav_order: 2270
permalink: /docs/how_it_works/services/digitaltwins.html
---


# Digital Twins

evan.network gives you the ability to digitize your machines/components/assets with Digital Twins. A Digital Twin can be basically every physical asset in the real world. When you create a new representation on evan.network you can store different data sets on the twin. These information are stored immutably on the blockchain as a smart contract.

## Interact with Digital Twins
Use the [Digital Twin Management](/docs/first_steps/power_apps/digital-twin.html).

## Functional Concept
The Digital Twin, acts like a simple catalog of "contract links". Each contract that can be linked into the Digital Twin is called a <b>Plugin Instance</b> or technical, <b>Data Container</b>. Each Plugin contains information about permissions, user interfaces and data specifications (so called Data Sets) including their format and validation. As a result of this, generic and reusable Plugins can be created, that can be instantiated into any Digital Twin. The Plugin configurations will be copied and written into the instantiated Plugin. This instance is a separate contract, so it's standalone and can be shared and edited separately to the Digital Twin. Also, it can be imported into any other Twin, e.g. to manage global batch of industry product metadata.

[![my Plugins](/docs/2000_how_it_works/img/digital-twin-apidoc-images-7-functional-ui.png){:width="100%"}](/docs/2000_how_it_works/img/digital-twin-apidoc-images-7-functional-ui.png)


## Real World Example
For example, a machine manufacturer wants to create digital representations of machines built by him to track the production internal processes which were done in the past. This data is stored securely on the Digital Twin of the machine. Besides the production data he stores references to manuals or service information about the machine.

When the manufacturer sells the machine, he also shares different data containers / plugin instances to the new owner like service information or other data related to this machine. The new owner creates his own Digital Twin of the machine and can now attach the shared information from the manufacturer to his representation of the machine where he owns the data. The production information aren't shared to the customer so that only the manufacturer can access the data.

At this point the machine has 2 different Digital Twins which represent different views about the machine.

The owner of the machine can now add additional services like a rental module to the Digital Twin and enable new capabilities on the twin which can't be accessed by the manufacturer.

Digital Twins on evan.network have a very open concept which can be adapted to every physical asset on the real world. You can handle which persons you give access to specific data elements stored on the Digital Twin.
