---
title: "Create Identity via REST"
parent: Developers
grand_parent: Management Tools
nav_order: 4570
permalink: /docs/developers/management-tools/create-identity
---

# Create Identity via REST

Identities can be created by using the onboarding process as described in [Create an Identity](/docs/first_steps/create-identity.html). This uses the frontend to create a profile and an account for a mnemonic and a password. A part of this process is accepting the terms of use, which is a functional requirement for making transaction on evan.network.

In some cases the profile is not necessary, the profile is usually a requirement for working with encrypted data. If encrypted data is not in the scope of the workflow of an account or if encryption keys can be made available in other ways, this profile can be omitted. Those accounts often also have the requirement, that another account has be a representative for accepting the terms of use for that profile-less account.

Accounts, that do not need profiles can be created with a REST endpoint. This endpoint

- creates an identity for the given account (which is a requirement for terms of use handling)
- issues verifications for
  + having accepted any terms of use
  + having accepted current terms of use
  + having a representative for accepting the terms of use (and who this is)
- add the given account to the transaction permission contract and allows it to perform transaction on the evan.network

For this the REST endpoint needs the account, that acts as the representative and the account, that receives an identity. For security purposes this endpoint also needs a message with a timestamp, that has been signed by the representative. This message is the current timestamp in milliseconds and has to be signed by the representative account, for example with web3:

```javascript
web3.eth.accounts.sign(`${Date.now()}`, `0x${privateKey}`)
```

This yields a signed message, that has to be added to the request headers. The endpoint needs the following inputs:

- REST parameter:
  + `accountIdParent`: an account that accepts the terms of use for another account, the representative
  + `accountIdChild`: an account that gets its identity created
- authorization header:
  + `EvanAuth`: accountId of signing user (is the same accountId as `accountIdParent`)
  + `EvanMessage`: current UNIX timestamp in milliseconds, timestamp may not be older than 5 minutes
  + `EvanSignedMessage`: cryptographically signed `EvanMessage` (signed with private key of the account set in `EvanAuth`)

This request done with curl may look like:

```bash
curl https://agents.test.evan.network/api/smart-agents/faucet/identity/create\?\
accountIdParent\=0xA1cFB71f0207B0da24bB00dF306D06EF721dB482\&\
accountIdChild\=0xbdd69b1957c1cf89c93d3e009f64682681511baf \
-H "Authorization: \
EvanAuth 0xA1cFB71f0207B0da24bB00dF306D06EF721dB482,\
EvanMessage 1557479808692,\
EvanSignedMessage 0x8e5289cbf79f7c1ea9b871d0180d512ec1e317b3194604d15e009fb71b97e64e2be2e9f7eef4f4f7ea0382cf696690896704e8046781d8bda441f5a91baa96781c"
```

Be careful not to let too much time pass by between creating the message and submitting it to the server as the message is not allowed to be older than five minutes.

## Troubleshooting

The rest service can return the following error messagen when receiving requests:

-------

```
"error": "No verified Account.",
```
This error means, that the signed message you provided does not match the defined account in the "EvanAuth" section in the authorization parameter.

You can verify the signed message with web3 the following way:

```javascript
const now = Date.now()
const signedMessage = web3.eth.accounts.sign(`${accountId}|${now}`, `0x${privateKey}`)
const accountId = web3.eth.accounts.recover(
  `${accountId}|${now}`,
  signedMessage.signature
)
```

the `accountId` variable must match the defined accountId in the "EvanAuth" section. **The Accountid must be written in checksum case**

-------

```
"error": "no authorization headers provided",
```

The sent request has no attached `Authorization` header. Please add a `Authorization` header with the markup above.


-------

```
"error": "signed message has expired",
```

The signed timestamp has expired. When you sign a timestamp it is valid for 5 minutes. Otherwise the REST endpoint will return this message and you have to provide a new signed timestamp.