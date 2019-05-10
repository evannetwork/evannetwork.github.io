---
title: "Create Identity via REST"
parent: Developers
grand_parent: Management Tools
nav_order: 4570
permalink: /docs/developers/management-tools/create-identity
---

# Create Identity via REST

Identities can be created by using the onboarding process as described in [Create an Identity](/docs/first_steps/create-identity.html). This uses the frontend to create a profile and an account for a mnemonic and a password. A part of this process is accepting the terms of use, which is a functional requirement for making transaction on evan.network.

In some cases the profile is not necessary, the profile is usually a requirement for working with encrypted data. If encrypted data is not in the scope of the workflow of an account or if encryption keys can be made available in other ways, this profile can be omitted. Those accounts often also have the requirement, that another account has be a stand-in for accepting the terms of use for that profile-less account.

Accounts, that do not need profiles can be created with a REST endpoint. This endpoint

- creates an identity for the given account (which is a requirement for terms of use handling)
- issues verifications for
  + having accepted any terms of use
  + having accepted current terms of use
  + having a stand-in for accepting the terms of use (and who this is)
- add the given account to the transaction permission contract and allows it to perform transaction on the evan.network

For this the REST endpoint needs the account, that acts as the stand-in and the account, that receives an identity. For security purposes this endpoint also needs a message with a timestamp, that has been signed by the stand-in. This message is the current timestamp in milliseconds and has to be signed by the stand-in account, for example with web3:

```javascript
web3.eth.accounts.sign(`${accountId}|${Date.now()}`, `0x${privateKey}`)
```

This yields a signed message, that has to be added to the request headers. The endpoint needs the following inputs:

- REST parameter:
  + `accountIdParent`: an account that accepts the terms of use for another account, the stand-in
  + `accountIdChild`: an account that gets its identity created
- authorization header:
  + `EvanAuth`: accountId of signing user (is the same accountId as `accountIdParent`)
  + `EvanMessage`: current UNIX timestamp in milliseconds, timestamp may not be older than 5 minutes
  + `EvanSignedMessage`: cryptographically signed `EvanMessage` (signed with private key of the account set in `EvanAuth`)

This request done with curl may look like:

```bash
curl https://agents.test.evan.network/api/smart-agents/faucet/identity/create\?\
accountIdParent\=0xbdD69b1957C1cF89C93d3e009f64682681511B1F\&\
accountIdChild\=0x29f192097B6884c29D6113D9FD93eaeB1C86707C \
-H "Authorization: \
EvanAuth 0xbdD69b1957C1cF89C93d3e009f64682681511B1F,\
EvanMessage 1557394510685,\
EvanSignedMessage 0xd96a963646c04098cf2d2c9aafa6d4fd8b7724f79780050ab3f761e9f4fd25f6561af611baac327286795c0b1427bd48302560e01eeb8d32bbb09e724af05e991c"
```

Be careful not to let too much time pass by between creating the message and submitting it to the server as the message is not allowed to be older than five minutes.