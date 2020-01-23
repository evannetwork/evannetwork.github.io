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
This allows participants in a supply chain to collaborate with each other, without having to establish explicit trust with each member in the supply chain.


## Verify the trust chain

To be safe that the issued verifications are completely valid, the root verification called `/evan` is issued by an account which is anchored in the chain spec of evan.network.


This means, if you want to verify the whole chain for a given verification you take the current verification path and check every section of the path if the account that received the portion has a proper verification from another account.


For example we take a verification with the path `/evan/company/12345/employee`.

![ENO verification](/docs/2000_how_it_works/img/eno_verification.png)

The verification with the path `/evan/company/12345/employee` was given to the identity `0xc2300E1bAC9d3f164F65c9c29f11f8F34Bf83Db4` and the API now tries to verify the validity of the verfication with the trust chain.

To verify this we must get the issued identity which has issued the `/evan/company/12345/employee` verification for the target identity. This information is provided by the API response from the `runtime.verifications.getVerifications`function. The result of this function returns that the issuer of the verification has the identity `0x4628Cd53af50192784Fb81470688575d4DD0BB82`

With this information we can check if the identity `0x4628Cd53af50192784Fb81470688575d4DD0BB82` now has a valid verification with the path `/evan/company/12345` given from another identity. We use the same function as above and get back another identity and doing the same until we arrive at the path `/evan`.

In this example, verifications with the path `/evan/company/12345` can only be issued by ENO verified notaries. The company verification is issued to companies which are verified by a [service based on evan.network](/docs/first_steps/power_apps/notary-verification.html).

When we arrive at the `/evan` verification we now have the root verification on evan.network. To have a root trust anchor that issues the `/evan` verification, the ENO created identities (which issue verifications) on the testcore and the core network. Those are owned by accounts defined in the chain specification of the respective networks. The chain specification defines the genesis block for the blockchain network and can not be edited after the network has been started. The specifications are publicly visible in the evan.network github space and the whole network relies on this.

-------

The following table visualizes the identities which can issue the `/evan` verifications and which account is the owner of these identities.

| Network | Verification Identity | Verification Account |
| :-: | :-: | :-: |
| evan.network testcore  | 0x8C073227ba523Ad2546c29F43071Ea3584C66D85 | 0x00a71373dA6e26F134B87faD634AbBB154C8778d |
| evan.network core       |  TBD | TBD |
{: .evan-flex-table }

