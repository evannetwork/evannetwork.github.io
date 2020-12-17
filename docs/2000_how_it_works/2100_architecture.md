---
title: "Architecture"
parent: How it works
nav_order: 2100
permalink: /docs/how_it_works/architecture.html
---

# Overview

The evan.network builds on existing blockchain technology with [Ethereum](https://ethereum.org) and a distributed file storage with [IPFS](https://ipfs.io).

This section describes the Overview of the Blockchain and the API's of evan.network

**Blockchain API** contains the programmable API of evan.network. The API offers many different services which are described in the following sections.

**Core Network** is hosted by AuthorityNodes and they provide access to the built-in [distributed storage service](/docs/how_it_works/services/ipfsfilehandling.html) and the underlying Blockchain layer.

<p style="text-align:center">
<?xml version="1.0" encoding="UTF-8"?>
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="653px" height="763px" viewBox="-0.5 -0.5 653 763" content="&lt;mxfile modified=&quot;2020-12-17T11:39:53.242Z&quot; host=&quot;Electron&quot; agent=&quot;5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) draw.io/12.9.13 Chrome/80.0.3987.163 Electron/8.2.1 Safari/537.36&quot; etag=&quot;YH7tTg2inAnzsmHaoXEK&quot; version=&quot;12.9.13&quot; type=&quot;device&quot;&gt;&lt;diagram id=&quot;u0hEuSjEkNMO_d3kX0L-&quot; name=&quot;Page-1&quot;&gt;7Vtdd6I6FP01PuqCBFAf/agzvTPjddWumTtPXREi5BYIN8Sq/fU3gaBAsO202jrt+FDJIYZw9snOyU7agqNo84mhJPhGPRy2gOFtWnDcAsDsGY74kpZtbgE26OcWnxFP1dob5uQeK6OhrCvi4bRSkVMacpJUjS6NY+zyig0xRtfVaksaVp+aIB9rhrmLQt36g3g8yK090N3bP2PiB8WTTUe9X4SKyupN0gB5dF0ywYsWHDFKeX4VbUY4lN4r/JL/bnLg7q5jDMf8KT8I6PRquoT+9P5LcP/jr/E1vcJt1codClfqhfEdijsx5mvKblXH+bbwBqOr2MOyQbMFh+uAcDxPkCvvrkUACFvAo1DdRiHxY3Ed4qXo4PAOM06EYwfKzKmsn3JGb/GIhpRlj4A9OHbGcHencHpmEY8isf81a29sWsK0pDFXQSNeX5VVfxs8VLyu6ArelEzKY58wjTBnW1GluFvEYRG/fVVe74PBsZUtKAUCMJQRqQD0d23vMRIXCqZfgMzSILvgAWZ4FQnrMKTurRsgEh8HO1e4DjPpWBKGTShJh5fsk+yjAVEBynRE+QjYQLuKDbRBx9bQMZ0GdPr2icAx9QF1OZvMhWV6zCF1zrDYzhnCAjRYWsAJufJABRHnvxUtbrTTzDcDUcEEyWZ/U1z58vtqNioaEh3L28rvPAC08TjQVVqMaYwbGbEGvzGCpmU0wHooHLR4OgL+lu1U8YdN+FuNnHkq+OEf+F8Lfsc5O/hh0+ivwYM9kfapImU8oD6NUXixtw6rAO7rfKUykclg+xdzvlWORytOq6CWUQEPoCJ8z7b/yOd0rL5ZGH6qB2eF8aZS2pZLM8yI8JvEMzN6KA1280vKEeMDmRdL2EOUpsQtzBMSFl09GAcpXTEXPzTUVHoiGvQxfzzzlH5/MKwYDhEnd9V0vClE1E9nlGQjumAjWEvg7Nock3dU/WofaMJHaFuqlsgK6S88RwXdPm7zFvdRvHvHF/CangsuSgmgMZhdHiffeE8pfNvU6chp4iOzf7L5yNZwG4m3ZsiVEdUCYvwZ0oCzCLuIXbZNOKEnzumHfXPSGz8zeQTHmT1My64Oo56eORoNWNm9U0HlaFD9HY/U+PqCZde/oRj5OMKKQN41PsAxzwyfrobPlXxsKh8We+LvFQ2xLMnhYxTDLH3/UMFu98yg6mlQfRe5ylLMKDm5faiRZPVhFR7nreHpa/DMGBWewx8MGcesIdN9Y2SKhVFZ8ptmmhKKJDhzzO6IcPi7R6Y++/QbdKXXReag3DfJx81nMQeFIuF9/9jUp5u3x0Zf9X9HjNBVWsoDxOX1NsEfIB2w+s6Z4aOLcuPhaPb+kajPL2+PhC4jDOXOqXDgh1cPrG5NPQBdfQdwt1tdkQ+sU8kHQJcP5hFikswG/tFStN8ZNdM5P9SgriRoQL2CCl1RgHc7C3v5t75/8ESluisW4iWlum10DAM8R67Gsafr08J4FHW6WGQ9rk4rSjy1PG07vU6/9OlVw7brVBs8IFYfS08GTwjRNECJvIw2vjzy03FJ6tKOS6NkJUBMb0TCe5MITJMAMxSmnTVe3CzUbFIJxN2+hKFP07udLI1nltlH4xlQYqqvaIHDGU1JpirA8YJyTqODVFYlx6eG/im2zmxYg3+3JVaWqoFOWo51Ks7SV55vwVnP4CORVpX5SNKR9Sw62hBe7MVBVf6puiWv923JwrZUqLf0AtbqnhlrAbu61nt1ntJF34M8RaLshF85nJp54FH6COWNIXJv/Sygm0gpe9ggTfKTiBJ1VBSWZCOHwFD1ZxxwLo8wDqRzwMT1YqtDXBoviRgqTPKpsHqII/El7WKFOpGJFG4Lgm0jyX4xjbZyG3XSk6uFCaOip20T9DpJ7Gu89isJ21OOFbw2NwKzzo3Q0rix29O5sXuqVRPUg/Dz9fVsLhqbY3fFpPzzAy9S6t5inkkOUbSKd2J3LVyFG3g9UWs4A1KGRpk0b9fDOyKel/FwU+Jf5eZHEDayz7G0vFqK3nCyEjYtg49xTCQd/xxF05vh/WKGnfZyML2bNZ2FvfTE+xEuez36bc5UahA0AHV44WRXFdZXPrzXiIuu4/05vHWYZV8EP3jTs3uN6DeohJfirzol8X102jF5JL3wZWOydibihHphlkYU/5CQZ2v7/+uAF/8D&lt;/diagram&gt;&lt;/mxfile&gt;"><defs/><g><rect x="1" y="561" width="650" height="200" rx="30" ry="30" fill="#ffffff" stroke="#83d6d3" stroke-width="3" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe flex-start; justify-content: unsafe flex-start; width: 634px; height: 1px; padding-top: 568px; margin-left: 17px;"><div style="box-sizing: border-box; font-size: 0; text-align: left; "><div style="display: inline-block; font-size: 20px; font-family: Helvetica; color: #000000; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">evan.network</div></div></div></foreignObject><text x="17" y="588" fill="#000000" font-family="Helvetica" font-size="20px" font-weight="bold">evan.network</text></switch></g><rect x="241" y="623.5" width="160" height="95" rx="14.25" ry="14.25" fill="#83d6d3" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 158px; height: 1px; padding-top: 671px; margin-left: 242px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 16px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">Ethereum Blockchain</div></div></div></foreignObject><text x="321" y="676" fill="#FFFFFF" font-family="Helvetica" font-size="16px" text-anchor="middle" font-weight="bold">Ethereum Blockchain</text></switch></g><rect x="451" y="623.5" width="160" height="95" rx="14.25" ry="14.25" fill="#83d6d3" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 158px; height: 1px; padding-top: 671px; margin-left: 452px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 16px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">IPFS Network</div></div></div></foreignObject><text x="531" y="676" fill="#FFFFFF" font-family="Helvetica" font-size="16px" text-anchor="middle" font-weight="bold">IPFS Network</text></switch></g><rect x="347" y="603.5" width="40" height="20" fill="#0c3140" stroke="none" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 38px; height: 1px; padding-top: 614px; margin-left: 348px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 16px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; white-space: normal; word-wrap: normal; "><font style="font-size: 12px">RPC</font></div></div></div></foreignObject><text x="367" y="618" fill="#FFFFFF" font-family="Helvetica" font-size="16px" text-anchor="middle">RPC</text></switch></g><rect x="557" y="603.5" width="40" height="20" fill="#0c3140" stroke="none" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 38px; height: 1px; padding-top: 614px; margin-left: 558px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 16px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; white-space: normal; word-wrap: normal; "><font style="font-size: 12px">RPC</font></div></div></div></foreignObject><text x="577" y="618" fill="#FFFFFF" font-family="Helvetica" font-size="16px" text-anchor="middle">RPC</text></switch></g><path d="M 320.2 452.37 L 320.2 503 L 320.16 554.63" fill="none" stroke="#000000" stroke-miterlimit="10" stroke-dasharray="3 3" pointer-events="stroke"/><path d="M 320.2 447.12 L 323.7 454.12 L 320.2 452.37 L 316.7 454.12 Z" fill="#000000" stroke="#000000" stroke-miterlimit="10" pointer-events="all"/><path d="M 320.15 559.88 L 316.66 552.88 L 320.16 554.63 L 323.66 552.89 Z" fill="#000000" stroke="#000000" stroke-miterlimit="10" pointer-events="all"/><rect x="1" y="256" width="640" height="190" rx="28.5" ry="28.5" fill="#ffffff" stroke="#83d6d3" stroke-width="3" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe flex-start; justify-content: unsafe flex-start; width: 624px; height: 1px; padding-top: 263px; margin-left: 17px;"><div style="box-sizing: border-box; font-size: 0; text-align: left; "><div style="display: inline-block; font-size: 20px; font-family: Helvetica; color: #000000; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">blockchain API</div></div></div></foreignObject><text x="17" y="283" fill="#000000" font-family="Helvetica" font-size="20px" font-weight="bold">blockchain API</text></switch></g><rect x="36" y="299" width="100" height="58" rx="8.7" ry="8.7" fill="#b91f8d" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 98px; height: 1px; padding-top: 328px; margin-left: 37px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">Contract + Content Encryption</div></div></div></foreignObject><text x="86" y="332" fill="#FFFFFF" font-family="Helvetica" font-size="12px" text-anchor="middle" font-weight="bold">Contract + Conte...</text></switch></g><rect x="152" y="299" width="100" height="58" rx="8.7" ry="8.7" fill="#b91f8d" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 98px; height: 1px; padding-top: 328px; margin-left: 153px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">OnChain Key Management</div></div></div></foreignObject><text x="202" y="332" fill="#FFFFFF" font-family="Helvetica" font-size="12px" text-anchor="middle" font-weight="bold">OnChain Key Mana...</text></switch></g><rect x="268" y="299" width="100" height="58" rx="8.7" ry="8.7" fill="#b91f8d" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 98px; height: 1px; padding-top: 328px; margin-left: 269px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">Rights and Roles on Contracts</div></div></div></foreignObject><text x="318" y="332" fill="#FFFFFF" font-family="Helvetica" font-size="12px" text-anchor="middle" font-weight="bold">Rights and Roles...</text></switch></g><rect x="384" y="297" width="100" height="58" rx="8.7" ry="8.7" fill="#b91f8d" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 98px; height: 1px; padding-top: 326px; margin-left: 385px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">Verification Management</div></div></div></foreignObject><text x="434" y="330" fill="#FFFFFF" font-family="Helvetica" font-size="12px" text-anchor="middle" font-weight="bold">Verification Man...</text></switch></g><rect x="504" y="298" width="100" height="58" rx="8.7" ry="8.7" fill="#b91f8d" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 98px; height: 1px; padding-top: 327px; margin-left: 505px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">Profile Management</div></div></div></foreignObject><text x="554" y="331" fill="#FFFFFF" font-family="Helvetica" font-size="12px" text-anchor="middle" font-weight="bold">Profile Manageme...</text></switch></g><rect x="152" y="366" width="100" height="58" rx="8.7" ry="8.7" fill="#b91f8d" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 98px; height: 1px; padding-top: 395px; margin-left: 153px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">ENS Name Service</div></div></div></foreignObject><text x="202" y="399" fill="#FFFFFF" font-family="Helvetica" font-size="12px" text-anchor="middle" font-weight="bold">ENS Name Service</text></switch></g><rect x="268" y="366" width="100" height="58" rx="8.7" ry="8.7" fill="#b91f8d" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 98px; height: 1px; padding-top: 395px; margin-left: 269px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">IPFS File Handling</div></div></div></foreignObject><text x="318" y="399" fill="#FFFFFF" font-family="Helvetica" font-size="12px" text-anchor="middle" font-weight="bold">IPFS File Handli...</text></switch></g><rect x="387" y="366" width="100" height="58" rx="8.7" ry="8.7" fill="#b91f8d" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 98px; height: 1px; padding-top: 395px; margin-left: 388px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">Various Contract Types</div></div></div></foreignObject><text x="437" y="399" fill="#FFFFFF" font-family="Helvetica" font-size="12px" text-anchor="middle" font-weight="bold">Various Contract...</text></switch></g><rect x="504" y="366" width="100" height="58" rx="8.7" ry="8.7" fill="#b91f8d" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 98px; height: 1px; padding-top: 395px; margin-left: 505px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">DBCP</div></div></div></foreignObject><text x="554" y="399" fill="#FFFFFF" font-family="Helvetica" font-size="12px" text-anchor="middle" font-weight="bold">DBCP</text></switch></g><rect x="361" y="1" width="210" height="140" rx="21" ry="21" fill="#ffffff" stroke="#83d6d3" stroke-width="3" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe flex-start; justify-content: unsafe flex-start; width: 194px; height: 1px; padding-top: 8px; margin-left: 377px;"><div style="box-sizing: border-box; font-size: 0; text-align: left; "><div style="display: inline-block; font-size: 20px; font-family: Helvetica; color: #000000; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">Browser</div></div></div></foreignObject><text x="377" y="28" fill="#000000" font-family="Helvetica" font-size="20px" font-weight="bold">Browser</text></switch></g><rect x="51" y="1" width="210" height="140" rx="21" ry="21" fill="#ffffff" stroke="#83d6d3" stroke-width="3" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe flex-start; justify-content: unsafe flex-start; width: 194px; height: 1px; padding-top: 8px; margin-left: 67px;"><div style="box-sizing: border-box; font-size: 0; text-align: left; "><div style="display: inline-block; font-size: 20px; font-family: Helvetica; color: #000000; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">Smart Agent</div></div></div></foreignObject><text x="67" y="28" fill="#000000" font-family="Helvetica" font-size="20px" font-weight="bold">Smart Agent</text></switch></g><path d="M 460 115 L 460 185.6 L 459.89 249.25" fill="none" stroke="#000000" stroke-miterlimit="10" pointer-events="stroke"/><path d="M 459.88 254.5 L 456.39 247.5 L 459.89 249.25 L 463.39 247.51 Z" fill="#000000" stroke="#000000" stroke-miterlimit="10" pointer-events="all"/><path d="M 436.88 102.93 L 437.4 93.49 L 483.12 93.49 L 483.12 102.93 Z M 482.06 115 L 482.06 112.37 L 487.85 103.98 L 487.85 109.22 Z M 482.06 112.37 L 482.06 115 L 429 115 L 429 112.37 Z M 437.4 58.87 L 483.12 58.87 L 483.12 93.49 L 437.4 93.49 Z M 483.12 93.49 L 491 85.62 L 491 51 L 483.12 58.87 Z M 482.06 112.37 L 429 112.37 L 435.31 103.98 L 487.85 103.98 Z M 483.12 102.93 L 483.12 93.49 L 491 85.62 L 491 96.12 Z" fill="#0c3140" stroke="#ffffff" stroke-width="2" stroke-linejoin="round" stroke-miterlimit="10" pointer-events="all"/><path d="M 444.76 62.53 C 475.24 62.53 475.24 62.53 475.24 62.53 C 477.33 62.53 478.91 64.64 478.91 66.22 C 478.91 85.62 478.91 85.62 478.91 85.62 C 478.91 87.71 477.33 89.29 475.24 89.29 C 444.76 89.29 444.76 89.29 444.76 89.29 C 442.65 89.29 441.08 87.71 441.08 85.62 C 441.08 66.22 441.08 66.22 441.08 66.22 C 441.08 64.64 442.65 62.53 444.76 62.53 Z" fill="#ffffff" stroke="none" pointer-events="all"/><rect x="429" y="51" width="0" height="0" fill="none" stroke="#ffffff" stroke-width="2" pointer-events="all"/><path d="M 491 51 L 446.34 51 L 437.4 58.87 L 483.12 58.87 L 491 51 Z" fill="#0c3140" stroke="#ffffff" stroke-width="2" stroke-linejoin="round" stroke-miterlimit="10" pointer-events="all"/><path d="M 454.74 68.83 C 448.96 67.79 446.34 70.94 446.86 73.03 C 446.86 73.55 446.86 73.55 446.86 73.55 C 442.13 74.09 443.71 79.33 445.8 79.33 C 445.8 79.33 445.8 79.33 445.8 79.33 C 445.28 82.99 450.53 85.1 453.17 82.99 C 453.17 82.47 453.17 82.47 453.17 82.47 C 454.22 86.14 465.78 86.14 467.87 84.05 C 467.87 84.05 467.87 84.05 467.87 84.05 C 473.14 84.05 475.24 80.9 474.18 78.27 C 474.18 78.27 474.18 78.27 474.18 78.27 C 476.29 77.75 476.29 74.09 473.14 73.55 C 473.66 73.03 473.66 73.03 473.66 73.03 C 474.72 70.94 471.56 68.31 467.87 68.83 C 467.35 68.83 467.35 68.83 467.35 68.83 C 464.2 66.22 455.8 66.22 454.74 68.83 Z" fill="#0c3140" stroke="none" pointer-events="all"/><path d="M 147.45 115 L 147.6 185.6 L 147.56 250.39" fill="none" stroke="#000000" stroke-miterlimit="10" pointer-events="stroke"/><path d="M 147.56 255.64 L 144.06 248.64 L 147.56 250.39 L 151.06 248.64 Z" fill="#000000" stroke="#000000" stroke-miterlimit="10" pointer-events="all"/><image x="108.5" y="36.5" width="78" height="78" xlink:href="https://cdn4.iconfinder.com/data/icons/space-and-astronomy-1/800/robot-128.png" preserveAspectRatio="none"/><rect x="151" y="181" width="300" height="20" fill="none" stroke="none" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 298px; height: 1px; padding-top: 191px; margin-left: 152px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: #000000; line-height: 1.2; pointer-events: all; white-space: normal; word-wrap: normal; ">HTTPS/Secure Websocket Communication</div></div></div></foreignObject><text x="301" y="195" fill="#000000" font-family="Helvetica" font-size="12px" text-anchor="middle">HTTPS/Secure Websocket Communication</text></switch></g><rect x="42" y="623.5" width="160" height="95" rx="14.25" ry="14.25" fill="#83d6d3" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 158px; height: 1px; padding-top: 671px; margin-left: 43px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 16px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">Identity Chain</div></div></div></foreignObject><text x="122" y="676" fill="#FFFFFF" font-family="Helvetica" font-size="16px" text-anchor="middle" font-weight="bold">Identity Chain</text></switch></g><rect x="147" y="603.5" width="40" height="20" fill="#0c3140" stroke="none" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 38px; height: 1px; padding-top: 614px; margin-left: 148px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 16px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; white-space: normal; word-wrap: normal; "><font style="font-size: 12px">RPC</font></div></div></div></foreignObject><text x="167" y="618" fill="#FFFFFF" font-family="Helvetica" font-size="16px" text-anchor="middle">RPC</text></switch></g><rect x="36" y="366" width="100" height="58" rx="8.7" ry="8.7" fill="#b91f8d" stroke="#000000" pointer-events="all"/><g transform="translate(-0.5 -0.5)"><switch><foreignObject style="overflow: visible; text-align: left;" pointer-events="none" width="100%" height="100%" requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"><div xmlns="http://www.w3.org/1999/xhtml" style="display: flex; align-items: unsafe center; justify-content: unsafe center; width: 98px; height: 1px; padding-top: 395px; margin-left: 37px;"><div style="box-sizing: border-box; font-size: 0; text-align: center; "><div style="display: inline-block; font-size: 12px; font-family: Helvetica; color: #FFFFFF; line-height: 1.2; pointer-events: all; font-weight: bold; white-space: normal; word-wrap: normal; ">DID + VC</div></div></div></foreignObject><text x="86" y="399" fill="#FFFFFF" font-family="Helvetica" font-size="12px" text-anchor="middle" font-weight="bold">DID + VC</text></switch></g></g><switch><g requiredFeatures="http://www.w3.org/TR/SVG11/feature#Extensibility"/><a transform="translate(0,-5)" xlink:href="https://desk.draw.io/support/solutions/articles/16000042487" target="_blank"><text text-anchor="middle" font-size="10px" x="50%" y="100%">Viewer does not support full SVG 1.1</text></a></switch></svg>

</p>

<!---

Component details
---

[Organizations, physical assets and machines receive a digital identity (Digital Twin)](/docs/04_developers/20_api/digital-twin.html) on the evan.network blockchain.
Digital twins can be addressed through transactions by any identity, human or otherwise, and integrated in complex business logic.


[In a Business Center](/docs/02_how_it_works/business.html), users can execute transactions and exchange data with each other, with other organizations or with the Digital Twins of real machines. Hence, the evan.network provides the basis for company-wide, efficient and secure Industry 4.0 business models.

For the interaction between users, processes and machines, evan.network offers predefined services (Smart Contracts), which can be adapted to specific needs.

The interaction with Smart Contracts takes place via ÐApps in web or mobile browsers or via API from existing IT systems, IT tools and/ or machines.
For this purpose, [Smart Agents communicate with the Smart Contracts](/docs/02_how_it_works/smart-agents.html). The Smart Contracts represent the professional framework of the respective service and are developed according to the specific needs.

For example, a Smart Contract that represents a Digital Twin can include the entire life cycle of the asset and its business processes.
In concrete terms, this means that the Smart Contract itself provides a kind of management console for the various data types and manages access to the data via an encryption management and a rights-and-role model.
In the case of master data such as product properties, the actual data is stored as a JSON object encrypted with the Digital Twin keys in the storage service.

The address where the data was stored in the storage is saved in the Smart Contract. Other data are handled in a similar way, e.g. service reports. If the service technician creates a report and wants to attach for example an image of the machine, this image is loaded into the storage in encrypted form and the corresponding address is inserted into the corresponding data area of the Digital Twin.

The complete control of who may insert or read data is controlled by the owner of the Digital Twin Smart Contract, who has complete data sovereignty.

<svg version="1.1" id="evan.network" width="50%" viewBox="0 0 330 700" style="float: left; margin-right: 1em; "
   xmlns:svg="http://www.w3.org/2000/svg"  xmlns="http://www.w3.org/2000/svg"
   xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs
     id="defs4305">
    <marker id="start-data" style="stroke: #88d2d0; fill: #88d2d0;"
       viewBox="0 0 10 10" refX="10" refY="5"
       markerUnits="strokeWidth" markerWidth="4" markerHeight="3" orient="auto">
      <path d="M 0 5 L 10 10 L 10 0 z" id="path4286" />
    </marker>
    <marker id="end-data" style="stroke: #88d2d0; fill: #88d2d0;"
       viewBox="0 0 10 10" refX="0"
       refY="5"
       markerUnits="strokeWidth"
       markerWidth="4"
       markerHeight="3"
       orient="auto">
      <path
         d="M 0 0 L 10 5 L 0 10 z"
         id="path4289" />
    </marker>
    <marker
       id="start-lookup"
       style="stroke: #f7aacf; fill: #f7aacf;"
       viewBox="0 0 10 10"
       refX="10"
       refY="5"
       markerUnits="strokeWidth"
       markerWidth="4"
       markerHeight="3"
       orient="auto">
      <path
         d="M 0 5 L 10 10 L 10 0 z"
         id="path4292" />
    </marker>
    <marker
       id="end-lookup"
       style="stroke: #f7aacf; fill: #f7aacf;"
       viewBox="0 0 10 10"
       refX="0"
       refY="5"
       markerUnits="strokeWidth"
       markerWidth="4"
       markerHeight="3"
       orient="auto">
      <path
         d="M 0 0 L 10 5 L 0 10 z"
         id="path4295" />
    </marker>
    <path
       id="protocol"
       style="stroke: #f7aacf; fill: #feeaf3;"
       d="M 0 0 l 25 5 h -5 v 10 h 5 l -25 5 l -25 -5 h 5 v -10 h -5 l 25 -5" />
    <path
       id="triangle"
       style="stroke: f7aacf; fill: #f7aacf;"
       d="M 0 0 h 200 l -100 10 l -100 -10" />
    <g
       id="seal"
       transform="translate(37,60) scale(0.4)">
      <circle
         fill="#8a9ea4"
         cx="61.613"
         cy="80.894"
         r="11.266"
         id="circle4300" />
      <path
         fill="#8a9ea4"
         d="M54.675,90.979v17.018l6.938-5.005l6.939,5.005V90.978c-1.973,1.36-4.361,2.161-6.939,2.161   C59.036,93.139,56.647,92.338,54.675,90.979z"
         id="path4302" />
    </g>
  </defs>
  <style
     type="text/css"
     id="style4307">
    text        { font: 10pt &quot;PT Sans&quot;, Helvetica, Arial, sans-serif; stroke: #003946; fill: #003946; }
    text.big    { font-size: 12pt; font-weight: bold; stroke-width: 0; }
    text.small  { font-size: 8pt; }
    text.bold   { font-weight: bold; }
    text.white  { stroke: #fff; stroke-width: 1; fill: #fff; }
    text.prot   { stroke: #f7aacf; fill: #f7aacf;}
    text.code   { font: 9pt monospace; stroke: #003946; stroke-width: 0.5; fill: #003946; }
    a           { cursor: pointer; }

    .grey       { stroke: #023845; stroke-width: 1; fill: #023845; fill-opacity: 0.5; opacity: 0.5; }
    .black      { stroke: #003946; stroke-width: 3; fill: #003946; fill-opacity: 1; }
    .dark      { stroke: #003946; stroke-width: 1; fill: #003946; fill-opacity: 1; }
    .thin       { stroke: #2a4d57; stroke-width: 0.5; fill: #2a4d572; fill-opacity: 1; }
    .bw         { stroke: #003946; fill-opacity: 1; fill: #fff; }
    .region     { stroke: #aaa; stroke-dasharray: 2 1; fill-opacity: 0; }

    .dotted     { stroke-dasharray: 1 1; }
    .create     { stroke: #88d2d0; stroke-width: 4; fill-opacity: 0; marker-end: url(#end-data); }
    .create2
    {
      stroke: #88d2d0; stroke-width: 3; fill-opacity: 0;
      marker-start: url(#start-data); marker-end: url(#end-data);
    }
    .use        { stroke: #f7aacf; stroke-width: 3; fill-opacity: 0; marker-end: url(#end-lookup); }
    .use2
    {
      stroke: #f7aacf; stroke-width: 3; fill-opacity: 0; marker-end: url(#end-lookup);
      marker-start: url(#start-lookup); marker-end: url(#end-lookup);
    }
    .library    { fill: #2a4d57; stroke: #63ceca; }
    .module     { fill: #8a9ea4; stroke: #63ceca; }
    .server     { fill: #a6dddc; stroke: #003946; stroke-width: 2; }
    .service    { fill: #f7aacf; stroke: #003946; stroke-width: 2; }
    .bubble     { fill: #f7aacf; stroke: #a6dddc; stroke-width: 1; }
    .contract   { fill: #e0e6e7; stroke: #8a9ea4; stroke-width: 1; }
  </style>
  <g
     transform="translate(-40, -40)"
     id="g4482">
    <path
       class="use"
       d="M 160 80 l -10 10"
       id="path4309" />
    <path
       class="use"
       d="M 230 80 l 10 10"
       id="path4311" />
    <path
       class="use"
       d="M 150 125 l 10 10"
       id="path4313" />
    <path
       class="use"
       d="M 240 125 l -10 10"
       id="path4315" />
    <image
       xlink:href="./img/person.png"
       height="50"
       width="50"
       y="50"
       x="170" />
    <text
        transform="scale(0.75)"
        class="thin"
        x="80"
        y="180"
        >Mobile Apps</text>

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
  </g>
  <g
     transform="translate(150,560)"
     stroke="none"
     stroke-width="1"
     fill="none"
     fill-rule="evenodd"
     id="g4526">
    <g
       id="g4514"
       transform="translate(-150, 0)">
      <title
         id="title4484">Smart Agents</title>
      <a
         xlink:href="/docs/02_how_it_works/smart-agents.html"
         id="a4512">
        <rect
           class="bw dotted"
           x="30"
           width="160"
           height="140"
           id="rect4486" />
        <text
           x="70"
           y="15"
           id="text4488">Edge Server</text>
        <g
           transform="translate(0,10)"
           id="g4510">
          <text
             class="small grey"
             x="42"
             y="24"
             id="text4490" />
          <rect
             class="module"
             x="40"
             y="30"
             width="130"
             height="60"
             id="rect4492" />
          <rect
             class="module"
             x="45"
             y="45"
             width="130"
             height="60"
             id="rect4494" />
          <rect
             class="module"
             x="50"
             y="60"
             width="130"
             height="60"
             id="rect4496" />
          <text
             class="small"
             x="45"
             y="41"
             id="text4498">Machine Agent</text>
          <text
             class="small"
             x="50"
             y="56"
             id="text4500">Sensor Agent</text>
          <text
             class="small"
             x="55"
             y="71"
             id="text4502">WebService Agent</text>
          <text
             class="small thin"
             x="75"
             y="89"
             id="text4504">Connects to 3rd APIs</text>
          <text
             class="small thin"
             x="75"
             y="99"
             id="text4506">and Blockchain</text>
          <text
             class="small thin"
             x="75"
             y="109"
             id="text4508" />
        </g>
      </a>
    </g>
    <g
       class="dark"
       transform="translate(-70,-85) scale(0.3)"
       fill="#000000"
       id="g4524">
      <g
         transform="translate(138.000000, 269.000000)"
         id="g4522">
        <g
           transform="translate(12.000000, 48.000000)"
           id="g4520">
          <g
             transform="translate(89.000000, 0.000000)"
             id="g4518">
            <path
               d="M23.957115,78.5050736 L12.9126843,78.5050736 C11.9783528,78.5050736 11.2219483,77.7486691 11.2219483,76.8143376 C11.2219483,75.8800062 11.9783528,75.1236017 12.9126843,75.1236017 L23.9576971,75.1236017 C24.0346545,74.3602095 24.352665,73.649196 24.8737601,73.0916242 C25.4952152,72.426332 26.3659399,72.043832 27.2615916,72.043832 L27.2658893,72.043832 L29.6844067,72.0445903 L29.6844067,65.1673416 L5.23982022,65.1673416 C2.35087079,65.1673416 2.84218179e-14,62.8173303 2.84218179e-14,59.9283809 L2.84218179e-14,52.2517348 C2.84218179e-14,49.3627854 2.35087079,47.0119146 5.23982022,47.0119146 L29.6844734,47.0119146 C29.6844307,47.006677 29.6844067,47.0014337 29.6844067,46.9961848 L29.6844067,41.3693949 L5.23982022,41.3693949 C2.35087079,41.3693949 2.84218179e-14,39.0202433 2.84218179e-14,36.1312938 L2.84218179e-14,28.4529287 C2.84218179e-14,25.5648388 2.35087079,23.213968 5.23982022,23.213968 L29.6844067,23.213968 L29.6844067,17.1719292 C29.6844067,17.0507333 29.6971483,16.9325311 29.7213632,16.8185852 C29.6970367,16.7043901 29.6842348,16.5859156 29.6842348,16.4644331 C29.6842348,15.5301017 30.4414989,14.7736972 31.3749708,14.7736972 L56.4179764,14.7736972 C57.4425607,14.7736972 58.2754652,13.9407927 58.2754652,12.9162084 L58.2754652,5.23956236 C58.2754652,4.21411854 57.4425607,3.3820736 56.4179764,3.3820736 L5.2394764,3.3820736 C4.21575169,3.3820736 3.38198764,4.21411854 3.38198764,5.23956236 L3.38198764,12.9162084 C3.38198764,13.9407927 4.21575169,14.7736972 5.2394764,14.7736972 L23.8478865,14.7736972 C24.7813584,14.7736972 25.5386225,15.5301017 25.5386225,16.4644331 C25.5386225,17.3987646 24.7813584,18.1551691 23.8478865,18.1551691 L5.2394764,18.1551691 C2.35052697,18.1551691 -0.000343820225,15.8060174 -0.000343820225,12.9162084 L-0.000343820225,5.23956236 C-0.000343820225,2.34975337 2.35052697,-0.000257865169 5.2394764,-0.000257865169 L56.4179764,-0.000257865169 C59.3069258,-0.000257865169 61.6569371,2.34975337 61.6569371,5.23956236 L61.6569371,12.9162084 C61.6569371,15.8060174 59.3069258,18.1551691 56.4179764,18.1551691 L33.0658787,18.1551691 L33.0658787,23.213968 L56.4183202,23.213968 C59.3064101,23.213968 61.6564213,25.5648388 61.6564213,28.4529287 L61.6564213,36.1312938 C61.6564213,39.0202433 59.3064101,41.3693949 56.4183202,41.3693949 L33.0658787,41.3693949 L33.0658787,46.9961848 C33.0658787,47.0014337 33.0658547,47.006677 33.065807,47.0119146 L56.4183202,47.0119146 C59.3064101,47.0119146 61.6564213,49.3627854 61.6564213,52.2517348 L61.6564213,59.9283809 C61.6564213,62.8173303 59.3064101,65.1673416 56.4183202,65.1673416 L33.0658787,65.1673416 L33.0658787,72.0456504 L35.4909287,72.0464107 C37.2052427,72.0496255 38.6189577,73.3995242 38.7939998,75.1236017 L49.8235904,75.1236017 C50.7570624,75.1236017 51.5143264,75.8800062 51.5143264,76.8143376 C51.5143264,77.7486691 50.7570624,78.5050736 49.8235904,78.5050736 L38.7930346,78.5050736 C38.7109915,79.3044268 38.3568611,80.0614179 37.7953837,80.6221466 C37.1739287,81.2427421 36.3556365,81.5848433 35.4909287,81.5848433 L35.4857713,81.5848433 L27.2615916,81.5822646 C25.5472775,81.5790498 24.1335625,80.2291511 23.957115,78.5050736 Z M5.23982022,26.5962994 C4.21523596,26.5962994 3.38147191,27.4292039 3.38147191,28.4529287 L3.38147191,36.1312938 C3.38147191,37.1550185 4.21523596,37.987923 5.23982022,37.987923 L56.4183202,37.987923 C57.4420449,37.987923 58.2749494,37.1550185 58.2749494,36.1312938 L58.2749494,28.4529287 C58.2749494,27.4292039 57.4420449,26.5962994 56.4183202,26.5962994 L5.23982022,26.5962994 Z M5.23982022,50.3942461 C4.21523596,50.3942461 3.38147191,51.2271506 3.38147191,52.2517348 L3.38147191,59.9283809 C3.38147191,60.9521056 4.21523596,61.7858697 5.23982022,61.7858697 L56.4183202,61.7858697 C57.4420449,61.7858697 58.2749494,60.9521056 58.2749494,59.9283809 L58.2749494,52.2517348 C58.2749494,51.2271506 57.4420449,50.3942461 56.4183202,50.3942461 L5.23982022,50.3942461 Z M27.2624511,75.4261635 L27.320041,78.1406242 L35.4892096,78.2025118 C35.4892096,78.2025118 35.429041,78.1457815 35.429041,78.1449219 L35.4307601,75.4854725 L27.2624511,75.4261635 Z M35.7551545,57.7809657 L34.9342837,57.7809657 C34.0008118,57.7809657 33.2435478,57.0237017 33.2435478,56.0902298 C33.2435478,55.1558983 34.0008118,54.3986343 34.9342837,54.3986343 L35.7551545,54.3986343 C36.6886264,54.3986343 37.4458904,55.1558983 37.4458904,56.0902298 C37.4458904,57.0237017 36.6886264,57.7809657 35.7551545,57.7809657 Z M42.7305792,57.7809657 L41.9097084,57.7809657 C40.9762365,57.7809657 40.2189725,57.0237017 40.2189725,56.0902298 C40.2189725,55.1558983 40.9762365,54.3986343 41.9097084,54.3986343 L42.7305792,54.3986343 C43.6640511,54.3986343 44.4213152,55.1558983 44.4213152,56.0902298 C44.4213152,57.0237017 43.6640511,57.7809657 42.7305792,57.7809657 Z M35.7551545,33.9830191 L34.9342837,33.9830191 C34.0008118,33.9830191 33.2435478,33.2257551 33.2435478,32.2922831 C33.2435478,31.3579517 34.0008118,30.6006876 34.9342837,30.6006876 L35.7551545,30.6006876 C36.6886264,30.6006876 37.4458904,31.3579517 37.4458904,32.2922831 C37.4458904,33.2257551 36.6886264,33.9830191 35.7551545,33.9830191 Z M42.7305792,33.9830191 L41.9097084,33.9830191 C40.9762365,33.9830191 40.2189725,33.2257551 40.2189725,32.2922831 C40.2189725,31.3579517 40.9762365,30.6006876 41.9097084,30.6006876 L42.7305792,30.6006876 C43.6640511,30.6006876 44.4213152,31.3579517 44.4213152,32.2922831 C44.4213152,33.2257551 43.6640511,33.9830191 42.7305792,33.9830191 Z M35.7551545,10.7684494 L34.9342837,10.7684494 C34.0008118,10.7684494 33.2435478,10.0111854 33.2435478,9.07771348 C33.2435478,8.14338202 34.0008118,7.38611798 34.9342837,7.38611798 L35.7551545,7.38611798 C36.6886264,7.38611798 37.4458904,8.14338202 37.4458904,9.07771348 C37.4458904,10.0111854 36.6886264,10.7684494 35.7551545,10.7684494 Z M42.7305792,10.7684494 L41.9097084,10.7684494 C40.9762365,10.7684494 40.2189725,10.0111854 40.2189725,9.07771348 C40.2189725,8.14338202 40.9762365,7.38611798 41.9097084,7.38611798 L42.7305792,7.38611798 C43.6640511,7.38611798 44.4213152,8.14338202 44.4213152,9.07771348 C44.4213152,10.0111854 43.6640511,10.7684494 42.7305792,10.7684494 Z M49.8546202,57.7809657 L49.0337494,57.7809657 C48.1002775,57.7809657 47.343873,57.0237017 47.343873,56.0902298 C47.343873,55.1558983 48.1002775,54.3986343 49.0337494,54.3986343 L49.8546202,54.3986343 C50.7880921,54.3986343 51.5453562,55.1558983 51.5453562,56.0902298 C51.5453562,57.0237017 50.7880921,57.7809657 49.8546202,57.7809657 Z M49.8546202,33.9830191 L49.0337494,33.9830191 C48.1002775,33.9830191 47.343873,33.2257551 47.343873,32.2922831 C47.343873,31.3579517 48.1002775,30.6006876 49.0337494,30.6006876 L49.8546202,30.6006876 C50.7880921,30.6006876 51.5453562,31.3579517 51.5453562,32.2922831 C51.5453562,33.2257551 50.7880921,33.9830191 49.8546202,33.9830191 Z M49.8546202,10.7684494 L49.0337494,10.7684494 C48.1002775,10.7684494 47.343873,10.0111854 47.343873,9.07771348 C47.343873,8.14338202 48.1002775,7.38611798 49.0337494,7.38611798 L49.8546202,7.38611798 C50.7880921,7.38611798 51.5453562,8.14338202 51.5453562,9.07771348 C51.5453562,10.0111854 50.7880921,10.7684494 49.8546202,10.7684494 Z M9.83514944,57.7809657 L9.01427865,57.7809657 C8.07994719,57.7809657 7.3235427,57.0237017 7.3235427,56.0902298 C7.3235427,55.1558983 8.07994719,54.3986343 9.01427865,54.3986343 L9.83514944,54.3986343 C10.7694809,54.3986343 11.5258854,55.1558983 11.5258854,56.0902298 C11.5258854,57.0237017 10.7694809,57.7809657 9.83514944,57.7809657 Z M16.8106601,57.7809657 L15.9897893,57.7809657 C15.0554579,57.7809657 14.2990534,57.0237017 14.2990534,56.0902298 C14.2990534,55.1558983 15.0554579,54.3986343 15.9897893,54.3986343 L16.8106601,54.3986343 C17.7449916,54.3986343 18.5013961,55.1558983 18.5013961,56.0902298 C18.5013961,57.0237017 17.7449916,57.7809657 16.8106601,57.7809657 Z M9.83514944,33.9830191 L9.01427865,33.9830191 C8.07994719,33.9830191 7.3235427,33.2257551 7.3235427,32.2922831 C7.3235427,31.3579517 8.07994719,30.6006876 9.01427865,30.6006876 L9.83514944,30.6006876 C10.7694809,30.6006876 11.5258854,31.3579517 11.5258854,32.2922831 C11.5258854,33.2257551 10.7694809,33.9830191 9.83514944,33.9830191 Z M16.8106601,33.9830191 L15.9897893,33.9830191 C15.0554579,33.9830191 14.2990534,33.2257551 14.2990534,32.2922831 C14.2990534,31.3579517 15.0554579,30.6006876 15.9897893,30.6006876 L16.8106601,30.6006876 C17.7449916,30.6006876 18.5013961,31.3579517 18.5013961,32.2922831 C18.5013961,33.2257551 17.7449916,33.9830191 16.8106601,33.9830191 Z M9.83514944,10.7684494 L9.01427865,10.7684494 C8.07994719,10.7684494 7.3235427,10.0111854 7.3235427,9.07771348 C7.3235427,8.14338202 8.07994719,7.38611798 9.01427865,7.38611798 L9.83514944,7.38611798 C10.7694809,7.38611798 11.5258854,8.14338202 11.5258854,9.07771348 C11.5258854,10.0111854 10.7694809,10.7684494 9.83514944,10.7684494 Z M16.8106601,10.7684494 L15.9897893,10.7684494 C15.0554579,10.7684494 14.2990534,10.0111854 14.2990534,9.07771348 C14.2990534,8.14338202 15.0554579,7.38611798 15.9897893,7.38611798 L16.8106601,7.38611798 C17.7449916,7.38611798 18.5013961,8.14338202 18.5013961,9.07771348 C18.5013961,10.0111854 17.7449916,10.7684494 16.8106601,10.7684494 Z"
               id="path4516" />
          </g>
        </g>
      </g>
    </g>
  </g>
  <image
     xlink:href="./img/machine.png"
     height="50"
     width="50"
     y="550"
     x="240" />
  <g
     transform="translate(280,600) scale(2)"
     id="g4548">
    <g
       id="g4534">
      <path
         d="M18.772,23.356c-0.172,0-0.338-0.089-0.43-0.244l-0.723-1.215c-0.218,0.005-0.432-0.005-0.65-0.029    c-0.222-0.025-0.433-0.063-0.638-0.112l-0.97,1.029c-0.164,0.174-0.427,0.209-0.629,0.081l-1.36-0.849    c-0.202-0.126-0.287-0.377-0.203-0.6l0.498-1.323c-0.277-0.333-0.51-0.699-0.693-1.095l-1.408-0.117    c-0.237-0.02-0.429-0.204-0.456-0.44l-0.185-1.593c-0.027-0.237,0.116-0.46,0.344-0.533l1.348-0.436    c0.086-0.428,0.228-0.838,0.421-1.225l-0.787-1.174c-0.133-0.197-0.107-0.462,0.061-0.631l1.131-1.138    c0.169-0.17,0.432-0.195,0.631-0.064l1.179,0.78c0.389-0.198,0.798-0.343,1.222-0.432L16.9,10.65    c0.072-0.228,0.283-0.375,0.531-0.347l1.594,0.175c0.236,0.026,0.422,0.216,0.443,0.453l0.125,1.408    c0.396,0.18,0.765,0.409,1.101,0.686l1.318-0.507c0.223-0.085,0.476-0.002,0.603,0.199l0.857,1.355    c0.127,0.202,0.095,0.465-0.078,0.63l-1.022,0.975c0.106,0.421,0.156,0.852,0.148,1.287l1.22,0.716    c0.206,0.121,0.298,0.37,0.22,0.596l-0.526,1.517c-0.078,0.225-0.307,0.362-0.54,0.331l-1.399-0.191    c-0.264,0.345-0.569,0.652-0.914,0.92l0.2,1.398c0.033,0.236-0.104,0.463-0.329,0.543l-1.513,0.534    C18.883,23.348,18.828,23.356,18.772,23.356z M17.895,20.883c0.176,0,0.339,0.092,0.43,0.244l0.667,1.121l0.74-0.261l-0.186-1.291    c-0.027-0.189,0.056-0.378,0.214-0.484c0.427-0.29,0.803-0.668,1.086-1.093c0.106-0.159,0.294-0.243,0.483-0.218l1.293,0.177    l0.258-0.742l-1.128-0.661c-0.166-0.098-0.261-0.281-0.245-0.473c0.042-0.519-0.017-1.032-0.175-1.524    c-0.06-0.183-0.008-0.383,0.131-0.516l0.944-0.9L21.989,13.6l-1.218,0.468c-0.181,0.067-0.381,0.028-0.521-0.102    c-0.38-0.354-0.818-0.628-1.304-0.812c-0.18-0.068-0.305-0.232-0.321-0.424l-0.116-1.303l-0.778-0.085l-0.395,1.245    c-0.058,0.184-0.216,0.317-0.405,0.345c-0.511,0.073-0.998,0.245-1.448,0.511c-0.164,0.096-0.371,0.092-0.529-0.014l-1.09-0.721    l-0.554,0.557l0.728,1.084c0.107,0.159,0.113,0.365,0.017,0.53c-0.26,0.445-0.429,0.934-0.5,1.452    c-0.026,0.19-0.159,0.349-0.342,0.407l-1.245,0.402l0.09,0.778l1.301,0.107c0.19,0.016,0.355,0.139,0.425,0.316    c0.19,0.488,0.467,0.926,0.822,1.301c0.132,0.139,0.173,0.341,0.105,0.52l-0.46,1.223l0.665,0.415l0.896-0.952    c0.133-0.14,0.331-0.19,0.517-0.134c0.239,0.076,0.485,0.128,0.754,0.158c0.261,0.029,0.52,0.03,0.772,0.011    C17.868,20.884,17.881,20.883,17.895,20.883z"
         id="path4530" />
      <path
         d="M17.455,19.143c-1.276,0-2.314-1.038-2.314-2.314c0-1.275,1.038-2.313,2.314-2.313c1.275,0,2.313,1.038,2.313,2.313    C19.768,18.104,18.73,19.143,17.455,19.143z M17.455,15.515c-0.725,0-1.314,0.589-1.314,1.313s0.59,1.314,1.314,1.314    s1.313-0.59,1.313-1.314S18.179,15.515,17.455,15.515z"
         id="path4532" />
    </g>
    <g
       id="g4540">
      <path
         d="M7.16,18.754c-0.172,0-0.337-0.089-0.43-0.244l-0.64-1.074c-0.198,0.008-0.378-0.007-0.566-0.027    c-0.19-0.021-0.375-0.053-0.556-0.096l-0.857,0.91c-0.164,0.174-0.427,0.207-0.629,0.082l-1.23-0.767    c-0.202-0.127-0.287-0.378-0.203-0.601l0.44-1.171c-0.24-0.292-0.442-0.611-0.604-0.954l-1.246-0.104    c-0.237-0.02-0.429-0.204-0.456-0.44l-0.167-1.44c-0.027-0.237,0.116-0.46,0.344-0.533l1.191-0.385    c0.078-0.372,0.201-0.729,0.367-1.066L1.222,9.805C1.089,9.607,1.115,9.343,1.283,9.174l1.022-1.029    c0.169-0.17,0.431-0.195,0.631-0.064l1.043,0.691c0.339-0.171,0.695-0.297,1.064-0.377L5.42,7.203    c0.071-0.227,0.281-0.371,0.531-0.347l1.441,0.157c0.236,0.025,0.422,0.216,0.443,0.453l0.111,1.247    c0.343,0.157,0.663,0.357,0.957,0.597l1.167-0.449c0.221-0.083,0.475-0.002,0.603,0.199l0.775,1.227    c0.127,0.202,0.095,0.465-0.078,0.63l-0.903,0.861c0.09,0.367,0.133,0.742,0.129,1.122l1.078,0.633    c0.206,0.121,0.298,0.37,0.22,0.596L11.419,15.5c-0.078,0.226-0.298,0.362-0.541,0.331l-1.237-0.17    c-0.23,0.299-0.497,0.567-0.797,0.802L9.022,17.7c0.033,0.236-0.104,0.464-0.329,0.543l-1.367,0.482    C7.271,18.745,7.215,18.754,7.16,18.754z M6.366,16.422c0.175,0,0.339,0.092,0.43,0.244l0.584,0.98l0.595-0.21l-0.162-1.129    c-0.027-0.189,0.056-0.378,0.214-0.484c0.388-0.264,0.713-0.591,0.969-0.975c0.106-0.159,0.296-0.242,0.483-0.218l1.131,0.154    l0.207-0.597L9.831,13.61c-0.166-0.098-0.261-0.281-0.245-0.473c0.037-0.463-0.016-0.921-0.156-1.36    c-0.06-0.183-0.008-0.383,0.131-0.516l0.825-0.786l-0.337-0.533l-1.064,0.409c-0.179,0.068-0.381,0.029-0.521-0.102    C8.123,9.933,7.732,9.689,7.299,9.525c-0.179-0.068-0.303-0.232-0.32-0.423l-0.103-1.14L6.251,7.895L5.906,8.983    C5.848,9.167,5.691,9.301,5.501,9.328C5.044,9.394,4.61,9.547,4.209,9.784C4.043,9.881,3.836,9.877,3.679,9.77l-0.953-0.63    L2.281,9.588l0.636,0.948c0.106,0.158,0.113,0.364,0.017,0.53c-0.231,0.397-0.382,0.834-0.446,1.296    c-0.026,0.189-0.159,0.348-0.342,0.406L1.057,13.12l0.072,0.626l1.138,0.094c0.19,0.016,0.356,0.139,0.426,0.317    c0.167,0.434,0.414,0.823,0.732,1.16c0.132,0.139,0.173,0.341,0.105,0.52l-0.402,1.068l0.535,0.334l0.783-0.832    c0.133-0.14,0.333-0.19,0.516-0.134c0.217,0.069,0.438,0.115,0.673,0.141c0.235,0.027,0.463,0.027,0.688,0.01    C6.338,16.423,6.352,16.422,6.366,16.422z"
         id="path4536" />
      <path
         d="M5.968,14.944c-1.181,0-2.141-0.96-2.141-2.141s0.96-2.141,2.141-2.141c1.18,0,2.14,0.96,2.14,2.141    S7.148,14.944,5.968,14.944z M5.968,11.663c-0.629,0-1.141,0.512-1.141,1.141s0.512,1.141,1.141,1.141    c0.628,0,1.14-0.512,1.14-1.141S6.596,11.663,5.968,11.663z"
         id="path4538" />
    </g>
    <g
       id="g4546">
      <path
         d="M15.468,10.644c-0.172,0-0.337-0.089-0.43-0.244l-0.503-0.845c-0.001,0-0.002,0-0.003,0c-0.14,0-0.281-0.008-0.424-0.023    s-0.283-0.039-0.421-0.07l-0.674,0.717c-0.164,0.174-0.427,0.209-0.629,0.081L11.37,9.626c-0.202-0.126-0.287-0.377-0.203-0.601    l0.347-0.919c-0.179-0.223-0.332-0.464-0.457-0.722l-0.979-0.081C9.84,7.284,9.649,7.1,9.622,6.863L9.484,5.674    C9.457,5.436,9.6,5.214,9.828,5.141l0.936-0.303c0.063-0.279,0.155-0.549,0.278-0.806l-0.548-0.816    c-0.133-0.197-0.107-0.462,0.061-0.631l0.845-0.85c0.168-0.17,0.431-0.194,0.631-0.064l0.819,0.542    c0.258-0.125,0.526-0.22,0.804-0.284l0.297-0.937c0.072-0.226,0.283-0.371,0.531-0.346l1.19,0.13    c0.236,0.026,0.422,0.216,0.443,0.453l0.087,0.979c0.258,0.123,0.5,0.273,0.725,0.451l0.916-0.353    c0.224-0.086,0.476-0.002,0.603,0.199l0.64,1.012c0.127,0.202,0.095,0.465-0.078,0.63l-0.71,0.677    c0.064,0.279,0.098,0.563,0.098,0.849l0.848,0.497c0.206,0.121,0.298,0.37,0.22,0.596l-0.393,1.132    c-0.077,0.225-0.295,0.363-0.541,0.331l-0.973-0.133c-0.177,0.224-0.378,0.426-0.602,0.605l0.139,0.974    c0.033,0.235-0.104,0.463-0.329,0.542l-1.129,0.398C15.58,10.636,15.524,10.644,15.468,10.644z M14.813,8.544    c0.175,0,0.339,0.092,0.43,0.244l0.445,0.749l0.356-0.126l-0.123-0.862c-0.026-0.188,0.056-0.376,0.214-0.483    c0.31-0.211,0.571-0.474,0.776-0.782c0.106-0.16,0.287-0.245,0.484-0.218l0.862,0.118l0.124-0.357l-0.753-0.441    c-0.166-0.098-0.262-0.281-0.245-0.474c0.03-0.368-0.012-0.734-0.125-1.088C17.2,4.641,17.252,4.44,17.39,4.308l0.63-0.601    l-0.201-0.319L17.006,3.7c-0.179,0.068-0.38,0.029-0.521-0.102c-0.271-0.254-0.585-0.449-0.932-0.58    c-0.18-0.068-0.305-0.232-0.321-0.424l-0.077-0.869L14.78,1.685l-0.264,0.832C14.459,2.699,14.3,2.833,14.111,2.86    c-0.365,0.052-0.713,0.175-1.034,0.365c-0.166,0.096-0.371,0.093-0.531-0.014L11.819,2.73l-0.267,0.269l0.485,0.724    c0.106,0.158,0.113,0.364,0.017,0.53c-0.186,0.319-0.306,0.668-0.357,1.037c-0.026,0.19-0.159,0.349-0.342,0.407l-0.83,0.269    l0.043,0.375l0.868,0.072c0.191,0.016,0.356,0.139,0.425,0.317c0.135,0.347,0.332,0.659,0.588,0.928    C12.581,7.798,12.622,8,12.554,8.18l-0.308,0.815l0.32,0.199l0.598-0.635c0.133-0.14,0.335-0.191,0.515-0.134    c0.174,0.055,0.353,0.092,0.54,0.112c0.187,0.021,0.372,0.021,0.553,0.008C14.786,8.545,14.799,8.544,14.813,8.544z"
         id="path4542" />
      <path
         d="M14.485,7.498c-1.022,0-1.854-0.832-1.854-1.854s0.832-1.854,1.854-1.854s1.854,0.832,1.854,1.854    S15.507,7.498,14.485,7.498z M14.485,4.789c-0.471,0-0.854,0.384-0.854,0.854s0.384,0.854,0.854,0.854    c0.471,0,0.854-0.384,0.854-0.854S14.956,4.789,14.485,4.789z"
         id="path4544" />
    </g>
  </g>
  <g
     transform="translate(240,650) scale(0.5)"
     id="g4552">
    <path
       data-name="Compound Path"
       d="M88,55.6V34.5a13,13,0,0,0-13-13H66.9V14c0-5.6-8.5-8-16.9-8S33.1,8.5,33.1,14v7.5H25a13,13,0,0,0-13,13V55.6C8.4,56.9,6,59,6,62V86c0,5.6,8.5,8,16.9,8s16.9-2.5,16.9-8V78.5H60.1V86c0,5.6,8.5,8,16.9,8S94,91.5,94,86V62C94,59,91.6,56.9,88,55.6Zm0,17.8c-.9.9-4.8,2.4-10.9,2.4S67,74.3,66.1,73.4V68.3A32.9,32.9,0,0,0,77.1,70,32.9,32.9,0,0,0,88,68.3ZM77.1,64c-5.4,0-9.1-1.2-10.5-2,1.4-.9,5.1-2,10.5-2s9.1,1.2,10.5,2C86.1,62.9,82.5,64,77.1,64ZM60.9,25.5c-.9.9-4.8,2.4-10.9,2.4s-10.1-1.5-10.9-2.4V20.4A32.9,32.9,0,0,0,50,22.1a32.9,32.9,0,0,0,10.9-1.7ZM39.1,32.2A32.9,32.9,0,0,0,50,33.9a32.9,32.9,0,0,0,10.9-1.7v5.5c-.9.9-4.8,2.4-10.9,2.4s-10-1.5-10.9-2.4ZM50,12c5.4,0,9.1,1.2,10.5,2-1.4.9-5.1,2-10.5,2s-9.1-1.2-10.5-2C40.9,13.2,44.6,12,50,12ZM18,34.5a7,7,0,0,1,7-7h8.1V38c0,5.6,8.5,8,16.9,8s16.9-2.5,16.9-8V27.5H75a7,7,0,0,1,7,7V54.2a40.4,40.4,0,0,0-4.9-.3c-8.4,0-16.9,2.5-16.9,8V72.5H39.9V62c0-5.6-8.5-8-16.9-8a40.4,40.4,0,0,0-4.9.3ZM12,68.3A32.9,32.9,0,0,0,22.9,70a32.9,32.9,0,0,0,10.9-1.7v5.1c-.9.9-4.8,2.4-10.9,2.4S12.9,74.3,12,73.4Zm10.9-8.4c5.4,0,9.1,1.2,10.5,2-1.4.9-5.1,2-10.5,2s-9.1-1.2-10.5-2C13.9,61.1,17.5,59.9,22.9,59.9Zm0,28.1c-6.2,0-10-1.5-10.9-2.4V80.1a32.9,32.9,0,0,0,10.9,1.7,32.9,32.9,0,0,0,10.9-1.7v5.5C33,86.5,29.1,88,22.9,88Zm54.1,0c-6.2,0-10-1.5-10.9-2.4V80.1a32.9,32.9,0,0,0,10.9,1.7A32.9,32.9,0,0,0,88,80.1v5.5C87.1,86.5,83.2,88,77.1,88Z"
       id="path4550" />
  </g>
  <path
     class="use2"
     d="M 110 545 v -20"
     id="path4554" />
  <path
     class="use2"
     d="M 200 650 l 10 10"
     id="path4556" />
  <path
     class="use2"
     d="M 202 630 h 14"
     id="path4558" />
  <path
     class="use2"
     d="M 200 610 l 10 -10"
     id="path4560" />
</svg>


## Business Center
In Business Centers, organizations, users and machines are interconnected with each other in order to interact as partners in a concrete business environment. Network partners who join a Business Center expand their profile with specific information and features for this business environment. In addition to extended descriptive information, the profile may also contain certificates, competencies and general skills.
The Business Center is an Ethereum-based development framework and provides specific Smart Contracts for initiating, entering into and implementing business relationships. The entire cooperation between network partners via Smart Contracts within a Business Center takes place directly, i.e. without a central intermediary, and is encrypted, i.e. secure against access by unauthorized third parties.

Depending on the requirements for business relationships, Business Centers are either public, closed, or restricted.


**Public Business Centers** are publicly available and can be found by all users. Any user can join a public Business Center.

**Private Business Centers**, on the other hand, are hidden. Only on explicit invitation of a Business Center administrator, users can join.

**Restricted Business Centers** are publicly listed. Users can submit a request to participate, but this must be approved by an administrator of the Business Center.

Users of evan.network are not obliged to use the Business Center structure of evan.network. You can create and run your own Ethereum-based Smart Contract developments on evan.network, but using the Business Center structure makes it much easier.

To map different business relationships, evan.network offers different Smart Contract templates, which are enriched in a Business Center with the specific logic required there. Creating concrete Smart Contracts for a business relationship and initializing them with the digital identities of the users involved is a complex process.
This is greatly simplified by the use of a Smart Contract factory. The factory manages all Business Center-specific Smart Contract templates, creates a configured instance of the Smart Contract and initializes this with the network partners authorized to the contract. From this point on, a direct business relationship is established between the network partners involved, which is only visible and executable for them.


Smart Contracts were developed with the goal of easy use and expansion. Each Smart Contract can be called directly from a Web3 browser using for example a name server entry. Initially, only the manifest file ([DBCP](/docs/04_developers/dbcp.html)) is referenced and loaded. This file contains a standardized structure with descriptive information to make the service human and machine readable. It also contains references to the actual Smart Contract in the blockchain and the Distributed App (ÐApp), which enables direct user interaction with the service.
In order to ensure interoperability of services, the manifest file corresponds to a standardized structure that is currently provided as an open source component (DBCP) as part of a project sponsored by the Thuringian Ministry of Economics, Science and Digital Society. This makes it possible to start an interaction with the services even without the evan.network framework.

This architecture enables the integration of any third-party Smart Contracts into an evan.network environment. Referenced via the manifest file existing Smart Contracts of other providers can be combined with evan.network-ÐApps and thus integrated into a homogeneous user experience.
Based on this architectural principle, the entire network was created. Thus, all applications the user communicates with in the evan.network, processes Smart Contracts with and makes transactions with are implemented as ÐApp.

## Security
The core technology of the evan.network is based on the Ethereum blockchain technology. The protection of transactions against manipulation is an essential element of this technology. This requires that the contents of the Smart Contracts can be read, interpreted and verified by all network partners (e.g. AuthorityNodes) in the blockchain, which represents a significant hurdle in the B2B adaptation of blockchain technology.

The evan.network therefore implements a hybrid storage concept that offers transaction and data security at the same time. All user data are encrypted (AES 256bit/CBC), stored in a distributed file system (IPFS) belonging to the network and referenced from the Smart Contract. This ensures that the actual content is only visible and usable for third parties, if they are invited into a contract and thus have an authorization for the respective data.


Each user receives a public and a private key at his or her first registration. These keys are used to establish communication (Diffie Hellman) with other users and Smart Contracts.

For the interaction within a specific business relationship, additional key pairs (public / private) are created, which only apply to the specific business relationship and the Smart Contract used there. This means that Smart Contracts and the contract contents can be assigned with access rights very flexible. This makes it possible, for example, to determine which parts of a Smart Contract a network partner may read or edit.

In addition, references and keys for data stored outside the blockchain can be stored within the Smart Contract. For example, cloud storage or IoT data streams can be referenced and access to them securely managed.

## Smart Contracts

evan.network supports Smart Contracts that are compatible with Ethereum technology (EVM). For the simple creation of specific business relationships, evan.network offers various basic Smart Contracts that make it easier for developers to implement business applications. These Smart Contracts offer functionalities such as rights and role management at business logic and data level, upgradeability, versioning and data encryption.
Business Center or application-specific characteristics can be derived from these basis Smart Contracts, for example:

- **Capa Contract** - Easy management of requests for available capacities for a specific requirement within the Business Center. Capacity requests are sent to users known by name or all users who meet certain profile criteria and can be answered automatically or via Capa-ÐApp. One or more relevant offers can be selected from the answers and an order in the form of a Business Contract can be concluded with the corresponding network partners.
Inquiries for services or rentals can also be defined and answered via Capa Contracts.

- **Business Contract** - A Business Contract defines a specific business transaction between two or more network partners and is comparable to a classic contract or order. It does not matter whether the Business Contract is closed directly or as a result of a previous Capa Contract request. Business Contracts can describe on-off and recurring orders. In addition to the contract conditions, a Business Contract can also contain almost any user data required for contract performance (access data, CAD data, etc.) or arising during contract performance (e.g. log data, production progress, performance reports, etc.).

- **Digital Twin Contract** - The Digital Twin Contract represents a real good in the blockchain, gives it an identity and enables it to securely exchange transactions and data with other users or goods. In a Digital Twin, real goods (e.g. machines, components etc.) but also concrete orders (e.g. logistics) can be provided with a digital identity. Via the Digital Twin Contract, data can be securely stored and, if required, specifically released to third parties. The Digital Twin can enter into contractual relationships with other users as well as with other Digital Twins, for example to allocate capacities of service technicians (capa contract). These are then ordered via the Business Contract. The Digital Twin stores and manages information about the real goods it represents, permanently and tamper-proof.

To ensure updateability and to solve the backward compatibility of derived Smart Contracts, each derived Smart Contract receives a fixed assignment to a ÐApp and a technical description of its structure (DBCP). This ensures that a Smart Contract can always be operated by network partners, even if technologies change or new versions of the Smart Contract are created.

## Account Management

To interact in evan.network, users, organizations or machines need an account. The account for real users is created during onboarding at the first login. A user profile is created with his public and private key, as well as an address book and a mailbox. The relationships of an user with other users are stored in the address book by storing the public keys of the accounts of the respective network partners required to decrypt the communication. In the mailbox of an account, notifications of invitations to this account are stored in contracts of other accounts.

Real users can be grouped into organizations to appear under their identity. This is used to map the relationship of users in a real organization. This allows contracts to be concluded between organizations, which then have to be served or signed by one or more real users.

Within a Business Center, the information in the profiles of the user and organization accounts is extended by subject-specific data. This makes it easy to find users and organizations within the Business Center and to initiate business. This specific profile information can be entered directly when a user or organization is admitted to the Business Center or collected automatically while working in the Business Center. An example of an automated date is the calculated delivery on time (key figure: delivery reliability) based on the completed business relationships.


## Interaction with Smart Contracts and Business Centers

The interaction capabilities in a Business Center should enable simple interaction between end users, IT systems and machines. Starting from today's mostly manual forms of communication, an automation of cross-company cooperation can be implemented step by step.

To interact as user or machine in evan.network, a network account is required. An account can be created directly via onboarding (self-service) or via an invitation. An invitation is sent by an existing user or Smart Contract on the network. In the invitation, you can control whether a user is invited directly to a Business Center or to a specific Smart Contract. In addition, EVEs can be sent directly to the invited user as part of the invitation process, so that the new user is immediately ready to work in the network. The invitation is sent either as a technical invitation via an API or by an user using an e-mail address. The invitation email contains an invitation text and a link to the onboarding ÐApp. This ÐApp guides the new user through the registration process, where he or she has to confirm e.g. terms and conditions and data protection and gets an own account with private key and Mnemonic. After successful registration, the user has an evan.network identity with which he or she can now participate in the Business Center and Smart Contract.

Every interaction with Business Centers and Smart Contracts takes place via ÐApps. Users interact with the respective ÐApp via web or mobile browsers. ÐApps are HTML applications loaded from the blockchain and make it easy for the user to work with Smart Contracts and evan.network interactively.

To communicate with Smart Contracts from your own applications and ÐApps, evan.network provides APIs in form of a JavaScript library and developer documentation. Thus, own applications can be implemented and operated on evan.network.

For an automation of the business relations, evan.network offers APIs to all Smart Contracts. Hence, the evan.network can be connected to own systems and a direct integration of business processes can be carried out. Furthermore, it is possible to add logic and workflow addons in the evan.network with the help of [Smart Agents](/docs/02_how_it_works/smart-agents.html). They are operated by the respective Smart Agent provider and can enable workflow-supported communication of the evan.network with existing IT systems and machines. Smart Agents can be invited into a Smart Contract, just like users, and thus receive access to its contents. The Smart Agent constantly checks the contract for changes and can automatically initiate new processes according to predefined rules as soon as it finds one.
If the user has the rights, he or she can also add content to the Smart Contract. Via Smart Agents, the invitation via email or the mobile push notifications are solved in the evan.network. They combine the "blockchain world" with other technologies.

## Scalability
A big challenge to blockchain technology is the number of possible parallel transactions. There is still no final solution for realistically achieving almost infinite scalability within a blockchain. To counter this fact the evan.network is structured in such a way that the organization and technology of the AuthorityNodes make it possible to launch specialized or use case specific SideChains at any time. These are also subject to DAO governance but, depending on your setup, configuration and rules, allow you to perform specified use cases in much higher volumes. The technologies and services used in evan.network such as the name service or DBCP descriptions make it easier for users and developers to interact seamlessly with their contracts and ÐApps regardless of this technical separation.

-->
