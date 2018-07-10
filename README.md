# Welcome to evan.network

The `evan.network` is an Ethereum Blockchain with an authority consensus that is publicly available. Our goal ist to offer a 100% Ethereum compliant blockchain that is fast, robust and cost efficient to offer application developers and companies a plattform to build their own decentralized applications.

<dl>
<dt><a href="/doc/first-steps">First Steps</a><dt>
<dd>The easiest way to get started is to just register and create a profile.<br />
This is all already done with distributed web applications.
</dd>
<dt><a href="/doc/goals">General Overview</a></dt>
<dd>And deeper look into the concepts of the <a href="/doc/network">network</a> and the <a href="/doc/dao">DAO</a>.</dd>
<dt><a href="/dev/overview">Technical Details</a></dt>
<dd>If you wanna know how it works and fits together.</dd>
<dt><a href="/dev/getting-started">Start Programming</a></dt>
<dd>Set up the environment and follow the tutorials.</dd>
<dt><a href="/doc/faq">FAQ</a></dt>
<dd> </dd>
<dt><a href="/doc/glossary">Glossary</a></dt>
<dd> </dd>

<p>If you want to join <code>evan.network</code> as an integral part of the infrastructure and shape its future, contact us on our <a href="https:///evan.network">WebSite</a>.
<a style="float: right" alt="Gitter" title="Gitter" href="https://gitter.im/evannetwork/Lobby"><img src="/public/chat.svg"/></a></p>

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
          d="M 0 0 l 25 5 h -5 v 10 h 5 l -25 5 l -25 -5 h 5 v -10 h -5 l 25 -5"  />
    <path id="triangle" style="stroke: f7aacf; fill: #f7aacf;" d="M 0 0 h 200 l -100 10 l -100 -10"  />
  </defs>
  <style type="text/css">
    text        { font: 10pt "Verdana", sans-serif; stroke: #003946; fill: #003946; }
    text.big    { font-size: 12pt; font-weight: bold; }
    text.small  { font-size: 8pt; }
    text.bold   { font-weight: bold; }
    text.white  { stroke: #fff; stroke-width: 1; fill: #fff; }
    text.prot   { stroke: #f7aacf; fill: #f7aacf;}
    text.code   { font: 9pt "Courier", monospace; stroke: #003946; fill: #003946; }
    
    .grey       { stroke: #023845; stroke-width: 1; fill: #023845; fill-opacity: 0.5; opacity: 0.5; }
    .black      { stroke: #003946; stroke-width: 3; fill: #003946; fill-opacity: 1; }
    .thin       { stroke: #2a4d57; stroke-width: 0.5; fill: #2a4d572; fill-opacity: 1; }
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
      <g transform="translate(80, 150)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-13" y="14">https</text>
        <title>Application Requests</title>
      </g>
      <g transform="translate(140, 150)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-10" y="14">wss</text>
        <title>Application Workflow</title>
      </g>
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
          <text class="small" x="50" y="56">Obboarding</text>
          <text class="small" x="55" y="71">Dashboard</text>
          <text class="small thin" x="75" y="89">Login</text>
          <text class="small thin" x="75" y="99">Session</text>
          <text class="small thin" x="75" y="109">Container</text>

        </g>

      </a>
      <g transform="translate(80, 150)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-13" y="14">https</text>
        <title>Application Requests</title>
      </g>
      <g transform="translate(140, 150)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-10" y="14">wss</text>
        <title>Application Workflow</title>
      </g>
    </g>

    <g id="applications" transform="translate(380, 50)">
      <title>Get Started with Programming</title>
      <a xlink:href="/dev/getting-started">
        <rect class="bw dotted" x="30" width="160" height="140" />
        <text x="70" y="15">Applications</text>
        <g transform="translate(70,45)">
          <ellipse class="bubble" rx="35" ry="15" />
          <text class="small" x="-24" y="0.25em">WebApps</text>
        </g>
        
        <g transform="translate(140,65)">
          <ellipse class="bubble" rx="45" ry="15" />
          <text class="small" x="-32" y="0.25em">Native Apps</text>
        </g>
        
        <g transform="translate(90,105)">
          <ellipse class="bubble" rx="45" ry="15" />
          <text class="small" x="-32" y="0.25em">Mobile Apps</text>
        </g>
      </a>
      <g transform="translate(80, 150)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-13" y="14">https</text>
        <title>Application Requests</title>
      </g>
      <g transform="translate(140, 150)">
        <use xlink:href="#protocol" />
        <text class="prot small" x="-10" y="14">wss</text>
        <title>Application Workflow</title>
      </g>
    </g>
  </g>
  <g id="core-api" transform="translate(10, 210)">
    <path class="dotted grey" d="M 0 0 h 580" />
    <text class="big grey" transform="rotate(90)" x="20">Core API</text>
    <use xlink:href="#triangle" x="180" y="-15" />
    
    <a xlink:href="/dev/blockchain-core" transform="translate(100,20)">
      <rect class="library" width="160" height="80" rx="2"/>
      <text class="white" x="24" y="42">Blockchain Core</text>
      <title>ECMAScript Library to work with Ethereum Contracts and IPFS</title>
    </a>

    <a xlink:href="/dev/dbcp" transform="translate(300,20)">
      <rect class="library" width="160" height="80" rx="2"/>
      <text class="white" x="58" y="42">DBCP</text>
      <title>A Description Language for Decentralized Business Applications</title>
    </a>

  </g>
  
  <g id="core-services" transform="translate(10, 340)">
    <path class="dotted grey" d="M 0 0 h 580" />
    <text class="big grey" transform="rotate(90)" x="20">Core Services</text>
    <use xlink:href="#triangle" x="180" y="-15" />
    
    <g transform="translate(0,20)">
      <g transform="translate(160,0)">
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
          <text class="code" x="4" y="12">RightsAndRoles</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#mailbox" transform="translate(60,36)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="4" y="12">Mailbox</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#profile" transform="translate(70,52)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="4" y="12">Profile</text>
          <text class="small grey" x="24" y="30">Roles</text>
          <text class="small grey" x="24" y="46">Crypt Keys</text>
          <title>Ethereum Contract</title>
        </a>

        <text class="small grey" x="220" y="12">factories</text>
        <a xlink:href="/dev/smart-contracts#contract-factories" transform="translate(220,20)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="4" y="12">ProfileFactory</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#contract-factories" transform="translate(230,36)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="4" y="12">DigitalTwinFactory</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#contract-factories" transform="translate(240,52)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="4" y="12">TaskFactory</text>
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
          <text class="code" x="4" y="12">Business Center</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#data-contract" transform="translate(240,182)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="4" y="12">DataContract</text>
          <text class="small grey" x="24" y="30">Entries</text>
          <text class="small grey" x="24" y="46">Access Rights</text>
          <title>Ethereum Contract</title>
        </a>

        <text class="small grey" x="50" y="142">infrastructure</text>
        <a xlink:href="/dev/smart-contracts#ens" transform="translate(50,150)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="4" y="12">ENS</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#event-hub" transform="translate(60,166)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="4" y="12">EventHub</text>
          <title>Ethereum Contract</title>
        </a>
        <a xlink:href="/dev/smart-contracts#base-contract" transform="translate(70,182)">
          <rect class="contract" width="130" height="60" rx="2"/>
          <text class="code" x="4" y="12">BaseContract</text>
          <text class="small grey" x="24" y="30">DBCP Reference</text>
          <text class="small grey" x="24" y="46">Sharing</text>
          <title>Ethereum Contract</title>
        </a>
      </g>
      <g transform="translate(50,0)">
        <a xlink:href="/dev/key-exchange" transform="translate(0,20)">
          <rect class="library" width="120" height="80" rx="2"/>
          <text class="white" x="14" y="42">Key Exchange</text>
        </a>

        <a xlink:href="/dev/blockchain#rpc-endpoint" transform="translate(0,150)">
          <rect class="server" width="120" height="80" rx="2"/>
          <text class="big" x="16" y="40">RPC Node</text>
          <text  x="21" y="55">(ethereum)</text>
          <title>Blockchain Client Parity</title>
        </a>
      </g>
    </g>
  </g>

  <g id="core-network" transform="translate(10, 630)">
    <path class="dotted grey" d="M 0 0 h 580" />
    <text class="big grey" transform="rotate(90)" x="20">Core Network</text>
    <use xlink:href="#triangle" x="180" y="-15" />

    <rect class="bw dotted" x="30" width="480" height="200" transform="translate(35, 40)"/>
    <rect class="bw dotted" x="30" width="480" height="200" transform="translate(30, 35)"/>
    <rect class="bw dotted" x="30" width="480" height="200" transform="translate(25, 30)"/>
    <rect class="bw dotted" x="30" width="480" height="200" transform="translate(20, 25)"/>
    <rect class="bw dotted" x="30" width="480" height="200" transform="translate(15, 20)"/>
    
    <title>Many MasterNodes provided by DAO members</title>
    <a xlink:href="/doc/masternode">
      <text x="240" y="45">Master Node</text>
    </a>


    <a xlink:href="/dev/blockchain" transform="translate(60,60)">
      <rect class="server" width="210" height="80" rx="3"/>
      <text class="big" x="58" y="40">Blockchain</text>
      <text  x="68" y="55">(ethereum)</text>
      <title>Blockchain Client Parity</title>
    </a>

    <a xlink:href="/dev/ipfs" transform="translate(300,60)">
      <rect class="server" width="210" height="80" rx="3"/>
      <text class="big" x="15" y="40">Distributed Storage</text>
      <text  x="81" y="55">(ipfs)</text>
      <title>IPFS Nodes</title>
    </a>

    <g transform="translate(85, 160)">
      <use xlink:href="#protocol" />
      <text class="prot small" x="-13" y="14">https</text>
      <title>Application Requests</title>
    </g>
    <g transform="translate(375, 160)">
      <use xlink:href="#protocol" />
      <text class="prot small" x="-13" y="14">https</text>
      <title>Application Requests</title>
    </g>
    <g transform="translate(140, 160)">
      <use xlink:href="#protocol" />
      <text class="prot small" x="-10" y="14">wss</text>
      <title>Application Workflow</title>
    </g>
    <g transform="translate(195, 160)">
      <use xlink:href="#protocol" />
      <text class="prot small" x="-10" y="14">ÐΞV</text>
      <title>Synchronization</title>
    </g>
    <g transform="translate(250, 160)">
      <use xlink:href="#protocol" />
      <text class="prot small" x="-6" y="14">IN³</text>
      <title></title>
    </g>
    
    <g transform="translate(430, 160)">
      <use xlink:href="#protocol" />
      <text class="prot small" x="-9" y="14">p2p</text>
      <title>Synchronization</title>
    </g>
    </g>
</svg>

