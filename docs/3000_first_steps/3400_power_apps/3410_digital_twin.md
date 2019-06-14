---
title: "Digital Twin"
parent: "First Steps"
nav_order: 3410
grand_parent: "Power Applications"
permalink: /docs/first_steps/power_apps/digital-twin.html
---

# Digital Twin
The Digital Twin management is a generalized application for handling digital representations of real world assets.

- For a detailed overview of <b>what a Digital Twin</b> is and how it works <b>functionally</b>, have a look at:
  - [Functional Overview](/docs/how_it_works/services/digitaltwins.html)
- For a <b>detailed technical deep dive</b> and how to access digital twins as a developer, have a look at:
  - [Digital Twin API](https://api-blockchain-core.readthedocs.io/en/latest/contracts/digital-twin.html)
  - [Data Container API](https://api-blockchain-core.readthedocs.io/en/latest/contracts/container.html)
  - [Usage Examples](https://api-blockchain-core.readthedocs.io/en/latest/contracts/digital-twin-usage-examples.html)

## Start using
The application is based on a new faster and optimized evan.network user interface. As a result of this, a new optimized dashboard, favorites, contacts, ... application is built. To start using it, the new Dashboard application must be opened.

1. Open the basic evan.network [dashboard application](https://dashboard.test.evan.network/#/dashboard.evan)
2. Click the [add Favorite button](http://localhost:4000/docs/first_steps/core_apps/dashboard.html) in the top right corner of the screen
3. Add the new <b>evan Dashbard</b> and <b>evan Dashbard - new Design</b> application to your favorites. Using this applications, you can switch between the old and the new UI using the favorites application.<br><br>
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

[![create](/docs/3000_first_steps/img/digitaltwin_create.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_create.png)
[![creating](/docs/3000_first_steps/img/digitaltwin_creating.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_creating.png)

Using the Search button, you can open already existing Digital Twins.

[![copy contract id](/docs/3000_first_steps/img/digitaltwin_contractid.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_contractid.png)
[![search](/docs/3000_first_steps/img/digitaltwin_search.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_search.png)

After your twin was created, you can [add new plugins](#digital-twin-detail) to your digital twin. If you have not created any plugins before, call the [plugin overview](https://dashboard.test.evan.network/#/dashboard.vue.evan/digitaltwins.evan/my-plugins) and create or import existing ones.

## My Plugins
In each Digital Twin different plugins can be installed for different topics like machine-specific metadata, service log or a calendar. Each plugin contains information about permissions, data specifications, including their format and validation and user interfaces.  In the <b>My Plugins overview</b>, all your plugins will be displayed.

[![my plugins](/docs/3000_first_steps/img/digitaltwin_myplugins.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_myplugins.png)

With the button in the top right corner, you can create new plugins or import existing ones. After a plugin was selected, data sets can be configured and added. If you want to test with existing templates, simply download one of the following templates and drag them into the dropzone within the plugin create modal dialog.

- [Forklift Metadata](/docs/3000_first_steps/3400_power_apps/3410_digital_twin_plugins/Forklift Metadata.json)
- [Aerial Work Platform Metadata](/docs/3000_first_steps/3400_power_apps/3410_digital_twin_plugins/Aerial Work Platform Metadata.json)

[![create plugin](/docs/3000_first_steps/img/digitaltwin_plugin_create.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_plugin_create.png)
[![create plugin](/docs/3000_first_steps/img/digitaltwin_plugin_create_add_set.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_plugin_create_add_set.png)
[![create plugin](/docs/3000_first_steps/img/digitaltwin_plugin_create_add_set2.png){:width="80%"}](/docs/3000_first_steps/img/digitaltwin_plugin_create_add_set2.png)

## Digital Twin Detail

## Plugin instances

## Data sets
