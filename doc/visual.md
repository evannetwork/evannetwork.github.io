---
title: "Evan.network Architectural Overview"
---
# Evan.network Architectural Overview

<g
   transform="translate(80,70) scale(0.5)"
   id="g4325">
  <path
     d="M24.6,95.3h50.8c3.8,0,6.9-3.1,6.9-6.9V11.5c0-3.8-3.1-6.9-6.9-6.9H24.6c-3.8,0-6.9,3.1-6.9,6.9v76.9  C17.7,92.2,20.8,95.3,24.6,95.3z M50,92.6c-1.1,0-2.1-0.9-2.1-2.1s0.9-2.1,2.1-2.1c1.1,0,2.1,0.9,2.1,2.1S51.1,92.6,50,92.6z   M21.4,13.6c0-1.1,0.9-2,2-2h53.1c1.1,0,2,0.9,2,2v70.1c0,1.1-0.9,2-2,2H23.5c-1.1,0-2-0.9-2-2V13.6z"
     />
  <path
     transform="scale(0.75) translate(80,70)"
     d="M67.286,7.58H32.714c-3.45,0-6.246,2.797-6.246,6.246v72.347c0,3.45,2.797,6.246,6.246,6.246h34.572  c3.45,0,6.246-2.797,6.246-6.246V13.827C73.532,10.377,70.736,7.58,67.286,7.58z M50,90.394c-1.944,0-3.52-1.576-3.52-3.52  s1.576-3.52,3.52-3.52s3.52,1.576,3.52,3.52S51.944,90.394,50,90.394z M69.526,80.946H30.474V13.83c0-0.085,0.07-0.155,0.155-0.155  h38.742c0.086,0,0.155,0.069,0.155,0.155V80.946z"
     />
</g>
<g
   transform="translate(260,70)"
   id="g4339">
  <g
     transform="scale(0.125)"
     id="g4335">
    <path
       d="M458.725,36H53.275c-26.468,0-48,21.533-48,48v251.826c0,26.467,21.532,48,48,48h98.835L133.828,440h-22.234   c-9.941,0-18,8.059-18,18s8.059,18,18,18h282.667c9.941,0,18-8.059,18-18s-8.059-18-18-18h-22.234l-18.283-56.174h104.981   c26.468,0,48-21.533,48-48V84C506.725,57.533,485.192,36,458.725,36z M334.168,440H171.686l18.283-56.174h125.916L334.168,440z    M470.725,335.826c0,6.617-5.383,12-12,12H53.275c-6.617,0-12-5.383-12-12V84c0-6.617,5.383-12,12-12h405.449   c6.617,0,12,5.383,12,12V335.826z"
       id="path4327" />
    <path
       d="M252.874,164.132c-24.867,0-45.098,20.23-45.098,45.098c0,25.282,20.23,45.851,45.098,45.851s45.098-20.231,45.098-45.098   C297.972,184.7,277.741,164.132,252.874,164.132z M252.874,219.08c-4.932,0-9.098-4.511-9.098-9.851   c0-5.102,3.996-9.098,9.098-9.098c4.932,0,9.098,4.511,9.098,9.85C261.972,215.083,257.976,219.08,252.874,219.08z"
       id="path4329" />
    <path
       d="M354.902,164.132c-24.867,0-45.098,20.23-45.098,45.098s20.23,45.098,45.098,45.098S400,234.097,400,209.229   S379.77,164.132,354.902,164.132z M354.902,218.327c-5.102,0-9.098-3.996-9.098-9.098s3.996-9.098,9.098-9.098   s9.098,3.996,9.098,9.098S360.004,218.327,354.902,218.327z"
       id="path4331" />
    <path
       d="M150.845,164.132c-24.867,0-45.098,20.23-45.098,45.098s20.23,45.098,45.098,45.098s45.099-20.23,45.099-45.098   C195.943,183.941,176.134,164.132,150.845,164.132z M150.845,218.327c-5.102,0-9.098-3.996-9.098-9.098s3.996-9.098,9.098-9.098   c6.716,0,9.099,4.901,9.099,9.098C159.943,214.331,155.946,218.327,150.845,218.327z"
       id="path4333" />
  </g>
  <text
     class="thin"
     x="80"
     y="90"
     transform="scale(0.75)"
     id="text4337">Web Apps</text>
