---
Title: "Verification management"
parent: How it works
grand_parent: Services
nav_order: 2240
permalink: /docs/how_it_works/services/verificationmanagement.html
---

# Verification Managment

In evan.network everything, no matter if human, machine or organization has a verified, self-sovereign identity which enables them to interact with each other in a swift and trusted way.

Identities are stored securely on the blockchain, ensuring that each identity is tamper-proof and can’t be impersonated by, for example, providing fraudulent documentation. Decentralized Identities are a critical feature to evan.network, as they constitute a pivotal point for safe business conduct on the platform.

Similar to a fingerprint, an identity serves as a unique identifier.
Their authenticity [can be verified without a doubt](/docs/first_steps/core_apps/verification.html), eliminating the risk of impersonation attacks.

Today we trust that, for example, the e-mail address of a recipient also belongs to the employee of a certain company, but this cannot be verified.

In the evan.network users should be able to ensure that the account with which they conclude a smart contract, for example, also belongs to the respective network partner with whom they want to do business.

This function is provided by the Verification Service. In general, different proofs of identity, so-called verifications, can be assigned to an account.


## Establishing trust relationships

Establishing trust is necessary to collaborate with others.

Trust can be given in two ways: **Explicit** or **Implicit**.

* Explicit trust is established by directly verifying your partner's identity. The relationship is established manually with your contacts through the [AddressBook](/docs/first_steps/core_apps/contacts.html) by exchanging keys.

* Implicit trust is established automatically.
Implicit trust functions in the way that identities, with which you have not established an explicit trust relationship, can be trusted indirectly and automatically.

For example, the TUV is issuing ISO 9001 certificates. If you and another user have both received the ISO certificates from the TUV, certain trust exists between the other user and yourself, even if you didn't explicitly establish trust by means of key exchange first.

This enables a user to see who confirmed the verification and whether it is trustworthy. Different verifications can be deposited and confirmed for each account. For example, ISO certificates, supplier proofs, quality certificates, etc. can be specified.

This feature is crucial in supply chain scenarios, where you might not or must not know all members of an n-tier supply chain.
When you have received a certificate from a trusted third party, like the TUV for example, you can implicitly trust other entities which have received the same certificate.
This allows for participants in a supply chain to collaborate with each other, without having to establish explicit trust with each member in the supply chain.