---
title: "Identity Verification"
parent: Developers
nav_order: 160
permalink: /docs/developers/concepts/identity-verification.html
---

# Identity Verification

Trust in the integrity and identity of a business partner is one of the most important factors in digital communication.

Today we trust that, for example, the e-mail address of a recipient also belongs to the employee of a certain company, but this cannot be verified.

In the evan.network users should be able to ensure that the account with which they conclude a smart contract, for example, also belongs to the respective network partner with whom they want to do business.

This function is provided by the Identity Service. In general, different proofs of identity, so-called claims, can be assigned to an account.

For example, a verification is an entry in the commercial register of a company. Verifications are managed by the owner of the respective account, but are initially unconfirmed and not trustworthy. Therefore, there are trustworthy instances (so-called trusties) that can confirm specific verifications.

This enables a user to see who confirmed the verification and whether it is trustworthy. Different verifications can be deposited and confirmed for each account. For example, ISO certificates, supplier proofs, quality certificates, etc. can be specified.

The Identity Service itself does not store any data and content such as trade licenses or ISO certificates, but only confirms them.
It is also not possible to trace which claims an account has. Proofs are only selectively released by the respective account upon request.
This strengthens the confidence of a business relationship and at the same time safeguards data protection.

