---
title: "Digital Twin Management"
parent: "First Steps"
nav_order: 3410
grand_parent: "Power Applications"
permalink: /docs/first_steps/power_apps/digital-twin.html
---

# Digital Twin Management
The Digital Twin Management is a generalized application for handling digital representations of real world assets.

- For a detailed overview of <b>what a Digital Twin</b> is and how it works <b>functionally</b>, have a look at:
  - [Functional Overview](/docs/how_it_works/services/digitaltwins.html)
- For a <b>detailed technical deep dive</b> and how to access digital twins as a developer, have a look at:
  - [Digital Twin API](https://api-blockchain-core.readthedocs.io/en/latest/contracts/digital-twin.html)
  - [Data Container API](https://api-blockchain-core.readthedocs.io/en/latest/contracts/container.html)
  - [Usage Examples](https://api-blockchain-core.readthedocs.io/en/latest/contracts/digital-twin-usage-examples.html)

## Start using
The application is based on a new faster and optimized evan.network user interface. As a result of this, a new optimized dashboard, favorites, contacts, ... application is built. To start using it, the new Dashboard application must be opened.

1. Open the basic evan.network [dashboard application](https://dashboard.test.evan.network/#/dashboard.evan)
2. Click the [add Favorite button](/docs/3000_first_steps/img/dashboard.png) in the top right corner of the screen
3. Add the new <b>evan Dashboard</b> and <b>evan Dashboard - new Design</b> application to your favorites. Using these applications, you can switch between the old and the new UI using the favorites application.<br><br>
  [![new dashboard](/docs/3000_first_steps/img/digitaltwin_new_dashboard.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_new_dashboard.png)
  <br>
4. open the new dashboard
5. click on <b>My Digital Twins</b><br><br>
  [![Digital Twin application](/docs/3000_first_steps/img/digitaltwin_open_app.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_open_app.png)

<b>
  Please note: The new favorites, addressbook, mailbox and profile application is under development. If functionalities are still missing or do not work, please use the previous dark version of the evan.network interface. You can reach this via the favorites in the left side menu.
  <br>
  Thank you very much for your understanding.
</b>

## My Digital Twins
On the home page of Digital Twin Management, you can see your favorite digital twins.

[![Digital Twin overtview](/docs/3000_first_steps/img/digitaltwin_overview.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_overview.png)

In the upper right corner of the application, there is a "Search" and a "Create" button. Within the creation dialog, you can give it a name and a description. Additionally, you can bind an alias, an ENS address, to this Digital Twin. This makes it easier for you to open your Digital Twin later without a contract address.

[![create](/docs/3000_first_steps/img/digitaltwin_create.png){:width="50%"}](/docs/3000_first_steps/img/digitaltwin_create.png)
[![creating](/docs/3000_first_steps/img/digitaltwin_creating.png){:width="50%"}](/docs/3000_first_steps/img/digitaltwin_creating.png)

Using the Search button, you can open already existing Digital Twins.

[![copy contract id](/docs/3000_first_steps/img/digitaltwin_contractid.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_contractid.png)
[![search](/docs/3000_first_steps/img/digitaltwin_search.png){:width="50%"}](/docs/3000_first_steps/img/digitaltwin_search.png)

After your twin was created, you can [add new Plugins](#digital-twin-detail) to your digital twin. If you have not created any Plugins before, call the [Plugin overview](https://dashboard.test.evan.network/#/dashboard.vue.evan/digitaltwins.evan/my-plugins) and create or import existing ones.

## My Plugins
In each Digital Twin different Plugins can be installed for different topics like machine-specific metadata, service log or a calendar. Each Plugin contains information about permissions, data specifications, including their format and validation and user interfaces.  In the <b>My Plugins overview</b>, all your Plugins will be displayed.

[![my Plugins](/docs/3000_first_steps/img/digitaltwin_myplugins.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_myplugins.png)

With the button in the top right corner, you can create new Plugins or import existing ones. After a Plugin was selected, Data Sets can be configured and added. If you want to test with existing templates, simply download one of the following templates and drag them into the dropzone within the Plugin create modal dialog. Each Plugin includes several Data Sets, scoped by categories. So a metadata Plugin can be seperated in multiple Data Sets like "owner", "wheels", ...

- [Forklift Metadata](/docs/3000_first_steps/3400_power_apps/3410_digital_twin_plugins/Forklift Metadata.json)
- [Aerial Work Platform Metadata](/docs/3000_first_steps/3400_power_apps/3410_digital_twin_plugins/Aerial Work Platform Metadata.json)

[![create Plugin](/docs/3000_first_steps/img/digitaltwin_plugin_create.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_plugin_create.png)
[![add Data Set](/docs/3000_first_steps/img/digitaltwin_plugin_create_add_set.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_plugin_create_add_set.png)
[![add Data Set modal](/docs/3000_first_steps/img/digitaltwin_plugin_create_add_set2.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_plugin_create_add_set2.png)

<b>
  Please note: Schema edition is only allowed in Plugins template. Once a Plugin was initialized within a Digital Twin, the data schema cannot be adjusted.
</b>

## Plugin Detail
Using the Plugin detail, new Data Sets can be added and existing ones can be added. Also the Plugin can be renamed, shared, exported or cloned.

[![Plugin detail](/docs/3000_first_steps/img/digitaltwin_myplugins.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_myplugins.png)
[![Data Set detail](/docs/3000_first_steps/img/digitaltwin_plugin_set.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_plugin_set.png)

## Digital Twin Detail
Within the Digital Twin detail, new Plugins can be added or imported. Also the twin can be renamed or mapped to ens addresses. The <b>Add Plugin</b> dialog is build analogous to the <b>New Plugin</b> dialog, but without specifing the data schema. The data schema is loaded from the plugin, so the user must only fill in the data. After all data was entered and the Plugin was instantiated, it is linked into the Digital Twin.

[![create container](/docs/3000_first_steps/img/digitaltwin_container_create.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_container_create.png)

The content of the Plugin Instance looks similar to the original plugin template user interface. The Plugin Instance can be edited, shared with contacts or linked into other Digital Twins.

By sharing a Plugin Instance, a contact can be seletected and each Data Set can be shared seperated by selecting the desired permissions.

[![plugin instance share](/docs/3000_first_steps/img/digitaltwin_container_share.png){:width="30%"}](/docs/3000_first_steps/img/digitaltwin_container_share.png) 

By clicking on a Data Set within a Plugin Instance, the values that are stored within the blockchain will be displayed and can be adjusted, when the user has write permissions.

[![Data Set values](/docs/3000_first_steps/img/digitaltwin_container_set.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_container_set.png)

Clicking on "Schema" in the twins header bar opens the data schema of currently selected field in current container.

[![Data Set schema](/docs/3000_first_steps/img/digitaltwin_container_schema.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_container_schema.png)

Is the Data Set type of list, also new list entries can be added.<br>
[![Data Set list](/docs/3000_first_steps/img/digitaltwin_container_list.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_container_list.png)
