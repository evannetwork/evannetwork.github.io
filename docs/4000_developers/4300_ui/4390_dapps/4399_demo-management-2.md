---
title: "Demo Management 2"
parent: Developers
nav_order: 389
permalink: /docs/developers/ui/dapps/demo-management-2.html
---

# Demo-Management

With the help of the "Demo Management" application different demo applications can be administered and started with users created especially for the use case. After you have logged into the evan.network add the Demo Management DApp to your favorites via the following ENS entry: **demomanagement.evan**.

[![ens-address](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-ens-address.png){:width="50%"}](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-ens-address.png)

[![favorites](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-favorites.png){:width="50%"}](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-favorites.png)

If the DApp is opened now, we will find an empty demo area. Click on "Create Demo" to add a new demo. There you can assign a name to the demo and select the type of demo.

[![empty](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-empty.png){:width="50%"}](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-empty.png)

[![create-demo](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-create-demo.png){:width="50%"}](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-create-demo.png)

After the demo is created, you can view the details of the demo.

[![overview](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-overview.png){:width="50%"}](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-overview.png)


## Rental-Demo

In the upper area of the details, the name and type of the demo is displayed again. To start the demo, two different users (a dispatcher and a supplier) have to be created first. Mnemonics, passwords and names will be generated automatically, but can also be adjusted until your final creation. Use the "Show passwords" checkbox to make Mnemonic passwords visible. Once you have entered your desired user information, verify the captcha query and use the "Create Profile" button.

[![users-create](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-rental-users-create.png){:width="50%"}](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-rental-users-create.png)

After the users have been created, the actual demo case including the corresponding contracts must now be created. Use the "Create contract structure" button to do this.

[![create-contracts](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-rental-create-contracts.png){:width="50%"}](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-rental-create-contracts.png)

As soon as the synchronization is finished, the demo case is created and the contract ID is displayed in the upper area. If a new contract without demo entries is required, a new contract can be created using the "Create new contract" button.

[![finished](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-rental-finished.png){:width="50%"}](/docs/4000_developers/4300_ui/4390_dapps/img/demo-management-rental-finished.png)

In the user area you can, as already described, use the "Show passwords" checkbox to display Mnemonic and password in plain text. Thus you can log in the normal way in another browser session with this user.

Alternatively, you can use the "Start Demo" button, which is displayed under each user, to open a new browser tab in which the demo user is automatically logged in. **Please note that the profile information (Menmonic, Password, AccountId) will be inserted in plain text in the URL. Use this mechanism only for demo users!**
