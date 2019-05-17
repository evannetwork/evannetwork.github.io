---
title: "Blockchain Core API"
parent: Developers
grand_parent: API
nav_order: 4210
permalink: /docs/developers/api/blockchain-core.html
---

<!--
  TODO:
    - refactor overview image
-->

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
    text        { font: 10pt "Verdana", sans-serif; stroke: #003946; fill: #003946; }
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

    <a xlink:href="/docs/how_it_works/services/dbcp.html" transform="translate(20,30)">
      <rect class="module" width="160" height="80" rx="3"/>
      <text class="big" x="56" y="45">DBCP</text>
      <title>Distributed Blockchain Contract Protocol</title>
      <text y="100">
        <tspan x="3">Links Ðapps with Contracts</tspan>
        <tspan x="3" dy="1.3em">Versioning</tspan>
        <tspan x="3" dy="1.3em">Contract Reflection</tspan>
        <tspan class="ns" x="3" dy="1.5em">nameResolver</tspan>
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

    <a xlink:href="/docs/developers/concepts/ipfs.html" transform="translate(420,30)">
      <rect class="module" width="160" height="80" rx="3"/>
      <text class="big" x="64" y="45">dfs</text>
      <title>Distributed File System (IPFS)</title>
      <text y="100">
        <tspan x="3">own dfs namespace</tspan>
        <tspan x="3" dy="1.3em">provides access to IPFS:</tspan>
        <tspan x="12" dy="1.3em" class="code">get</tspan>
        <tspan x="12" dy="1.3em" class="code">add</tspan>
        <tspan x="3" dy="2em">also Provides</tspan>
        <tspan x="12" dy="1.3em" >a local memcache</tspan>
        <tspan x="12" dy="1.3em" >an IPLD interface</tspan>
        <tspan class="ns" x="0" dy="1.5em">dfs</tspan>
        <tspan class="ns" x="0" dy="1.5em">ipld</tspan>
      </text>
    </a>

    <a xlink:href="/docs/developers/concepts/ipfs.html" transform="translate(620,30)">
      <rect class="module" width="160" height="80" rx="3"/>
      <text class="big" x="7" y="45">Smart Contracts</text>
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

</svg>

The [Blockchain Core Library](https://github.com/evannetwork/api-blockchain-core) is the central tool used in all development with evan.network. It is actually a collection of own functionality, and wrappers around 3rd party core functionality like blockchain transactions and distributed file system operations.

The full [API documentation](https://api-blockchain-core.readthedocs.io) shows the actual exposed sub-namespaces in the blockchain core module are a little more fine-grained.
