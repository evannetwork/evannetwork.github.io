---
title: "Hello World ÐApp"
---
# Hello World ÐApp

## 1. Get Tutorial Application
- [Download Tutorial Application](https://github.com/evannetwork/contractus-dapps-tutorial)

## 2. ÐApp Wrapper application
The downloaded folder "contractus-dapps-tutorial" looks like this on the top level.

[![contractus-dapps-tutorial - directory](/public/dapps/hello-world/contractus-dapps-tutorial-dir-structure.png){:width="150px"}](/public/dapps/hello-world/contractus-dapps-tutorial-dir-structure.png)

In order to be able to work in ordered and staked projects, it is necessary to split the project into several projects (e.g. dashboard-dapp, list-dapp, contract1-dapp, contract2-dapp) after a short time. To anticipate this problem and different building jobs, each project uses a [lerna](https://github.com/lerna/lerna) project structure to handle multiple repositories as easily as possible. The lerna project only includes the basic requirements and build jobs for the sub projects. The build jobs are definied within the [contractus dapp-gulp project](/angular/dapp-gulp).

## 3. Build, serve and start the application
Navigate into the lerna project and run the following commands. The same documentation is also included into the lerna projects readme itself.

### 3.1 Install
```bash
npm install -g lerna
npm install
lerna bootstrap --hoist
npm link contractus-core-link
```

### 3.2 Basic Development
- build all included dapps
```bash
npm run dapps-build
```

- watch for changes and rebuild dapps
```bash
npm run dapps-serve
```

- build and watch
 ```bash
npm run serve
```

- build and serve the local dapp serve, starts an local server at http://localhost:3000
```bash
npm run serve-standalone
```

## 4. The ÐApp structure
In the DApp folder of each lerna project are the individual DApps. You will find different projects for the different stages of the tutorial. In the first step we will focus on the hello-word project to explain the basics.

By watching into this repository you will find a project structure like the following:
- dbcp.json
- package.json
- README.MD
- src
  - components
    - hello-world
      - hello-world.html
      - hello-world.scss
      - hello-world.ts
    - root
      - root.html
      - root.scss
      - root.ts
  - i18n
    - de.ts
    - en.ts
    - registry.ts
  - index.ts
  - services
    - helloworld.service.ts
- tsconfig.json
- tslint.json
- VERSIONS.md

At the root directory you will find the usal nodejs files, like the readme.md, versions.md or package.json. One file, the dbcp.json, is used to handle the dbcp definition of the application. With this file, you can specify general metadata about the application and "documentation", how the application works. The contractus dapp application loader will look into this file first, to specify wich files and dependencies should be loaded. With the same logic, using the module property, the angular-core library will know, which module should be loaded during angular setup. 

Against usal metadata that can be declared within this file, contract abi definitions or a data schema can be defined too. So the application can define its contract and data usage by itself.
It looks like the following.

```json
{
  "public": {
    "autor": "contractus",
    "dapp": {
      "dependencies": {
        "angular-core": "0.9.0",
        "angular-libs": "0.9.0"
      },
      "entrypoint": "helloword.js",
      "files": [
        "helloword.js",
        "helloword.css"
      ],
      "module": "HelloWorldModule",
      "primaryColor": "#004f7d",
      "secondaryColor": "#f9f9ff",
      "standalone": true,
      "type": "dapp"
    },
    "description": "Hello World.",
    "i18n": {
      "description": {
        "de": "Hello World",
        "en": "Hello World"
      },
      "name": {
        "de": "Hello World",
        "en": "Hello World"
      }
    },
    "imgSquare": "data:image/svg+xml;base64,PD...",
    "name": "helloworld",
    "tags": [
      "dapp",
      "contractus"
    ],
    "version": "0.1.0",
    "versions": { }
  }
}
```

Within the src folder, the frontend source code is located. In this case, we are using Angular 5 to create a dynamic frontend application. Starting by the index.ts file, the build job will include every file into two output files, ts files into a comined js file, that includes logic and html templates and the scss files into a combined css, to declare stylings.

## 5. Angular
### 5.1 index.ts
### 5.2 routing
### 5.3 components
### 5.4 services
### 5.5 translations

