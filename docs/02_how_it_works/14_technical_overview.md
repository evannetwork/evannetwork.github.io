---
title: "evan.network Technical Overview"
parent: How it works
nav_order: 14
permalink: /docs/02_how_it_works/technical_overview.html
---

<svg id="evan.network" version="1.1" width="100%" viewBox="0 0 1000 620" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
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
  </defs>
  <style type="text/css">
    text        { font: 10pt "PT Sans", Helvetica, Arial, sans-serif; stroke: #003946; fill: #003946; }
    text.big    { font-size: 12pt; font-weight: bold; stroke-width: 0;}
    text.small  { font-size: 9pt; }
    text.bold   { font-weight: bold; }
    text.white  { stroke: #fff; stroke-width: 1; fill: #fff; }
    a           { cursor: pointer; }


    .grey       { stroke: #023845; stroke-width: 1; fill: #023845; fill-opacity: 0.5; opacity: 0.5; }
    .black      { stroke: #003946; stroke-width: 3; fill: #003946; fill-opacity: 1; }
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
    .module     { fill: ; stroke: #63ceca; }
    .server     { fill: #a6dddc; stroke: #003946; stroke-width: 2; }
    .service    { fill: #f7aacf; stroke: #003946; stroke-width: 2; }

  </style>

  <text x="350" y="20" style="font-size: 20pt;">Evan Network Infrastructure</text>
  <g transform="translate(0,80)">
    <title>evan.network AuthorityNodes</title>
    <rect class="bw dotted" width="410" height="240" transform="translate(15,-15)"/>
    <rect class="bw dotted" width="410" height="240" transform="translate(10,-10)"/>
    <rect class="bw dotted" width="410" height="240" transform="translate(5,-5)"/>
    <rect class="bw dotted" width="410" height="240"/>
    <rect class="bw dotted" width="410" height="240"/>
    <a xlink:href="/docs/02_how_it_works/authoritynode.html">
      <text x="160" y="20">AuthorityNode</text>
    </a>
    <text class="grey small" x="70" y="230">every DAO member runs a AuthorityNode</text>
    <a xlink:href="/dev/blockchain" transform="translate(20,30)">
      <rect class="server" width="160" height="80" rx="3"/>
      <text class="big" x="50" y="38">
        <tspan>Signing</tspan>
        <tspan x="70" dx="-0.75em" dy="1em">Parity</tspan>
      </text>
      <title>AuthorityNode Ethereum Client</title>
    </a>
    <a xlink:href="/dev/blockchain" transform="translate(220,130)">
      <rect class="server" width="160" height="80" rx="3"/>
      <text class="big" x="52" y="38">
        <tspan x="35">Transaction</tspan>
        <tspan x="70" dx="-0.75em" dy="1em">Parity</tspan>
      </text>
      <title>AuthorityNode Ethereum Client</title>
    </a>
    <a xlink:href="/dev/ipfs" transform="translate(20,130)">
      <rect class="server" width="160" height="80" rx="3"/>
      <text class="big" x="62" y="45">IPFS</text>
      <title>Redundant Interplanetary File System AuthorityNode</title>
    </a>
    <a xlink:href="/dev/ipfs" transform="translate(220,30)">
      <rect class="server" width="160" height="80" rx="3"/>
      <text class="big" x="62" y="45">IPFS</text>
      <title>Redundant Interplanetary File System AuthorityNode</title>
    </a>
    <path class="bidirectional-lookup" d="M 190 110 l 20 20"/>
    <path class="bidirectional-lookup" d="M 190 130 l 20 -20"/>
  </g>

  <g transform="translate(0,360)">
    <rect class="bw dotted" width="410" height="240"/>
      <title>evan.network Distributed Application</title>
    <a  xlink:href="/dapps/introduction">
      <text x="140" y="20">Ðapp (in Browser)</text>
    </a>

    <a xlink:href="/dev/blockchain-core" transform="translate(20,30)">
      <rect class="library" width="360" height="80" rx="3"/>
      <text class="big white" x="115" y="45">Blockchain Core</text>
      <title>Blockchain Core Library</title>
    </a>

    <a xlink:href="/dapps/angular/hello-world" transform="translate(20,130)">
      <rect class="library" width="360" height="80" rx="3"/>
      <text class="big white" x="115" y="40">Web Framework</text>
      <text class="white" x="110" y="60">(angular, vue, jquery ...)</text>
      <title>Any Web Framework or Library is Usable</title>
    </a>
  </g>

  <g transform="translate(540,80)">
    <rect class="bw dotted" width="410" height="240"/>
    <title>evan.network Web Service</title>
    <a xlink:href="/dev/smart-agents">
      <text x="160" y="20">Edge Server</text>
    </a>
    <text class="grey small" x="45" y="230">primarily used for services with special access rights</text>

    <a xlink:href="/dev/blockchain-core" transform="translate(20,30)">
      <rect class="library" width="360" height="80" rx="3"/>
      <text class="big white" x="115" y="45">Blockchain Core</text>
      <title>Blockchain Core Library</title>
    </a>

    <a xlink:href="/dev/smart-agents" transform="translate(20,130)">
      <rect class="library" width="360" height="80" rx="3"/>
      <text class="big white" x="127" y="45">Smart Agent</text>
      <title>an ActionHero</title>
    </a>
  </g>

  <g transform="translate(540,360)">
    <rect class="bw dotted" width="410" height="240"/>
      <title>Any Normal Webservice</title>
    <a xlink:href="/dev/smart-agents">
      <text x="180" y="20">Services</text>
    </a>

    <g transform="translate(78,50)">
      <g transform="translate(20,30)">
        <ellipse class="service" rx="80" ry="40" />
        <text class="big" x="-17" y="0.3em">SAP</text>
      </g>

      <g transform="translate(50,130)">
        <ellipse class="service" rx="80" ry="40" />
        <text class="big" x="-17" y="0.3em">SQL</text>
      </g>

      <g transform="translate(220,70)">
        <ellipse class="service" rx="80" ry="40" />
        <text class="big" x="-35" y="0.3em">wetter.de</text>
      </g>
    </g>
  </g>

  <g transform="translate(60, 390)">
    <path class="data-flow" d="M 0 0 v -90"/>
    <text class="grey" x="10" y="-45">https</text>
  </g>

  <g transform="translate(320, 390)">
    <path class="data-flow" d="M 0 0 v -90"/>
    <text class="grey" x="10" y="-45">websocket</text>
  </g>


  <g transform="translate(560, 130)">
    <path class="data-flow" d="M 0 0 h -170"/>
    <text class="grey" x="-100" y="-15">https</text>
  </g>

  <g transform="translate(760, 318)">
    <path class="data-flow" d="M 0 0 v 35"/>
    <text class="grey" x="10" y="28">https, RPC, SMTP ...</text>
  </g>

  <g transform="translate(410, 430)">
    <path class="data-flow" d="M 0 0 h 100 v -160 h 40"/>
    <text class="grey" x="42" y="-15">https</text>
  </g>

  <g transform="translate(560, 170)">
    <path class="data-flow" d="M 0 0 h -50 v 60 h -120"/>
    <text class="grey" x="-128" y="45">websocket</text>
  </g>
  <g id="legend" transform="translate(20, 40)">
    <rect class="server" width="20" height="20"/>
    <text class="small" x="30" y="15">server</text>
    <circle class="service" cy="10" cx="120" r="10"/>
    <text class="small" x="140" y="15">service</text>
    <rect class="library" x="230" width="20" height="20"/>
    <text class="small" x="260" y="15">library</text>

    <path class="data-flow" d="M 340 10 h 20"/>
    <text class="small" x="380" y="15">network requests</text>
    <path class="lookup" d="M 510 10 h 20"/>
    <text class="small" x="550" y="15">synchronizes</text>

  </g>
</svg>

The evan.network builds on existing technology like a programmable blockchain with [Ethereum](https://ethereum.org), and a distributed file storage with [IPFS](https://ipfs.io).

It combines those two technologies and provides the storage and computing power and bandwidth to run distributed
applications with the [AuthorityNodes](/docs/02_how_it_works/authoritynode.html).

All this infrastructure is exposed and made usable by fairly ordinary web-applications via the [Blockchain Core Library](/dev/blockchain-core).

This means that all data in the blockchain and all data in the IPFS are completely open to everyone to read,
unless encrypted, and the entire application code would run in the browser and is fully readable and modifiable. Accordingly, there exists a need for a third class of code, which isn't as cryptographically secured as blockchain code, but also not as
exposed as Javascript in your browser. This could be something with exclusive access rights to certain contracts in the blockchain and other limited resources. For this reason, [Smart Agents](/dev/smart-agents) exist.
They are just small webservices, that run on controlled servers providing controlled access to resources and contracts that others might need access too, but can't be given full rights.

<!-- moved to plunder -->

<!-- 
<svg id="blockchain-core" version="1.1" width="100%" viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
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
  </defs>
  <style type="text/css">
    a#belt rect { fill: url(#slot-fill); stroke: #003946; }
    text        { font: 10pt "PT Sans", Helvetica, Arial, sans-serif; stroke: #003946; fill: #003946; }
    text.big    { font-size: 12pt; font-weight: bold; }
    text.small  { font-size: 9pt; }
    text.bold   { font-weight: bold; }
    text.white  { stroke: #fff; stroke-width: 1; fill: #fff; }
    text.code,
    tspan.code  { font: 9pt "Courier", monospace; stroke: #003946; fill: #003946; }
    text.ns,
    tspan.ns    { font: 10pt "Courier", monospace; stroke: #ef7fb9; fill: #ef7fb9; }

    .grey       { stroke: #023845; stroke-width: 1; fill: #023845; fill-opacity: 0.5; opacity: 0.5; }
    .black      { stroke: #003946; stroke-width: 3; fill: #003946; fill-opacity: 1; }
    .bw         { stroke: #003946; fill-opacity: 1; fill: #fff; }
    .slot       { fill: url(#slot-fill); stroke: #003946; }
    .region     { stroke: #aaa; stroke-dasharray: 2 1; fill-opacity: 0; }

    .dram       { fill: #bdd; stroke: none; }
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

  </style>

  <a xlink:href="https://github.com/evannetwork/api-blockchain-core">
   <text x="240" y="20" style="font-size: 20pt;">Blockchain Core Library</text>
  </a>
  <g transform="translate(0,80)">
    <title>Blockchain Core Library</title>
    <rect class="bw dotted" width="800" height="320"/>
    <a xlink:href="https://github.com/evannetwork/api-blockchain-core">
      <text x="350" y="20">blockchain-core</text>
    </a>
    <text class="grey small" x="76" y="230"></text>

    <a xlink:href="/dev/dbcp" transform="translate(20,30)">
      <rect class="module" width="160" height="80" rx="3"/>
      <text class="big" x="60" y="45">DBCP</text>
      <title>Distributed Blockchain Contract Protocol</title>
      <text y="100">
        <tspan x="3">links Ðapps with contracts</tspan>
        <tspan x="3" dy="1.3em">versioning</tspan>
        <tspan x="3" dy="1.3em">contract API reflection</tspan>
        <tspan class="ns" x="3" dy="1.5em">nameResolver</tspan>
        <tspan class="ns" x="3" dy="1.5em">cryptor</tspan>
        <tspan class="ns" x="3" dy="1.5em">contractLoader</tspan>
        <tspan class="ns" x="3" dy="1.5em">onboarding</tspan>
        <tspan class="ns" x="3" dy="1.5em">keyExchange</tspan>
      </text>

    </a>

    <a xlink:href="https://github.com/ethereum/web3.js" transform="translate(220,30)">
      <rect class="module" width="160" height="80" rx="3"/>
      <text class="big" x="60" y="45">web3</text>
      <title>Blockchain Interactions</title>
      <text y="100">
        <tspan x="3">read contracts</tspan>
        <tspan x="3" dy="1.3em">transactions</tspan>
        <tspan x="3" dy="1.3em">encryption</tspan>
        <tspan x="3" dy="1.3em">signing</tspan>
        <tspan x="3" dy="1.3em">events</tspan>
        <tspan class="ns" x="0" dy="1.5em">web3</tspan>
        <tspan class="ns" x="0" dy="1.5em">executor</tspan>
        <tspan class="ns" x="0" dy="1.5em">signer</tspan>
      </text>
    </a>

    <a xlink:href="/dev/IPFS" transform="translate(420,30)">
      <rect class="module" width="160" height="80" rx="3"/>
      <text class="big" x="68" y="45">dfs</text>
      <title>Distributed File System (IPFS)</title>
      <text y="100">
        <tspan x="3">own dfs namespace</tspan>
        <tspan x="3" dy="1.3em">provides access to IPFS:</tspan>
        <tspan x="12" dy="1.3em" class="code">get</tspan>
        <tspan x="12" dy="1.3em" class="code">add</tspan>
        <tspan x="12" dy="1.3em" class="code">pin add</tspan>
        <tspan x="3" dy="2em">also Provides</tspan>
        <tspan x="12" dy="1.3em" >a local memcache</tspan>
        <tspan x="12" dy="1.3em" >an IPLD interface</tspan>
        <tspan class="ns" x="0" dy="1.5em">dfs</tspan>
        <tspan class="ns" x="0" dy="1.5em">ipld</tspan>
        <tspan class="ns" x="0" dy="1.5em">keyProvider</tspan>
      </text>
    </a>

    <a xlink:href="/docs/02_how_it_works/smart-contracts.html#smart-contracts-in-evannetwork" transform="translate(620,30)">
      <rect class="module" width="160" height="80" rx="3"/>
      <text class="big" x="22" y="45">Smart Contracts</text>
      <title>Basic Functionality Contracts</title>
      <text y="100">
        <tspan x="3">solidity compilation</tspan>
        <tspan x="3" dy="1.3em">profiles</tspan>
        <tspan x="3" dy="1.3em">access rights</tspan>
        <tspan x="3" dy="1.3em">data contracts</tspan>
        <tspan x="3" dy="1.3em">mail box</tspan>
        <tspan x="3" dy="1.3em">...</tspan>
        <tspan class="ns" x="0" dy="1.5em">profile</tspan>
        <tspan class="ns" x="0" dy="1.5em">dataContract</tspan>
        <tspan class="ns" x="0" dy="1.5em">serviceContract</tspan>
        <tspan class="ns" x="0" dy="1.5em">mailbox</tspan>
      </text>
    </a>
  </g>

  <g id="legend" transform="translate(20, 40)">
    <rect class="module" width="20" height="20"/>
    <text class="small" x="30" y="15">module</text>
    <text class="ns" x="140" y="15">namespace</text>
    <!--
    <circle class="service" cy="10" cx="120" r="10"/>
    <text class="small" x="140" y="15">service</text>
    <rect class="library" x="230" width="20" height="20"/>
    <text class="small" x="260" y="15">library</text>

    <path class="data-flow" d="M 340 10 h 20"/>
    <text class="small" x="380" y="15">network requests</text>
    <path class="lookup" d="M 510 10 h 20"/>
    <text class="small" x="550" y="15">synchronizes</text>
    -->
  </g>

</svg> -->
<!-- 
The Blockchain Core Library is the central tool used in all development with evan.network. It is actually a collection of own functionalities and wrappers around third party core functionalities like blockchain transactions and distributed file system operations.

[The full API documentation](https://github.com/evannetwork/api-blockchain-core) shows the actual exposed sub-namespaces in the blockchain core module are slightly more fine-grained.

 -->