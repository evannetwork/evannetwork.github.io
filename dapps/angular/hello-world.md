---
title: "Hello World ÐApp"
---
# Hello World ÐApp

## 1. Get Tutorial Application
- [Download Tutorial Application](https://github.com/evannetwork/dapps-tutorial-angular)

## 2. ÐApp Wrapper application
The downloaded folder "dapps-tutorial-angular" looks like this on the top level.

[![dapps-tutorial - directory](/public/dapps/hello-world/dapps-tutorial-dir-structure.png){:width="150px"}](/public/dapps/hello-world/dapps-tutorial-dir-structure.png)

In order to be able to work in ordered and staked projects, it is necessary to split the project into several projects (e.g. dashboard-dapp, list-dapp, contract1-dapp, contract2-dapp) after a short time. To anticipate this problem and different building jobs, each project uses a [lerna](https://github.com/lerna/lerna) project structure to handle multiple repositories as easily as possible. The lerna project only includes the basic requirements and build jobs for the sub projects. The build jobs are definied within the [evan.network dapp-gulp project](/frontend/dapp-gulp).

## 3. Build, serve and start the application
Navigate into the lerna project and run the following commands. The same documentation is also included into the lerna projects readme itself.

### 3.1 Install
```bash
npm install -g lerna
npm install
lerna bootstrap --hoist
```

### 3.2 Basic Development
- build and serve the local dapp serve, starts an local server at http://localhost:3000
```bash
npm run serve-standalone
```

- build all included dapps
```bash
npm run dapps-build
```

- watch for changes and rebuild dapps
```bash
npm run dapps-serve
```

- build and watch everything
 ```bash
npm run serve
```

### 3.3 Open the DApp
When you are opening http://localhost:3000 initially you will be navigated to the [onboarding page](/tutorial/create-identity). After you have imported or created an identity and logged in, you will find yourself on the Favorites page.

http://localhost:3000/#/dashboard.evan/favorites.evan

Replace "dashboard.evan/favorites.evan" with "dashboard.evan/helloworld.evan" or "helloworld.evan" to open your test application. You will see an simple application with two pages. At the end of this tutorial we explain how you can deploy your application and add it to your dashboard via the Favorites or also access it via https://dashboard.evan.network.com.

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

At the root directory you will find the usal nodejs files, like the readme.md, versions.md or package.json. One file, the dbcp.json, is used to handle the dbcp definition of the application. With this file, you can specify general metadata about the application and "documentation", how the application works. The evan.network dapp application loader will look into this file first, to specify wich files and dependencies should be loaded. With the same logic, using the module property, the angular-core library will know, which module should be loaded during angular setup. 

Against usal metadata that can be declared within this file, contract abi definitions or a data schema can be defined too. So the application can define its contract and data usage by itself.
It looks like the following.

```json
{
  "public": {
    "author": "contractus",
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
      "contractus"
    ],
    "version": "0.1.0",
    "versions": { }
  }
}
```

Within the src folder, the frontend source code is located. In this case, we are using Angular 5 to create a dynamic frontend application. Starting by the index.ts file, the build job will include every file into two output files, ts files into a comined js file, that includes logic and html templates and the scss files into a combined css, to declare stylings.

## 5. Angular 5 & Ionic 3
In the next sections it is advantageous to have a certain basic knowledge of Angular 5 and to be familiar with the various possibilities that Ionic offers. Here you will find various instructions and introductions to the frameworks:
- [Angular 5](https://angular.io/guide/quickstart)
- [Ionic 3](https://ionicframework.com/docs)

If you have questions about our fancy Angular interpretation and you want to know more, about the evan.network angular libraries, have a look [here](angular/basics).

### 5.1 index.ts
The index file, as you would have expected, describes the entry point into the application. In this case, the routes and module definitions, including the services and components created, are defined and referenced here. At the end of the file you will find the "startDApp" function which is used to start the application from outside. Since this is a simple function, only one container is given by rendering the application, it is also possible to start applications completely without Angular. For more information on how DApps can be developed with other frameworks, see [here](/dapps/use-other-frameworks).

The head of the index file, starts with the library includes of functions, services, components and more. The normale angular application require its dependencies from @angular/core or @angular/common and so on. To reduce and optimize loaded files during the application runtime, the libraries are already bundled within the [angular-libs](/frontend/angular-libs) for you. If you want to include libraries that are not included yet, you can load it like a normal application.

The [dapp](/frontend/dapp-wrapper) represents the stable entry point of the evan.network application. In short, it loads DBCP definitions and load applications from their.

The [angular-core](/frontend/angular-core) includes core functionalities that are developed by the evan.network, to handle blockchain interactions easily using angular services. Also it provides translation-, routing-, animation- and utility functionalities.

```ts
import {
  getDomainName,
} from 'dapp';

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
  RoutesBuilder,
  BootstrapComponent,
  startAngularApplication, createIonicAppElement,
} from 'angular-core';
```

The next part of the index file defines routing behavior of the application. Using the RoutesBuilder of the angular-core, its possible to create a large routing tree. By default, fallback routes and evan.network default routes will be attached, to be able to open applications like the evan.network mailbox or data synchronisation DApp within each application, easily [routes-builder](/frontend/angular-core/routes-builder). The RootComponent is needed within every DApp to handle [transitions between views](/fronend/animations) easily.

<b>Keep in mind: Were using Ionic 3, but not the Routing service of it. The routing of Ionic has some restrictions by dynamic loading of modules. For more informations about the Angular 5 default routing, have a look in [here](https://angular.io/guide/router).</b>

```ts
const dbcpOrigin = 'helloworld';
/**
 * Returns the route definitions
 */
function getRoutes(): Routes {
  // Defines the root route, fallback routes and applies the contractus default routes to handle
  // queue, mailbox and anything else within this application
  return RoutesBuilder.buildModuleRoutes(
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

The definition of the core module of your angular application is also defined in this file. To handle a dynamic module creation, were are using a "getConfig" function, to overload the module definition with parameters. In case of the "Hello World DApp" we have no advantages of this function. During the creation of the "task sample DApp", it will get it's sence. So keep in mind the declaration "dispatcher", it will get a bigger role in future.
The definition of the module is normally based on the Angular Standards, but also includes the AngularCore module to load necessary services.

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

At the end of the file the initialization logic, mentioned below, is defined. By using the angular-core functions to start your application, you will be able to handle nested Angular applications, to speed up the load performance of your application and to prevent memory leaks of Angular([ionic-app-elements.ts](/frontend/angular-core/ionic-app-elements)).

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

### 5.2 services
Services are declared within the service folder and are loaded and referenced within the index.ts. The services are the standard angular implementation, with a great feature that can be used. Instances of services will be created initially and only availbable from the highest module or component reference. As a result, a service that is to be initialized only once may be initialized more often. Using the singleton service from the angular-core, you will be able to instantiate your service only one time over the whole application.

```ts
import {
  Injectable, // @angular/core
} from 'angular-libs';

import {
  ContractusCoreService,
  SingletonService,
  ContractusTranslationService
} from 'angular-core';

/**************************************************************************************************/

@Injectable()
export class HelloWorldService {
  constructor(
    private singleton: SingletonService,
    private core: ContractusCoreService,
    private translations: ContractusTranslationService
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

### 5.3 translations
The translation service uses [ngx-translate](https://github.com/ngx-translate/core). Using the plugin, you can use the "| translate" pipe within html templates and you can use the ContractusTranslationService for instant translations within the code.

```ts
this.translations.instant('hello-world')
```

```html
<div>{{ 'hello-world' | translate }}</div>
```

Within the translations folder you will find the translation definition service and the according translation definition files.
For each language define a new file with the respective abbreviation of the language and enter the translations as key value pair. These can also be endlessly nested.

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

To register the translations, load them within the translation service of your application.

```ts
import {
  Injectable, // @angular/core
} from 'angular-libs';

import {
  ContractusTranslationService
} from 'angular-core';

import { en } from './en';
import { de } from './de';

export const translations = {
  en, de
};

@Injectable()
export class Translations {
  constructor(translate: ContractusTranslationService) {
    translate.setTranslation('en', en);
    translate.setTranslation('de', de);
  }
}

```

### 5.4 components
Components are normal components from Angular 5. For more informations, have a look into [Angular 5 components](https://angular.io/guide/displaying-data) and [Performance optimizations](performance-optimizations).
Look in to the "components/hello-world" or "components/hello-world-2" directory to inspect an very small component sample. Within the hello-world-1 component, the angular-core core service is used, to access the current logged in user, its balance and so on. The hello-world-2 sample uses functions to load data from contracts. You can only view this page, by deploying your hello-word application to an contract. Watch at point "6.2 Deploy DApp within an contract", how to do that.

<b>The component uses several evan.network core angular service. Drill down some logs and try yourself by testing some functions.</b>

What we need to explain is the "components/root" folder. This represents the root component, that handles transitions and routings of your application. Using the animation definition, you will create an swipe animation between two views. The views are declared using the "state" parameter, mentioned below, within the routes definition. So you can define, when you want to swipe to the left, right, top or bottom. The rest of the file registers route change watchers, the [password dialog component](/frontend/password-dialog) and runs the "finishDAppLoading" function. During the application load, the DApp or the parent application will included an loading symbol for your application. To handle the success and hiding of the loading symbol, this function is called. 

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

export class RootComponent implements OnInit {
  private loading: boolean;
  private watchRouteChange: Function;

  constructor(
    private core: ContractusCoreService,
    private bcc: ContractusBCCService,
    private ref: ChangeDetectorRef,
    private routingService: ContractusRoutingService
  ) { }

  async ngOnInit() {
    this.ref.detach();
    this.loading = true;

    this.ref.detectChanges();
    await this.bcc.initialize((accountId) => this.bcc.globalPasswordDialog(accountId));

    this.watchRouteChange = this.routingService.subscribeRouteChange(() => this.ref.detectChanges());

    this.loading = false;
    this.core.finishDAppLoading();
    this.ref.detectChanges();
  }

  ngOnDestroy() {
    this.watchRouteChange();
  }
}

```

The html file includes an dapp-wrapper that is capsuled around your application router. The [dapp-wrapper](/frontend/angular-core/dapp-wrapper) provides a bunch of functions:
  - Header bar including the current routes part translated (route https://evan.network#/hello-word will show {{ 'hello-world' | translate}})
  - Back Navigation Button, when the navigateBack Parameter is enable within the current routes data
  - Back Navigation Button, when the reload Parameter is enable within the current routes data
  - If we are in an [ionic split-pane](/frontend/ionic-split-pane) and the screen is smaller than 769px, a menu toggle button is inserted.
  - evan.network Mailbox indicator for new mails
  - evan.network Synchronisation identicator (loading / error case)

```html
<contractus-loading *ngIf="loading" delayLoading="500"></contractus-loading>
<dapp-wrapper *ngIf="!loading" #dappWrapper>
  <div contractus-content [@routerTransition]="o?.activatedRouteData?.state">
    <router-outlet #o="outlet"></router-outlet>
  </div>
</dapp-wrapper>
```

## 6 Deploy it to the real world
### 6.1 Deploy DApp to ENS
Each DApp can be deployed to the evan.network, so it can be accessed from anywhere, not only from a localhost server. This is handle by an wrapped library, to handle the deployment as simple as possible. To deploy your application run the following command.

```ts
npm run deploy
```

Now, you can open the ens address to your application on https://dashboard.evan.network#/my-ens-address.evan. (my-ens-address = dbcp.name)

### 6.2 Deploy DApp within an contract
Each application can be deployed together with a contract. This allows the contract to contain the information as it should be displayed. A little sample, how to create and sample contract with your hello world app can be found within the dapps-tutorial-angular/scripts/create-contract.js file. Run the following command to start the script for your specific application.

```sh
npm run ipfs deamon hello-world
```

```sh
npm run deploy-to-contract hello-world
```

After the contract id of the created contract was logged to your console, you can open this contract like the ens path before. Just replace your DApp ens path, with the id of your contract (#/dashboard/helloworld.evan => #/dashboard/0x65dCf129E612d4e40bEA8866029e0595BC1Ba5EC). Within the network tab you will see, that the sources for your contract are now loaded from the contract address. 

[![dapps-tutorial - directory](/public/dapps/hello-world/dapp-from-contract.png){:width="200px"}]