</g>
<g
   id="edge-server"
   transform="translate(20,150)">
  <rect
     class="bw dotted"
     x="30"
     width="320"
     height="400"
     id="rect4341"
     y="0"
     style="fill:#ffffff;fill-opacity:1;stroke:#003946;stroke-dasharray:1, 1" />
  <text
     x="130"
     y="15"
     >Ethereum Blockchain</text>
  <g
     transform="translate(0,10)"
     id="g4369">
    <text
       class="code grey"
       x="42"
       y="24"
       >User Profiles</text>
    <rect
       class="contract"
       x="40"
       y="30"
       width="130"
       height="60"
       id="rect4347"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <rect
       class="contract"
       x="45"
       y="45"
       width="130"
       height="60"
       id="rect4349"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <rect
       class="contract"
       x="50"
       y="60"
       width="130"
       height="60"
       id="rect4351"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <text
       class="small"
       x="45"
       y="41"
       >Peter Lustig</text>
    <text
       class="small"
       x="50"
       y="56"
       >Hanna Hempel</text>
    <text
       class="small"
       x="55"
       y="71"
       >Fritz Kunz</text>
    <text
       class="small thin"
       x="75"
       y="86"
       >Keys</text>
    <text
       class="small thin"
       x="75"
       y="96"
       >Contacts</text>
    <text
       class="small thin"
       x="75"
       y="106"
       >Bookmarks</text>
    <text
       class="small thin"
       x="75"
       y="116"
       >...</text>
    <use
       xlink:href="#seal"
       id="use4367"
       x="0"
       y="0"
       width="100%"
       height="100%" />
  </g>
  <path
     class="create2"
     d="m 140,140 10,10"
     id="path4371"
     />
  <path
     class="create2"
     d="m 330,140 -10,10"
     id="path4373"
     />
  <path
     class="create2"
     d="m 150,200 -10,10"
     id="path4375"
     />
  <path
     class="create2"
     d="m 300,265 v 20"
     id="path4377"
     />
  <path
     class="create"
     d="m 160,335 c -0.77297,22.31891 12.97056,19.89949 20,20"
     id="path4379"
     />
  <g
     transform="translate(160,10)"
     id="g4405">
    <text
       class="code grey"
       x="42"
       y="24"
       >Company Profiles</text>
    <rect
       class="contract"
       x="40"
       y="30"
       width="130"
       height="60"
       id="rect4383"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <rect
       class="contract"
       x="45"
       y="45"
       width="130"
       height="60"
       id="rect4385"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <rect
       class="contract"
       x="50"
       y="60"
       width="130"
       height="60"
       id="rect4387"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <text
       class="small"
       x="45"
       y="41"
       >Construction Carl</text>
    <text
       class="small"
       x="50"
       y="56"
       >Software Services GmbH</text>
    <text
       class="small"
       x="55"
       y="71"
       >Rental Equipment KG</text>
    <text
       class="small thin"
       x="75"
       y="86"
       >Keys</text>
    <text
       class="small thin"
       x="75"
       y="96"
       >Contacts</text>
    <text
       class="small thin"
       x="75"
       y="106"
       >Bookmarks</text>
    <text
       class="small thin"
       x="75"
       y="106"
       >...</text>
    <use
       xlink:href="#seal"
       id="use4403"
       x="0"
       y="0"
       width="100%"
       height="100%" />
  </g>
  <g
     transform="translate(130,130)"
     id="g4431">
    <text
       class="code grey"
       x="42"
       y="24"
       >Business Centers</text>
    <rect
       class="contract"
       x="40"
       y="30"
       width="130"
       height="60"
       id="rect4409"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <rect
       class="contract"
       x="45"
       y="45"
       width="130"
       height="60"
       id="rect4411"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <rect
       class="contract"
       x="50"
       y="60"
       width="130"
       height="60"
       id="rect4413"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <text
       class="small"
       x="45"
       y="41"
       >Agriculture</text>
    <text
       class="small"
       x="50"
       y="56"
       >IT Berlin</text>
    <text
       class="small"
       x="55"
       y="71"
       >Construction Saxony</text>
    <text
       class="small thin"
       x="75"
       y="86"
       >Members</text>
    <text
       class="small thin"
       x="75"
       y="96"
       >Bidding Calls</text>
    <text
       class="small thin"
       x="75"
       y="106"
       >Offers</text>
    <text
       class="small thin"
       x="75"
       y="116"
       >...</text>
    <use
       xlink:href="#seal"
       id="use4429"
       x="0"
       y="0"
       width="100%"
       height="100%" />
  </g>
  <g
     transform="translate(0,210)"
     id="g4455">
    <text
       class="code grey"
       x="42"
       y="24"
       >Factories</text>
    <rect
       class="contract"
       x="40"
       y="30"
       width="130"
       height="60"
       id="rect4435"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <rect
       class="contract"
       x="45"
       y="45"
       width="130"
       height="60"
       id="rect4437"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <rect
       class="contract"
       x="50"
       y="60"
       width="130"
       height="60"
       id="rect4439"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <text
       class="small"
       x="45"
       y="41"
       id="text4441"
       >DigitalTwinFactory</text>
    <text
       class="small"
       x="50"
       y="56"
       >ServiceFactory</text>
    <text
       class="small"
       x="55"
       y="71"
       >TaskFactory</text>
    <text
       class="small thin"
       x="75"
       y="86"
       >creates contracts</text>
    <text
       class="small thin"
       x="75"
       y="96"
       >initializes entries</text>
    <text
       class="small thin"
       x="75"
       y="106"
       >initializes roles</text>
    <use
       xlink:href="#seal"
       id="use4453"
       x="0"
       y="0"
       width="100%"
       height="100%" />
  </g>
  <g
     transform="translate(160,270)"
     id="g4479">
    <text
       class="code grey"
       x="42"
       y="24"
       >Contracts</text>
    <rect
       class="contract"
       x="40"
       y="30"
       width="130"
       height="60"
       id="rect4459"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <rect
       class="contract"
       x="45"
       y="45"
       width="130"
       height="60"
       id="rect4461"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <rect
       class="contract"
       x="50"
       y="60"
       width="130"
       height="60"
       id="rect4463"
       style="fill:#e0e6e7;stroke:#8a9ea4;stroke-width:1" />
    <text
       class="small"
       x="45"
       y="41"
       >DigitalTwin</text>
    <text
       class="small"
       x="50"
       y="56"
       >Service</text>
    <text
       class="small"
       x="55"
       y="71"
       >Task</text>
    <text
       class="small thin"
       x="75"
       y="90"
       >Contract Parameters</text>
    <text
       class="small thin"
       x="75"
       y="100"
       >Access Rights</text>
    <text
       class="small thin"
       x="75"
       y="110"
       >...</text>
    <use
       xlink:href="#seal"
       id="use4477"
       x="0"
       y="0"
       width="100%"
       height="100%" />
  </g>
</g>
