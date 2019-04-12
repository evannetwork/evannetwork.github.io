---
title: "Hello World ÐApp"
parent: Developers
nav_order: 342
permalink: /docs/04_developers/angular-hello-world.html
---

# Hello World ÐApp
## 1. Get Tutorial Application
- [Download Tutorial Application](https://github.com/evannetwork/dapps-tutorial-angular)

## 2. Build, serve and start the Application
Navigate into the Lerna project and run the following commands. The same documentation is also included in the Lerna projects readme itself.

### 2.1 Install
```bash
npm install -g lerna
npm install
lerna bootstrap --hoist
```

### 2.2 Basic Development
Build and serve the local ƉApp server, start as local server at http://localhost:3000
```bash
npm run serve-standalone
```
Build all included ƉApps
```bash
npm run dapps-build
```

Watch for changes and rebuild ƉApps
```bash
npm run dapps-serve
```

Build and watch everything
```bash
npm run serve
```

### 2.3 Open the ƉApp
When you are opening `http://localhost:3000` for the first time, you will be navigated to the [onboarding page](/docs/03_first_steps/create-identity.html). After having imported or created an identity and logged in, you will find yourself on the favorites page.

`http://localhost:3000/#/dashboard.evan/favorites.evan`

Replace `dashboard.evan/favorites.evan` with `dashboard.evan/helloworld.evan` or `helloworld.evan` to open your test application. You will see a simple application with two pages. In [this section](/docs/04_developers/deployment.html), we explain how you can deploy your application and add it to your dashboard via the favorites or also access it via `https://dashboard.test.evan.network`.

## 3. The ÐApp structure
In the ƉApp folder of each Lerna project are the individual ƉApps. You will find different projects for the different stages of the tutorial. In the first step, we will focus on the 'Hello World' project to explain the basics.

By watching into this repository, you will find a project structure like the following:
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

At the root directory, you will find the usual `nodejs`-files, like the `readme.md`, `versions.md` or `package.json`. One file, the `dbcp.json`, is used to handle the DBCP definition of the application. With this file you can specify general metadata about the application and documentation (explaining how the application works). The evan.network ƉApp application loader will look into this file first, in order to specify which files and dependencies should be loaded. With the same logic, using the module property, the Angular-core library will know, which module should be loaded during Angular setup.

Next to usual metadata, which can be declared within this file, contract ABI definitions or a data scheme can be defined, too. So the application can define its contract and data usage by itself.
It looks like as follows.

```json
{
  "public": {
    "author": "evan GmbH",
    "dapp": {
      "dependencies": {
        "angular-core": "^1.0.0",
        "angular-libs": "^1.0.0"
      },
      "entrypoint": "helloword.js",
      "files": [
        "helloword.js",
        "helloword.css"
      ],
      "primaryColor": "#004f7d",
      "secondaryColor": "#f9f9ff",
      "standalone": false,
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
      "evan"
    ],
    "version": "0.1.0",
    "versions": { }
  }
}
```

Within the src-folder, the frontend source code is located. In this case, we are using Angular 5 to create a dynamic frontend application. Starting with the `index.ts` file, the build-job will include every file into two output files, ts-files into a comined js-file, which includes logic and HTML templates and the scss-files into a combined css, to declare stylings.

## 4. Angular 5 & Ionic 3
In the next sections, it is advantageous to have a certain basic knowledge of Angular 5 and to be familiar with the various possibilities that Ionic offers. Here you will find various instructions and introductions to the frameworks:
- [Angular 5](https://angular.io/guide/quickstart)
- [Ionic 3](https://ionicframework.com/docs)

### 4.1 index.ts
The index file, as you might have expected, describes the point of entry into the application. In this case, the routes and module definitions, including the services and components created, are defined and referenced here. At the end of the file you will find the `startDApp` function, which is used to start the application from outside. Since this is a simple function, only one container is given by rendering the application. It is also possible to start applications completely without Angular. For more information on how ƉApps can be developed with other frameworks, see [here](/docs/04_developers/writing-dapps.html).

The head of the index file, starting with the library, includes functions, services, components and more. The normal Angular application requires its dependencies from `@angular/core` or `@angular/common`, and so on. To reduce and optimize loaded files during the application runtime, the libraries are already bundled within the [libraries](/docs/04_developers/libs.html) for you. If you want to include libraries that are not included yet, you can load them like a normal application.

The `dapp-wrapper` represents the stable point of entry to the evan.network application. In short, it loads DBCP definitions and applications.

The `Angular-core` includes core functionalities that are developed by the evan.network to handle blockchain interactions easily with Angular services. Also, it provides translation-, routing-, animation- and utility functionalities.

```ts
import {
  getDomainName,
} from 'dapp-browser';

import {
  NgModule,                    // @angular/core
  CommonModule,                // @angular/common
  RouterModule, Routes,        // @angular/router
  IonicModule, IonicApp,       // ionic-angular
  BrowserAnimationsModule,     // @angular/platform-browser/animations
} from 'angular-libs';

import {
  AngularCore,
  DAppLoaderComponent,
  buildModuleRoutes,
  BootstrapComponent,
  startAngularApplication, createIonicAppElement,
} from 'angular-core';
```

The next part of the index file defines routing behavior of the application. Using the `buildModuleRoutes` of the Angular-core, it becomes possible to create a large routing tree. By default, fallback routes and evan.network default routes will be attached to be able to open applications like the evan.network mailbox or data synchronisation ƉApp within each application easily zroutes-builderz). The `RootComponent` is needed within every ƉApp to handle transitions` easily.

<b>Keep in mind: We are using Ionic 3, but not the routing service of it. The routing of Ionic has some restrictions regarding dynamic loading of modules. For more information about the Angular 5 default routing, have a look [here](https://angular.io/guide/router).</b>

```ts
const dbcpOrigin = 'helloworld';
/**
 * Returns the route definitions
 */
function getRoutes(): Routes {
  // Defines the root route, fallback routes and applies the evan default routes to handle
  // queue, mailbox and anything else within this application
  return buildModuleRoutes(
    `${ dbcpOrigin }.${ getDomainName() }`,
    RootComponent,
    [
      {
        path: '',
        redirectTo: `hello-world-1`,
        pathMatch: 'full'
      },
      {
        path: `hello-world-1`,
        data: {
          // used for router transition tracking
          state: 'hello-world-1',
          navigateBack: true,
        },
        component: HelloWorldComponent,
      },
      {
        path: `hello-world-2`,
        data: {
          // used for router transition tracking
          state: 'hello-world-2',
          navigateBack: true
        },
        component: HelloWorld2Component,
      },
    ]
  );
}
```

The definition of the core module of your Angular application is also defined in this file. To handle a dynamic module creation, we are are using a `getConfig` function in order to overload the module definitions with parameters. In case of the 'Hello World' ƉApp, we have no advantages from this function. During the creation of the 'task sample' ƉApp, it will receive its justification. So keep in mind the declaration dispatcher, it will get a more important role in future.
The definition of the module is normally based on the Angular standards, but also includes the Angular-core module to load necessary services.

```ts
/**
 * Returns the module configuration for the normal or dispatcher module.
 * In case of the dispatcher module, Router configurations and BrowserModule imports are excluded
 * to load the module during runtime by the dispatcher service.
 *
 * @param isDispatcher  boolean value if the config is used for the dispatcher module
 */
function getConfig(isDispatcher?: boolean) {
  let config: any = {
    imports: [
      CommonModule,
      AngularCore,
    ],
    // reference your services
    providers: [
      Translations,
      HelloWorldService
    ]
  };

  if (!isDispatcher) {
    config.imports.unshift(BrowserAnimationsModule);
    config.imports.unshift(RouterModule.forRoot(getRoutes(), { enableTracing: false, }));

    // start the application with the angular-core bootstrap component
    config.imports.push(IonicModule.forRoot(BootstrapComponent, {
      mode: 'md'
    }));

    // start with the IonicApp module
    config.bootstrap = [
      IonicApp
    ];

    // declare your components that should be included
    config.declarations = [
      BootstrapComponent,
      RootComponent,
      HelloWorldComponent,
      HelloWorld2Component,
    ];
  }

  return config;
}

// declare your module
@NgModule(getConfig())
class HelloWorldModule {
  constructor(
    // registered your translations
    private translations: Translations,
  ) { }
}
```

At the end of the file, the initialization logic, explained below, gets defined. By using the Angular-core functions to start your application, you will be able to handle nested Angular applications to speed up the load performance of your application and to prevent memory leaks of Angular(`ionic-app-elements.ts`).

```ts
/**
 *
 * @param container  container, where the application should be rendered in
 * @param dbcpName   The name that is included in the dbcp, where this file was load from
 */
export async function startDApp(container, dbcpName) {
  const ionicAppEl = createIonicAppElement(container, dbcpOrigin);

  await startAngularApplication(HelloWorldModule, getRoutes());

  container.appendChild(ionicAppEl);
}

```

### 4.2 Services
Services are defined within the service folder and are loaded and referenced within the `index.ts`. The services are the standard Angular implementation, with a great feature that can be used. Instances of services will be created initially and then only availbable from the highest module or component reference. As a result, a service that is to be initialized only once may be initialized more often. Using the singleton service from the Angular-core, you will be able to instantiate your service only one time over the whole application.

```ts
import {
  Injectable, // @angular/core
} from 'angular-libs';

import {
  EvanCoreService,
  SingletonService,
  EvanTranslationService
} from 'angular-core';

/**************************************************************************************************/

@Injectable()
export class HelloWorldService {
  constructor(
    private singleton: SingletonService,
    private core: EvanCoreService,
    private translations: EvanTranslationService
  ) {
    return singleton.create(HelloWorldService, this, () => {
      // do something on first time when task was initialized
    }, true);
  }

  getHelloWorld() {
    return this.translations.instant('hello-world');
  }
}

```

### 4.3 Translations
The translation service uses [ngx-translate](https://github.com/ngx-translate/core). Using the plugin, you can use the `| translate` pipe within HTML templates and you can use the `EvanTranslationService for instant translations within the code.

```ts
this.translations.instant('hello-world')
```

```html
<div>{{ 'hello-world' | translate }}</div>
```

Within the translations folder, you will find the translation definition service and the corresponding translation definition files.
Define a new file for each language with the respective abbreviation of the language and enter the translations as key value pair. These can also be nested endlessly.

```ts
export const en = {
  'hello-world': 'Hello World',
  '_helloworld': {
    'field': 'Field',
    'value': 'Value',
    'account-id': 'My Account ID'
  }
};
```

To register the translations, load them into the translation service of your application.

```ts
import {
  Injectable, // @angular/core
} from 'angular-libs';

import {
  EvanTranslationService
} from 'angular-core';

import { en } from './en';
import { de } from './de';

export const translations = {
  en, de
};

@Injectable()
export class Translations {
  constructor(translate: EvanTranslationService) {
    translate.setTranslation('en', en);
    translate.setTranslation('de', de);
  }
}

```

### 4.4 Components
Components are normal components from Angular 5. For more information, have a look into [Angular 5 components](https://angular.io/guide/displaying-data).
Look into the `components/hello-world` or `components/hello-world-2` directory to inspect a small component sample. Within the `Hello World-1`-component, the Angular-core service is used to access the current logged-in user, his balance and so on. The `Hello World-2`-sample uses functions to load data from contracts. You can only view this page by deploying your 'Hello World'-application to a contract. Take a look at paragraph "6.2 Deploy ƉApp within a contract" how to do that.

<b>The component uses several evan.network Angular-core services. Drill down some logs and try yourself by testing some functions.</b>

What we need to explain is the `components/root` folder. It represents the root component that handles transitions and routings of your application. Using the animation definition, you will create a swipe animation between two views. The views are declared using the `state` parameter, which is introduced below, within the `routes` definition. So you can define when you want to swipe to the left, right, top or bottom. The rest of the file registers route change watchers, the `password dialog component` and runs the `finishDAppLoading` function. During the loading of application, the ƉApp or the parent application will include a loading symbol for your application. To handle the success and the hiding of the loading symbol, this function is called.

By using the evan.network ƉApps, you need to capture some special cases. In normal Angular applications, you would use the `OnInit`, `OnDestroy`, `AfterViewInit` interfaces to define, which life cycle your app is going through. In our case, we need to use some asynchronious `ngOnInit` functions. If the ƉApp is switched fast, the `ngOnDestroy` is called before the `ngOnInit` was resolved. As a result of this, watcher can be bound after `ngOnDestroy` and will never be detached again. Also, the `this.core.finishDAppLoading()` and `this.ref.detectChanges()` functions are called after the `ngOnInit` was resolved. If the view is already detached, this will trigger more errors. We can solve this issue by extending our component with the `AsyncComponent` class. Extend your component with this class and change your `ngOnInit` and `ngOnDestroy` functions into `_ngOnInit` and `_ngOnDestroy`. The ref is automatically detached and the loading attribute is set, until the `ngOnInit` was resolved. At the end, if the view wasn't destroyed before, the loading will be removed and the function `this.ref.detectChanges();` will be called.


```ts
{
  path: `hello-world`,
  data: { state: 'hello-world' },
  component: HelloWorldComponent,
},
```

```ts
@Component({
  selector: 'hello-world-root',
  templateUrl: 'root.html',
  animations: [
    new AnimationDefinition('*', '=>', 'hello-word-1', 'right'),
    new AnimationDefinition('hello-word-2', '=>', 'hello-word-1', 'left'),
  ]
})

export class RootComponent extends AsyncComponent {
  private loading: boolean;
  private watchRouteChange: Function;

  constructor(
    private core: EvanCoreService,
    private bcc: EvanBCCService,
    private ref: ChangeDetectorRef,
    private routingService: EvanRoutingService
  ) {
    super(ref);
  }

  async _ngOnInit() {
    await this.bcc.initialize((accountId) => this.bcc.globalPasswordDialog(accountId));
    this.watchRouteChange = this.routingService.subscribeRouteChange(() => this.ref.detectChanges());
    this.core.finishDAppLoading();
  }

  async _ngOnDestroy() {
    this.watchRouteChange();
  }
}

```

The HTML file includes a ƉApp wrapper that is capsuled around your application router. The `ƉApp-wrapper` provides a bunch of functions:
  - header bar including the current routes' part translated (route `https://evan.network#/hello-word` will show {{ 'hello-world' | translate}})
  - back navigation button, when the `navigateBack` parameter is enabled within the current routes' data
  - back navigation button, when the `reload` parameter is enabled within the current routes' data
  - if we are in an `Ionic split-pane` and the screen is smaller than 769px, a menu toggle button is inserted
  - evan.network mailbox indicator for new mails
  - evan.network synchronisation identicator (loading / error case)

```html
<evan-loading *ngIf="loading" delayLoading="500"></evan-loading>
<dapp-wrapper *ngIf="!loading" #dappWrapper>
  <div evan-content [@routerTransition]="o?.activatedRouteData?.state">
    <router-outlet #o="outlet"></router-outlet>
  </div>
</dapp-wrapper>
```

## 5 Deploy it to the Real World
### 5.1 Deploy ƉApp within a Contract
Each application can be deployed together with a contract. This allows the contract to contain the information as it should be displayed. A sample how to create and sample contracts with your 'Hello World' ƉApp can be found within the `ƉApps-tutorial-angular/scripts/create-contract.js` file. Run the following commands:

1. Start IPFS client
```sh
./scripts/go-ipfs
```

2. Publish your files to the IPFS
```sh
ipfs add -r dapps/hello-world/src
```
[![dapps-tutorial - directory](./30_ui/340_angular/img/deploy-to-ipfs.png){:width="50%"}](./30_ui/340_angular/img/deploy-to-ipfs.png)

3. Insert the deployed folder hash (e.g. "QmfZLwBPUT1n3DoJqpqnLCTcUKABLgUsgfE4KetkXdq8XK") to the correct origin to `dbcp.json` file.
[![dapps-tutorial - directory](./30_ui/340_angular/img/add-to-dbcp.png){:width="50%"}](./30_ui/340_angular/img/add-to-dbcp.png)

4. Deploy it to the contract
```sh
npm run deploy-to-contract hello-world
```

You will get a console output similar to the following. Behind the log parameter `created contract`, you will find the newly created contract ID.

[![dapps-tutorial - directory](./30_ui/340_angular/img/deploy-to-contract.png){:width="50%"}](./30_ui/340_angular/img/deploy-to-contract.png)

### 5.2 Deploy ƉApp to ENS
Have a look at [ƉApp deployment](/docs/04_developers/deployment.html).

### 5.3 View it in the Real World
After you deployed the application within a contract or using an ENS address, the ƉApp is available from everywhere, **globally**. To test this, you can use the evan.network dashboard. Open the following URL [https://dashboard.test.evan.network/index.html](https://dashboard.test.evan.network/index.html) and navigate to the `favorites ƉApp`. Before you can access your favorites, it is nessecary to create an evan.network identity. If you haven't created an identity before, have a look [here](/docs/03_first_steps.html).

Add the favorite using the following steps:

1. Open Dashboard:
[![dapps-tutorial - directory](./30_ui/340_angular/img/favorites-1.png){:width="50%"}](./30_ui/340_angular/img/favorites-1.png)

2. Add the favorite:
[![dapps-tutorial - directory](./30_ui/340_angular/img/favorites-2.png){:width="50%"}](./30_ui/340_angular/img/favorites-2.png)

3. Open the ƉApp:
[![dapps-tutorial - directory](./30_ui/340_angular/img/favorites-3.png){:width="50%"}](./30_ui/340_angular/img/favorites-3.png)

4. Result:
[![js tutorial preview](./30_ui/340_angular/img/hello-world-preview.png){:width="50%"}](./30_ui/340_angular/img/hello-world-preview.png)

By having a look into the browser network tab, you will see that your data is loaded from the IPFS server:

[![dapps-tutorial - directory](./30_ui/340_angular/img/dapp-from-contract.png){:width="400px"}](./30_ui/340_angular/img/dapp-from-contract.png)
