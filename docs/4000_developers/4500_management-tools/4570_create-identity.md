---
title: "Create Identity"
parent: Developers
grand_parent: Management Tools
nav_order: 4570
permalink: /docs/developers/management-tools/create-identity
---

# Create Identity

Identities can be created by using the onboarding process as described in [Create an Identity](/docs/first_steps/create-identity.html). This uses the frontend to create a profile and an account for a mnemonic and a password. A part of this process is accepting the terms of use, which is a functional requirement for making transaction on evan.network.

In some cases the profile is not required, which are usually a requirement for working with encrypted data. If encrypted data is not in the scope of the workflow of an account or if encryption keys can be made available in other ways, this profile can be omitted. Those accounts often also have the requirement, that another account has be a stand-in for accepting the terms of use for that profile-less account.

Accounts, that do not need profiles can be created with a REST endpoint. This endpoint

- creates an identity for the given account (which is a requirement for terms of use handling)
- issues identities for
  + having accepted any terms of use
  + having accepted current terms of use
  + having a stand-in for accepting the terms of use (and who this is)

For this the REST endpoints needs the account, that acts as the stand-in and the account, that receives an identity. For security purposes this endpoint needs a message with a timestamp, that has been signed by the stand-in. This message looks like:

```javascript
`${accountId}|${Date.now()}`
```

and can be signed with web3 for example like:

```javascript
web3.eth.accounts.sign(`${accountId}|${Date.now()}`, `0x${privateKey}`)
```

This yields a signed message, that has to be added to the request headers. A request submitted with curl may look like:

```bash
curl https://agents.test.evan.network/api/smart-agents/faucet/identity/create\?\
accountIdParent\=0xbdD69b1957C1cF89C93d3e009f64682681511B1F\&\
accountIdChild\=0xbdd69b1957c1cf89c93d3e009f64682681511b7f \
-H "Authorization: \
EvanMessage 0xbdD69b1957C1cF89C93d3e009f64682681511B1F|1557394510685,\
EvanSignedMessage 0xd96a963646c04098cf2d2c9aafa6d4fd8b7724f79780050ab3f761e9f4fd25f6561af611baac327286795c0b1427bd48302560e01eeb8d32bbb09e724af05e991c,\
EvanAuth 0x0Ca678B118f5d6F14CfaBD99E5D3949EdD4c486b"
```