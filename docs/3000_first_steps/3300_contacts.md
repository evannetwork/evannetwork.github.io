---
title: "Contacts"
parent: First Steps
nav_order: 3300
permalink: /docs/first_steps/contacts.html
---

# Contacts
The contacts ÐAPP is your address book, in which you can manage contacts from the blockchain.

[![contacts overview](/docs/3000_first_steps/img/contacts_overview.png){:width="50%"}](/docs/3000_first_steps/img/contacts_overview.png)

Contacts are just other evan.network accounts with a profile, just like yours. But to prevent unsolicited messaging, both contact partners need to exchange keys to be able to send and read each others encrypted messages.

And you have guessed it, this key exchange is a contract on the blockchain again, the protocol of accomplishing it and the storage of the keys. And adding contacts executes and changes those contracts in your profile on the blochain.


## Adding new Contacts
Adding new contacts initiates a key exchange process with the person you want to add, which will, if completed, allow you to exchange blockchain mails or "Bmails" (see [Mailbox](/docs/first_steps/mailbox.html)) with this person.

[![contact add type select](/docs/3000_first_steps/img/contacts_add_type_select.png){:width="50%"}](/docs/3000_first_steps/img/contacts_add_type_select.png)

When you add new contacts, you can choose whether you want to add the contact via account ID or via Email address.

If adding accounts via account ID, a key exchange with this person will be triggered and the invitee will receive a Bmail with your contact request.

If adding accounts via Email, you are required to provide a small amount of onboarding EVEs for the invitee. The invitee will receive an Email with your onboarding invitation and a link to create or import a profile and then verification the provided onboarding EVEs.

Inviting users via Email requires you to have added the onboarding [Smart Agent](/docs/how_it_works/services/smart-agents.html) to your contacts. If you haven't already added the agent to your contacts, a request for this is displayed when clicking on the "Using an Email" button.

[![add smart agent to contacts](/docs/3000_first_steps/img/contacts_add_smart_agent.png){:width="50%"}](/docs/3000_first_steps/img/contacts_add_smart_agent.png)

Confirming this request will perform a key exchange with the Smart Agent to enable you to send encrypted messages with the Smart Agent, which is required to invite new users via Email.


## Managing Contacts
You can rename or delete contacts from your address book by clicking on them.

[![contact details](/docs/3000_first_steps/img/contacts_detail.png){:width="50%"}](/docs/3000_first_steps/img/contacts_detail.png)

The second tab, "contact status" allows you to review your contact request status, which allows you to check if an invitee already has replied to your contact request.

Please note that deleting accounts also removes keys exchanged with them. Without these keys, you won't be able to read contracts created by them and Bmails sent by them.
