---
title: "Architecture"
---
# Architecture

Real goods and machines receive a digital identity (Digital Twin) in the evan.network blockchain and can thus participate directly in digital transactions. In a business center, users can execute transactions and exchange data with each other, with other organizations or with the digital twins of real machines. The evan.network thus provides the basis for company-wide, efficient and secure Industry 4.0 business models.

For the interaction between users, processes and machines evan.network offers predefined services (Smart Contracts) which can be adapted to specific needs. The interaction with Smart Contracts takes place via ÐApps in web or mobile browser or via API from existing IT systems, IT tools and/or machines. For this purpose Smart Agents communicate with the Smart Contracts. The Smart Contracts represent the professional framework of the respective service and are developed according to the specific needs. For example, a Smart Contract that represents a digital twin can include the entire life cycle of the asset and its business processes. In concrete terms, this means that the smart contract itself provides a kind of management shell for the various data types and manages access to the data via an encryption management and a rights and role model. In the case of master data such as product properties, the actual data is stored as a JSON object encrypted with the DigitalTwin keys in the storage service. The address where the data was stored in the storage is stored in the Smart Contract. Other data is handled in a similar way, e.g. service reports. If the service technician creates a report and wants to attach an image of the machine, for example, this image is loaded into the storage in encrypted form and the corresponding address is inserted into the corresponding data area of the Digital Twin. The complete control of who may insert or read data is controlled by the owner of the Digital Twin Smart Contract, who thus has complete data sovereignty.

<img a style="float: left; margin-right: 1em; " alt="Business Architecture" title="Business Architecture" width="50%" height="100%" src="/public/business_view.svg"/>

## Business Center
In business centers, organizations, users and machines are networked with each other in order to interact as partners in a concrete business environment. Network partners who join a business center expand their profile with specific information and features for this business environment. In addition to extended descriptive information, the profile may also contain certificates, competencies and general skills.
The Business Center is an Ethereum-based development framework and provides specific Smart Contracts for initiating, entering into and implementing business relationships. All cooperation between network partners via Smart Contracts within a Business Center takes place directly, i.e. without a central intermediary, and is encrypted, i.e. secure against access by unauthorized third parties.

Depending on the requirements for business relationships, business centers are either public, closed, or restricted. 


**Public Business Centers** are publicly available and can be found by all users. Any user can join a Public Business Center. 

**Private Business Centers**, on the other hand, are hidden. Only on explicit invitation of a Business Center Administrator, users can join. 

**Restricted Business Centers** are publicly listed. Users can submit a request to participate, but this must be approved by an administrator of the Business Center.

Users of evan.network are not obliged to use the business center structure of evan.network. You can create and run your own Ethereum-based SmartContract developments on evan.network, but using the business center structure makes it much easier.

To map different business relationships, evan.network offers different Smart Contract Templates, which are enriched in a business center with the specific logic required there. Creating concrete Smart Contracts for a business relationship and initializing them with the digital identities of the users involved is a complex process. 
This is greatly simplified by the use of a Smart-Contract-Factory. The factory manages all business center-specific Smart-Contract templates, creates a configured instance of the Smart Contract and initializes this with the network partners authorized to the contract. From this point on, a direct business relationship is established between the network partners involved, which is only visible and executable for them.


Smart Contracts were developed with the goal of easy use and expansion. Each Smart Contract can be called directly from a Web3 browser using a name server entry, for example. Initially, only the manifest file ([DBCP](/dev/dbcp)) is referenced and loaded. This file contains a standardized structure with descriptive information to make the service human and machine readable. It also contains references to the actual Smart Contract in the blockchain and the Distributed App (ÐApp), which enables direct user interaction with the service. 
In order to ensure interoperability of services, the manifest file corresponds to a standardized structure that is currently provided as an open source component (DBCP) as part of a project sponsored by the Thuringian Ministry of Economics, Science and Digital Society. This makes it possible to start an interaction with the services even without the evan.network framework.

This architecture enables the integration of any third-party Smart Contracts into an evan.network environment. Referenced via the manifest file existing Smart Contracts of other providers can be combined with evan.network-ÐApps and thus integrated into a homogeneous user experience. 
Based on this architectural principle, the entire network was created. Thus, all applications the user communicates with in the evan.network, processes Smart Contracts and makes transactions, are implemented as ÐApp. 

## Security
The core technology of the evan.network is based on the Ethereum blockchain technology.  The protection of transactions against manipulation is an essential element of this technology. This requires that the contents of the Smart Contracts can be read, interpreted and verified by all network partners (e.g. MasterNodes) in the block chain, which represents a significant hurdle in the B2B adaptation of block chain technology.

The evan.network therefore implements a hybrid storage concept that offers transaction and data security at the same time. All user data is encrypted (AES 256bit/CBC), stored in a distributed file system (IPFS) belonging to the network and referenced from the smart contract. This ensures that the actual content is only visible and usable for third parties if they are invited into a contract and thus have an authorization for the respective data.


Each user receives a public and a private key for this at his first registration. These keys are used to establish communication (Diffie Hellman) with other users and Smart Contracts. 

For the interaction within a specific business relationship, additional key pairs (public / private) are created, which only apply to the specific business relationship and the Smart Contract used there. This means that Smart Contracts and the contract contents can be assigned access rights very flexibly. This makes it possible, for example, to determine which parts of a Smart Contract a network partner may read or edit.

In addition, references and keys for data stored outside the blockchain can be stored within the Smart Contract. For example, cloud storage or IoT data streams can be referenced and accesses to them securely managed. 

## Smart Contracts

