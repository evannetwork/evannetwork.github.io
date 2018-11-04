
# Welcome to evan.network
Evan.network is an enterprise-ready, Ethereum based, open ecosystem. 
Designed to trustfully enable decentralized business applications and solutions in the 4.0 industry, absolute governance of your data and files is at the helm of priorities. 

In realization of this vision, Evan.network comes with features catered to meet every blockchain business need. 
With effectiveness and data sovereignty in mind, the platform consists of masternodes hosted by trusted European enterprises and businesses. 
High transaction throughput coupled with stable transaction fees model the network into a cost-effective and decisively more secure alternative to conventional solutions. 

Key functionalities, amongst others, are:

* DApps (decentralized applications) 
* Digital Twins as virtual counterparts of real-life assets, organizations, and people 
* encrypted on chain messaging service
* an identity solution (Decentralized Identities) for accounts
* Flexible yet secure delegation of smart contract permissions, including trans organizational 

Integrating the network's capabilities into your productive environment allows you to seamlessly tap into advantages that Web 3.0 distributed applications (DApps) and Decentralized Identities bring with them, as applications and services on the evan chain are reachable via API calls and through a user interface.

Evan adheres to the concept of a Decentralized Autonomous Organization, or DAO. Unique to the DAO is the characteristic of no central point of authority in any shape or form. Naturally, this includes Evan as a company as well.
Thus transparent and democratic network governance lies at the heart of Evan.network. 

We follow a philosophy of open source and have made our codebase publicly available. The neutrality aspect of the system is safeguarded by an openly available authority consensus our masternodes use to defend against potential hostile network takeovers.

<p><a style="float: right" alt="Gitter" title="Gitter" href="https://gitter.im/evannetwork/Lobby"><img src="/public/chat.svg"/></a></p>



Core features at a glance
----

#### [Decentralized Identities](https://evannetwork.github.io/doc/Identity)

In evan.network everything, no matter if human, machine or organization has a decentralized, self-sovereign identity which enables them to securely and instantaneously interact with each other.

#### [Smart Contract Access Delegation (SCAD)](https://evannetwork.github.io/dev/security)

Smart Contract Access Delegation (SCAD) enables evan.network users to define permissions for smart contracts at a granular level, including complex trans organizational rights and permission management. 

#### [Packaged DApps](https://evannetwork.github.io/dapps/basics)

Packaged Distributed Applications (DApps) on the evan.network are designed to ease the development process on the blockchain by automically taking care of all necessary backend components.

#### [Customized Namespaces](https://evannetwork.github.io/doc/namespaces)

Evan.network uses a nameservice to provide namespaces for DApps and identities, adding unique names as identifiers for applications or identities. 

#### [Secure IoT connectivity](https://evannetwork.github.io/doc/iotsecurity)

In order to adequately cover all security aspects without the need for any extra service implementation, the secure IoT connectivity feature of evan.network offers a functioning IoT security suite for enterprises. 

#### [Contract Templates](https://evannetwork.github.io/dev/deployment)

Contract templates are a great way to bootstrap smart contract development and adapt contracts to specific business needs.


Getting started on evan.network
----

<dl>
<dt><a href="/tutorial/quick-start">Quick Start</a><dt>
<dd>Beginning your journey with evan is easy.<br />
Creating a profile that you register through our decentralized web service is all it takes.
</dd>
<dt><a href="/doc/goals">General Overview</a></dt>
<dd>A deeper look into the concepts of the <a href="/doc/network">network</a> and the <a href="/doc/dao">DAO</a>.</dd>
<dt><a href="/dev/overview">Technical Details</a></dt>
<dd>If you wanna know how it works and fits together.</dd>
<dt><a href="/dev/getting-started">Start Programming</a></dt>
<dd>Set up the environment and start building right way, we have handy tutorials ready to help you become familiar with the platform.</dd>
<dt><a href="/doc/faq">FAQ</a></dt>
<dd> </dd>
<dt><a href="/doc/glossary">Glossary</a></dt>
<dd> </dd>

<p>If you want to join <code>evan.network</code> as an integral part of the infrastructure and shape its future, contact us on our <a href="https:///evan.network">WebSite</a>.

<br>

<h2><a href="doc/architecture">Architecture</a></h2>

