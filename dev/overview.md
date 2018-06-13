---
title: "evan.network Technical Overview"
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
    a#belt rect { fill: url(#slot-fill); stroke: #003946; }
    text        { font: 10pt "Verdana", sans-serif; stroke: #003946; fill: #003946; }
    text.big    { font-size: 12pt; font-weight: bold; }
    text.small  { font-size: 9pt; }
    text.bold   { font-weight: bold; }
    text.white  { stroke: #fff; stroke-width: 1; fill: #fff; }

    
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
    .module     { fill: ; stroke: #63ceca; }
    .server     { fill: #a6dddc; stroke: #003946; stroke-width: 2; }
    .service    { fill: #f7aacf; stroke: #003946; stroke-width: 2; }

  </style>

  <text x="350" y="20" style="font-size: 20pt;">Evan Network Infrastructure</text>
  <g transform="translate(0,80)">
    <title>evan.network Master Nodes</title>
    <rect class="bw dotted" width="410" height="240" transform="translate(15,-15)"/>        
    <rect class="bw dotted" width="410" height="240" transform="translate(10,-10)"/>
    <rect class="bw dotted" width="410" height="240" transform="translate(5,-5)"/>
    <rect class="bw dotted" width="410" height="240"/>
    <rect class="bw dotted" width="410" height="240"/>
    <a xlink:href="/doc/masternode">
      <text class="grey" x="160" y="20">Master Node</text>
    </a>
    <text class="grey small" x="76" y="230">every DAO member runs a MasterNode</text>
    <a xlink:href="/doc/parity" transform="translate(20,30)">
      <rect class="server" width="160" height="80" rx="3"/>
      <text class="big" x="48" y="38">
        <tspan>Master</tspan>
        <tspan x="48" dx="-0.75em" dy="1em">Ethereum</tspan>
      </text>
      <title>Redundant MasterNode Parity</title>
    </a>
    <a xlink:href="/doc/parity" transform="translate(220,130)">
      <rect class="server" width="160" height="80" rx="3"/>
      <text class="big" x="48" y="38">
        <tspan>Master</tspan>
        <tspan x="48" dx="-0.75em" dy="1em">Ethereum</tspan>
      </text>
      <title>Redundant MasterNode Parity</title>
    </a>
    <a xlink:href="/dev/ipfs" transform="translate(20,130)">
      <rect class="server" width="160" height="80" rx="3"/>
      <text class="big" x="64" y="45">IPFS</text>
      <title>Redundant Interplanetary File System MasterNode</title>
    </a>
    <a xlink:href="/dev/ipfs" transform="translate(220,30)">
      <rect class="server" width="160" height="80" rx="3"/>
      <text class="big" x="64" y="45">IPFS</text>
      <title>Redundant Interplanetary File System MasterNode</title>
    </a>
    <path class="bidirectional-lookup" d="M 190 110 l 20 20"/>
    <path class="bidirectional-lookup" d="M 190 130 l 20 -20"/>
  </g>

  <g transform="translate(0,360)">
    <rect class="bw dotted" width="410" height="240"/>
      <title>evan.network Distributed Application</title>    
    <a  xlink:href="/dapps/introduction">
      <text class="grey" x="140" y="20">Ðapp (in Browser)</text>
    </a>

    <a xlink:href="/dev/blockchain-core" transform="translate(20,30)">
      <rect class="library" width="360" height="80" rx="3"/>
      <text class="big white" x="110" y="45">Blockchain Core</text>
      <title>Blockchain Core Library</title>
    </a>

    <a xlink:href="/dapps/angular/hello-world" transform="translate(20,130)">
      <rect class="library" width="360" height="80" rx="3"/>
      <text class="big white" x="110" y="40">Web Framework</text>
      <text class="white" x="106" y="60">(angular, vue, jquery ...)</text>
      <title>Any Web Framework or Library is Usable</title>
    </a>
  </g>

  <g transform="translate(540,80)">
    <rect class="bw dotted" width="410" height="240"/>
    <title>evan.network Web Service</title>
    <a xlink:href="/dev/smart-agents">
      <text class="grey" x="160" y="20">Edge Server</text>
    </a>
    <text class="grey small" x="45" y="230">primarily used for services with special access rights</text>

    <a xlink:href="/dev/blockchain-core" transform="translate(20,30)">
      <rect class="library" width="360" height="80" rx="3"/>
      <text class="big white" x="110" y="45">Blockchain Core</text>
      <title>Blockchain Core Library</title>
    </a>

    <a xlink:href="/dev/smart-agents" transform="translate(20,130)">
      <rect class="library" width="360" height="80" rx="3"/>
      <text class="big white" x="125" y="45">Smart Agent</text>
      <title>an ActionHero</title>
    </a>
  </g>

  <g transform="translate(540,360)">
    <rect class="bw dotted" width="410" height="240"/>
      <title>Any Normal Webservice</title>    
    <a xlink:href="/dev/smart-agents">
      <text class="grey" x="160" y="20">Web Services</text>
    </a>

    <g transform="translate(78,50)">
      <g transform="translate(20,30)">
        <ellipse class="service" rx="80" ry="40" />
        <text class="big" x="-50" y="0.25em">google.com</text>
      </g>
    
      <g transform="translate(50,130)">
        <ellipse class="service" rx="80" ry="40" />
        <text class="big" x="-55" y="0.25em">amazon.com</text>
      </g>
      
      <g transform="translate(220,70)">
        <ellipse class="service" rx="80" ry="40" />
        <text class="big" x="-45" y="0.25em">wetter.de</text>
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

  <g transform="translate(410, 530)">
    <path class="data-flow" d="M 0 0 h 120"/>
    <text class="grey" x="42" y="-15">https</text>
  </g>

  <g transform="translate(560, 130)">
    <path class="data-flow" d="M 0 0 h -170"/>
    <text class="grey" x="-100" y="-15">https</text>
  </g>
  
  <g transform="translate(760, 318)">
    <path class="data-flow" d="M 0 0 v 35"/>
    <text class="grey" x="10" y="28">https</text>
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

It combines those two technologies, and provides the storage and computing power and bandwidth to run distributed
applications with the [Master Nodes](/doc/masternode).

All this infrastructure is exposed and made usable by fairly ordinary Web-Applications via the [Blockchain Core Library](/dev/blockchain-core).

Since this means, that all data in the blockchain, and all data in the IPFS are completely open to everyone to read,
unless encrypted, and all application code would run in the browser and is fully readable and modifiable, there
exists a need for a third class of code, that isn't as cryptographically secured as blockchain code, but also not as
exposed as Javascript in your browser. Maybe something with exclusive access rights to certain contracts in the blockchain and other limited resources. For this reason [Smart Agents](/dev/smart-agents) exist.
They are just small webservices, that run on controlled servers, that provide controlled access to resources and contracts that others might need access too, but can't be given full rights.