evan.network supports Smart Contracts that are compatible with Ethereum technology (EVM). For the simple creation of specific business relationships, evan.network offers various basic smart contracts that make it easier for developers to implement business applications. These smart contracts offer functionalities such as rights and role management at business logic and data level, upgradeability, versioning and data encryption.
Business center or application-specific characteristics can be derived from these basis Smart Contracts, for example:

- **Capa Contract** - Easy management of requests for available capacities for a specific requirement within the Business Center. Capacity requests are sent to users known by name or all users who meet certain profile criteria and can be answered automatically or via Capa-ÐApp. One or more relevant offers can be selected from the answers and an order in the form of a business contract can be concluded with the corresponding network partners. 
Inquiries for services or rental can also be defined and answered via capa-contracts.

- **Business Contract** - A business contract defines a specific business transaction between two or more network partners and is comparable to a classic contract or order. It does not matter whether the business contract is closed directly or as a result of a previous capa contract request. Business contracts can describe one-off and recurring orders. In addition to the contract conditions, a business contract can also contain almost any user data required for contract performance (access data, CAD data, etc.) or arising during contract performance (e.g. log data, production progress, performance reports, etc.).

- **Digital Twin Contract** - The Digital Twin Contract represents a real good in the blockchain, gives it an identity and enables it to securely exchange transactions and data with other users or goods. In a Digital Twin, real goods (e.g. machines, components etc.) but also concrete orders (e.g. logistics) can be provided with a digital identity. Via the Digital Twin Contract, data can be securely stored and, if required, specifically released to third parties. The Digital Twin can enter into contractual relationships with other users as well as with other Digital Twins, for example to allocate capacities of service technicians (Capa Contract). These are then ordered via the business contract. The Digital Twin stores and manages information about the real goods it represents, permanently and tamper-proof.

To ensure updateability and to solve the backward compatibility of derived Smart Contracts, each derived Smart Contract receives a fixed assignment to a ÐApp and a technical description of its structure (DBCP). This ensures that a smart contract can always be operated by network partners, even if technologies change or new versions of the smart contract are created.

## Account Management

To interact in evan.network, users, organizations or machines need an account. The account for real users is created during onboarding during the first login. A user profile is created with his public and private key, as well as an address book and a mailbox. The relationships of a user with other users are stored in the address book by storing the public keys of the accounts of the respective network partners required to decrypt the communication. In the mailbox of an account, notifications of invitations to this account are stored in contracts of other accounts. 

Real users can be grouped into organizations to appear under their identity. This is used to map the relationship of users in a real organization. This allows contracts to be concluded between organizations, which then have to be served or signed by one or more real users. 

Within a Business Center, the information in the profiles of the user and organization accounts is extended by subject-specific data. This makes it easy to find users and organizations within the Business Center and to initiate business. This specific profile information can be entered directly when a user or organization is admitted to the Business Center or collected automatically while working in the Business Center. An example of an automated date is the calculated delivery on time (key figure: delivery reliability) based on the completed business relationships.


## Interaction with Smart Contracts and Business Centers

The interaction capabilities in a business center should enable simple interaction between end users, IT systems and machines. Starting from today's, mostly manual forms of communication, an automation of cross-company cooperation can be implemented step by step.

To interact as user or machine in evan.network, a network account is required. An account can be created directly via onboarding (self-service) or via an invitation. An invitation is sent by an existing user or SmartContract on the network. In the invitation, you can control whether a user is invited directly to a business center or to a specific SmartContract. In addition, EVEs can be sent directly to the invited user as part of the invitation process, so that the new user is immediately ready to work in the network. The invitation is sent either as a technical invitation via an API or by a user using an e-mail address. The invitation email contains an invitation text and a link to the Onboarding ÐApp. This ÐApp guides the new user through the registration process where he has to confirm e.g. terms and conditions and data protection and gets an own account with PrivateKey and Mnemonic. After successful registration the user has an evan.network identity with which he can now participate in the Business Center and Smart Contract.

All interaction with business centers and smart contracts takes place via ÐApp's. Users interact with the respective ÐApp via web or mobile browsers. ÐApps are HTML applications loaded from the blockchain and make it so easy for the user to work with Smart Contracts and evan.network interactively. 

To communicate with Smart Contracts from your own applications and ÐApps, evan.network provides APIs in form of a JavaScript library and developer documentation. Thus own applications can be implemented and operated on evan.network.

For an automation of the business relations evan.network offers APIs to all Smart Contracts. Thus the evan.network can be connected to own systems and a direct integration of business processes can be carried out. Furthermore, it is possible to add logic and workflow addons in the evan.network with the help of [smart agents](/dev/smart-agents). They are operated by the respective smart agent provider and can enable workflow-supported communication of the evan.network with existing IT systems and machines. Smart Agents can be invited into a Smart Contract, just like users, and thus receive access to its contents. The Smart Agent constantly checks the contract for changes and can automatically initiate new processes according to predefined rules as soon as it finds one.  
If the user has the rights, he or she can also add content to the Smart Contract again. Via Smart Agents the invitation via email or the mobile push notifications are solved in the evan.network. They combine the "blockchain world" with other technologies.

## Scalability
A big challenge to blockchain technology is the number of possible parallel transactions. Thus, there is still no final solution for realistically achieving almost infinite scalability within a blockchain. To counter this fact the evan.network is structured in such a way that the organization and technology of the MasterNodes make it possible to launch specialized or UseCase specific SideChains at any time. These are also subject to DAO governance but, depending on your setup, configuration and rules, allow you to perform specified use cases in much higher numbers. The technologies and services used in evan.network such as the name service or DBCP descriptions make it easier for users and developers to interact seamlessly with their contracts and ÐApp's regardless of this technical separation.