<svg id="evan.network" version="1.1" width="100%" viewBox="0 0 600 900" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <marker id="start-data" style="stroke: #003946; fill: #003946;" viewBox="0 0 10 10" refX="10" refY="5" markerUnits="strokeWidth" markerWidth="4" markerHeight="3" orient="auto">
      <path d="M 0 5 L 10 10 L 10 0 z"/>
    </marker>
    <marker id="end-data" style="stroke: #003946; fill: #003946;" viewBox="0 0 10 10" refX="0" refY="5" markerUnits="strokeWidth" markerWidth="4" markerHeight="3" orient="auto">
      <path d="M 0 0 L 10 5 L 0 10 z"/>
    </marker>
    <marker id="start-lookup" style="stroke: #63ceca; fill: #63ceca;" viewBox="0 0 10 10" refX="10" refY="5" markerUnits="strokeWidth" markerWidth="4" markerHeight="3" orient="auto">
      <path d="M 0 5 L 10 10 L 10 0 z"/>
    </marker>
    <marker id="end-lookup" style="stroke: #63ceca; fill: #63ceca;" viewBox="0 0 10 10" refX="0" refY="5" markerUnits="strokeWidth" markerWidth="4" markerHeight="3" orient="auto">
      <path d="M 0 0 L 10 5 L 0 10 z"/>
    </marker>
    <path id="protocol" style="stroke: #f7aacf; fill: #feeaf3;"
          d="M 0 0 l 20 5 h -5 v 10 h 5 l -20 5 l -20 -5 h 5 v -10 h -5 l 20 -5"  />
    <path id="triangle" style="stroke: f7aacf; fill: #f7aacf;" d="M 0 0 h 200 l -100 10 l -100 -10"  />
    <g id="master-node">
      <rect class="bw dotted" x="0" width="68" height="22" />
      <text class="small thin" x="7" y="14">MasterNode</text>
    </g>
  </defs>
  <style type="text/css">
    text        { font: 10pt "PT Sans", Helvetica, Arial, sans-serif; stroke: #003946; fill: #003946; }
    text.big    { font-size: 12pt; font-weight: bold; stroke-width: 0; }
    text.small  { font-size: 8pt; }
    text.bold   { font-weight: bold; }
    text.white  { stroke: #fff; stroke-width: 1; fill: #fff; }
    text.prot   { stroke: #f7aacf; fill: #f7aacf;}
    text.code   { font: 9pt monospace; stroke: #003946; stroke-width: 0.5; fill: #003946; }
    a           { cursor: pointer; }
    
    .grey       { stroke: #023845; stroke-width: 1; fill: #023845; fill-opacity: 0.5; opacity: 0.5; }
    .black      { stroke: #003946; stroke-width: 3; fill: #003946; fill-opacity: 1; }
    .thin       { stroke: #2a4d57; stroke-width: 0.5; fill: #2a4d572; fill-opacity: 1; }
    .pink       { stroke: #d9028d;  stroke-width: #d9028d; fill: #d9028d; }
    .bw         { stroke: #003946; fill-opacity: 1; fill: #fff; }
    .region     { stroke: #aaa; stroke-dasharray: 2 1; fill-opacity: 0; }

    .dotted     { stroke-dasharray: 1 1; }
    .data-flow  { stroke: #003946; stroke-width: 3; fill-opacity: 0; marker-end: url(#end-data); }
    .bidirectional-data
    {
      stroke: #003946; stroke-width: 3; fill-opacity: 0;
      marker-start: url(#start-data); marker-end: url(#end-data);
    }
    .lookup     { stroke: #63ceca; stroke-width: 3; fill-opacity: 0; marker-end: url(#end-lookup); }
    .bidirectional-lookup
    {
      stroke: #63ceca; stroke-width: 3; fill-opacity: 0;
      marker-start: url(#start-lookup); marker-end: url(#end-lookup);
    }
    .library    { fill: #2a4d57; stroke: #63ceca; }
    .module     { fill: #8a9ea4; stroke: #63ceca; }
    .server     { fill: #a6dddc; stroke: #003946; stroke-width: 2; }
    .service    { fill: #f7aacf; stroke: #003946; stroke-width: 2; }
    .bubble     { fill: #f7aacf; stroke: #a6dddc; stroke-width: 1; }
    .contract   { fill: #e0e6e7; stroke: #8a9ea4; stroke-width: 1; }
    
  </style>

  <g transform="translate(-20, -40)">
    <g id="edge-server" transform="translate(20, 50)">
      <title>Smart Agents</title>
      <a xlink:href="/dev/smart-agents">
        <rect class="bw dotted" x="30" width="160" height="140" />
        <text x="70" y="15">Edge Server</text>
        <g transform="translate(0,10)">
          <text class="small grey" x="42" y="24">Smart Agents</text>
          <rect class="module" x="40" y="30" width="130" height="60" />
          <rect class="module" x="45" y="45" width="130" height="60" />
          <rect class="module" x="50" y="60" width="130" height="60" />
          <text class="small" x="45" y="41">Notification</text>
          <text class="small" x="50" y="56">Faucet</text>
          <text class="small" x="55" y="71">Onboarding</text>
          
          <text class="small thin" x="75" y="89">Terms of Use</text>
          <text class="small thin" x="75" y="99">Profile Creation</text>
          <text class="small thin" x="75" y="109">Invitations</text>
        </g>
      </a>
    </g>
    <g id="core-dapps" transform="translate(200, 50)">
      <title>ÐApps</title>
      <a xlink:href="/dapps/introduction">
        <rect class="bw dotted" x="30" width="160" height="140" />
        <text x="70" y="15">Core ÐApps</text>
        <g transform="translate(0,10)">
          <text class="small grey" x="42" y="24">...</text>
          <rect class="module" x="40" y="30" width="130" height="60" />
          <rect class="module" x="45" y="45" width="130" height="60" />
          <rect class="module" x="50" y="60" width="130" height="60" />
          <text class="small" x="45" y="41">Tasks</text>
          <text class="small" x="50" y="56">Onboarding</text>
          <text class="small" x="55" y="71">Dashboard</text>
          <text class="small thin" x="75" y="89">Login</text>
          <text class="small thin" x="75" y="99">Session</text>
          <text class="small thin" x="75" y="109">Container</text>

        </g>

      </a>
    </g>

    <g id="applications" transform="translate(380, 50)">
      <title>Get Started with Programming</title>
      <a xlink:href="/dev/getting-started">
        <rect class="bw dotted" x="30" width="160" height="140" />
        <text x="70" y="15">Applications</text>
        <g transform="translate(70,45)">
          <ellipse class="bubble" rx="35" ry="15" />
          <text class="small" x="-21" y="0.25em">WebApps</text>
        </g>
        
        <g transform="translate(140,65)">
          <ellipse class="bubble" rx="45" ry="15" />
          <text class="small" x="-27" y="0.25em">Native Apps</text>
        </g>
        
        <g transform="translate(90,105)">
          <ellipse class="bubble" rx="45" ry="15" />
          <text class="small" x="-28" y="0.25em">Mobile Apps</text>
        </g>
      </a>
    </g>
  </g>
  <g id="core-api" transform="translate(10, 180)">
    <path class="dotted grey" d="M 0 0 h 580" />
    <text class="big grey" transform="rotate(90)" x="20">Core API</text>
    <use xlink:href="#triangle" x="180" y="-15" />
    
    <a xlink:href="/dev/security#key-exchange" transform="translate(20,20)">
      <rect class="library" width="160" height="80" rx="2"/>
      <text class="white" x="40" y="42">Key Exchange</text>
      <title>Establishes Account Communication Channels</title>
    </a>

    <a xlink:href="/dev/blockchain-core" transform="translate(200,20)">
      <rect class="library" width="160" height="80" rx="2"/>
      <text class="white" x="32" y="42">Blockchain Core</text>
      <title>ECMAScript Library to work with Ethereum Contracts and IPFS</title>
    </a>

    <a xlink:href="/dev/dbcp" transform="translate(380,20)">
      <rect class="library" width="160" height="80" rx="2"/>
      <text class="white" x="64" y="42">DBCP</text>
      <title>A Description Language for Decentralized Business Applications</title>
    </a>

  </g>
  
  <g id="core-services" transform="translate(10, 310)">
    <path class="dotted grey" d="M 0 0 h 580" />
    <text class="big grey" transform="rotate(90)" x="20">Core Services</text>
    <use xlink:href="#triangle" x="180" y="-15" />
    
    <g transform="translate(0,20)">
      <g transform="translate(70,0)">
        <a xlink:href="https://github.com/evannetwork/smart-contracts-admin">
          <text class="small grey" transform="rotate(90)" x="20" y="-36">admin</text>
          <title>Private Repository</title>
        </a>
        <a xlink:href="https://github.com/evannetwork/smart-contracts-core">
          <text  class="small grey" transform="rotate(90)" x="150" y="-36">core</text>
          <title>Public Repository</title>
        </a>

        <text class="small grey" x="50" y="12">user management</text>
        <a xlink:href="/dev/smart-contracts#rights-and-roles" transform="translate(50,20)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="2" y="12">RightsAndRoles</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#mailbox" transform="translate(60,36)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="2" y="12">Mailbox</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#profile" transform="translate(70,52)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="2" y="12">Profile</text>
          <text class="small grey" x="24" y="30">Roles</text>
          <text class="small grey" x="24" y="46">Crypt Keys</text>
          <title>Ethereum Contract</title>
        </a>

        <text class="small grey" x="220" y="12">factories</text>
        <a xlink:href="/dev/smart-contracts#contract-factories" transform="translate(220,20)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="2" y="12">ProfileFactory</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#contract-factories" transform="translate(230,36)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="2" y="12">DigitalTwinFactory</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#contract-factories" transform="translate(240,52)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="2" y="12">TaskFactory</text>
          <text class="small grey" x="24" y="30">DataContracts</text>
          <text class="small grey" x="24" y="46">from template</text>
          <title>Ethereum Contract</title>
        </a>

        <text class="small grey" x="220" y="142">templates</text>
        <a xlink:href="/dev/smart-contracts#service-contract" transform="translate(220,150)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="4" y="12">ServiceContract</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#business-center" transform="translate(230,166)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="2" y="12">BusinessCenter</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#data-contract" transform="translate(240,182)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="2" y="12">DataContract</text>
          <text class="small grey" x="24" y="30">Entries</text>
          <text class="small grey" x="24" y="46">Access Rights</text>
          <title>Ethereum Contract</title>
        </a>

        <text class="small grey" x="50" y="142">infrastructure</text>
        <a xlink:href="/dev/smart-contracts#ens" transform="translate(50,150)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="2" y="12">ENS</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#event-hub" transform="translate(60,166)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="2" y="12">EventHub</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#base-contract" transform="translate(70,182)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="2" y="12">BaseContract</text>
          <text class="small grey" x="24" y="30">DBCP Reference</text>
          <text class="small grey" x="24" y="46">Sharing</text>
          <title>Ethereum Contract</title>
        </a>
      </g>
    </g>
  </g>

  <g id="core-network" transform="translate(10, 600)">
    <path class="dotted grey" d="M 0 0 h 580" />
    <text class="big grey" transform="rotate(90)" x="20">Core Network</text>
    <use xlink:href="#triangle" x="180" y="-15" />
    
    <g transform="translate(40, 0)">
    
      <path class="pink" d="M 34,40 L -2,151" />
      <path class="pink" d="M 34,40 L 242,90" />
      <path class="pink" d="M 242,90 L 86,211" />
      <path class="pink" d="M -2,151 L 86,211" />
      <path class="pink" d="M -2,151 L 242,90" />
      <path class="pink" d="M 34,40 L 86,211"/>
      <path class="pink" d="M -2,151 L 242,90" />"
      <path class="pink" d="M 186,201 L 86,211"/>
      <path class="pink" d="M 186,201 L 242,90"/>
      <path class="pink" d="M 186,201 L 206,241"/>
      <path class="pink" d="M 186,201 L 308,211"/>
      <path class="pink" d="M 206,241 L 308,211"/>
      <path class="pink" d="M 308,211 L 242,90"/>
      <path class="pink" d="M 308,211 L 434,185"/>
      <path class="pink" d="M 308,211 L 414,233"/>
      <path class="pink" d="M 434,185 L 414,233"/>
      <path class="pink" d="M 434,185 L 486,85"/>
      <path class="pink" d="M 242,90 L 486,85"/>
      <path class="pink" d="M 308,211 L 486,85"/>
    
      <use x="0" y="29" xlink:href="#master-node" />
      <use x="-32" y="140" xlink:href="#master-node" />
      <use x="52" y="200" xlink:href="#master-node" />
      <use x="152" y="190" xlink:href="#master-node" />
      <use x="182" y="230" xlink:href="#master-node" />
      <use x="272" y="200" xlink:href="#master-node" />
      <use x="400" y="174" xlink:href="#master-node" />
      <use x="455" y="74" xlink:href="#master-node" />
      <use x="380" y="222" xlink:href="#master-node" />
      
      <rect class="bw dotted" x="30" width="395" height="130" transform="translate(15, 40)"/>
      <title>MasterNodes provided by DAO members</title>
      <a xlink:href="/doc/masternode">
        <text x="210" y="60">Master Node</text>
      </a>

      <a xlink:href="/dev/blockchain" transform="translate(60,70)">
        <rect class="server" width="175" height="80" rx="3"/>
        <text class="big" x="48" y="40">Blockchain</text>
        <text  x="58" y="55">(ethereum)</text>
        <title>Blockchain Client Parity</title>
      </a>
      
      <a xlink:href="/dev/ipfs" transform="translate(250,70)">
        <rect class="server" width="175" height="80" rx="3"/>
        <text class="big" x="17" y="40">Distributed Storage</text>
        <text  x="70" y="55">(ipfs)</text>
        <title>IPFS Nodes</title>
      </a>
      
      <g transform="translate(80,10)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-12" y="14">https</text>
        <title>Application Requests</title>
      </g>
      <g transform="translate(315,10)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-12" y="14">https</text>
        <title>Application Requests</title>
      </g>
      <g transform="translate(125,10)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-8" y="14">wss</text>
        <title>Application Workflow</title>
      </g>
      <g transform="translate(170,10)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-10" y="14">ÐΞV</text>
        <title>Synchronization</title>
      </g>
      <g transform="translate(215,10)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-6" y="14">IN³</text>
        <title>Transaction Security</title>
      </g>
      
      <g transform="translate(360,10)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-8" y="14">p2p</text>
        <title>Synchronization</title>
      </g>
      </g>
    </g>
</svg>

