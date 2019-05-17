---
title: "Angular - Task ƉApp DataContract"
parent: Developers
grand_parent: UI
nav_order: 4346
permalink: /docs/developers/ui/angular/task-data-contract.html
---

# Angular - Task ƉApp Data-Contract
**Before performing this example, please go through the [Task ƉApp setup](/docs/developers/ui/angular/task.html) tutorial, as this tutorial is based on this example.**

In this section you will create contracts, read from them and handle several data interactions with the contracts by using the evan.network DataContract and the blockchain-core. So each data that is currently cached within the local storage will be moved into a contract. All needed I18N values and keys are predefined within the I18N folder and not noticed during the example.

For how to write the task ƉApp using your own contract implementation, have a look at this: [Angular - Task ƉApp Custom Contract](/docs/developers/ui/angular/task-custom-contract.html).

If you don't want to code by yourself, you can simply read the docs and copy the final resulting src folder from [dapps/task-data-contract/src](https://github.com/evannetwork/sample-dapps-angular/tree/master/dapps/task-data-contract) to the [dapps/task/src](https://github.com/evannetwork/sample-dapps-angular/tree/master/dapps/task) folder.

# 1. Contract Implementation
Before your start your implementation, it is important to decide what functionalities you will need. You need to think about data parameters, user roles including security restrictions and so on...

For this example, we need a contract that handles some contract metadata and a list of todos. This is the perfect case for the [evan.network DataContract](/docs/developers/concepts/data-contract.html) / [DataContract API doc](https://api-blockchain-core.readthedocs.io/en/latest/contracts/data-contract.html).

When you use a self-implemented contract, it is important to add the contract implementation ABI to our `dbcp.json` definition file. In this case, we can simply use the blockchain-core DataContract wrapper implementation to handle our contract calls. For documentation reasons, you should still put the ABI definition of the DataContract into the DBCP definition. So other people that read the DBCP definition of the created contract automaticaly receive your contract definition and functions. So you can program the contract from anywhere, also outside of your application.

Insert the ABI definition into your `dbcp.json` file from the following [dbcp.json](https://github.com/evannetwork/sample-dapps-angular/blob/master/dapps/task/dbcp.json) (it is a bit large to insert the full ABI here in the documentation).

```json
{
  "public": {
    ...
    "abis": {
      "own": [
        {
          "constant": true,
          "inputs": [
            {
              "name": "key",
              "type": "bytes32"
            }
          ],
          "name": "getListEntryCount",
          ...
        }
    }
    ...
  }
}
```

# 2. Data Scheme
The data scheme is also a property of the `dbcp.json` that describes the data structure of our contract deeply. In our case, the data scheme will describe the data that are saved within our DataContract's todo list.

```json
{
  ...
  "dataSchema": {
    "todos": {
      "$id": "todos_schema",
      "additionalProperties": false,
      "type": "object",
      "properties": {
        "id": {
          "type": "string"
        },
        "title": {
          "type": "string"
        }
      }
    },
    "todologs": {
      "$id": "todologs_schema",
      "additionalProperties": false,
      "type": "object",
      "properties": {
        "id": {
          "type": "string"
        },
        "solved": {
          "type": "boolean"
        }
      }
    }
  }
  ...
}
```

# 3. Create and read the DataContract
The ƉApp will be designed to handle both sides, the contract creation and the data consumption. The evan.network dashboard includes a dynamic parameter routing to open unregistered ENS and contract addresses. So the ƉApp can check the current opened URL, if a contract ID or the normal ENS address is opened. When the ENS address is opened, we will redirect to a contract creation page. When a contract ID is opened, the user gets redirected to the `TodoMVC` component.

To do this, you will need some new structures within your code:
  1. Contract service that handles contract creation
  2. Dispatcher to handle asynchronious and page-reload-save contract interactions
  3. Contract creation components
  4. Routing for create and detail
  5. Create a new task

## 3.1 Contract Service
Create a new file within the services folder and name it `task.ts`. Within this file, we will declare all the functions that are needed to interact with task contracts. To create a new DataContract using the DBCP definition of our tutorial task, only view lines of code are needed. We will create a new DataContract instance and apply the loaded description to the DataContract creation function.

```ts
  /**
   * Create a new DataContract instance.
   */
  getDataContract() {
    return new DataContract({
      cryptoProvider: this.bccService.description.cryptoProvider,
      dfs: this.bccService.CoreBundle.CoreRuntime.dfs,
      executor: this.bccService.executor,
      loader: this.bccService.contractLoader,
      nameResolver: this.bccService.nameResolver,
      sharing: this.bccService.sharing,
      web3: this.bccService.web3,
      description: this.bccService.description,
    });
  }

  /**
   * Create a new task data contract instance.
   * @param name name of the task data contract
   */
  async createNewTask(name: string) {
    // create new data contract instance
    const dataContract = this.getDataContract();

    // load dapp description to add contract metadata
    const dappDescription = await this.descriptionService.getDescription(this.ensAddress, true);
    dappDescription.name = name;
    dappDescription.i18n.name.en = name;
    dappDescription.i18n.name.de = name;

    return await dataContract.create(
      'tasks',
      this.coreService.activeAccount(),
      null,
      { public: dappDescription }
    );
  }
```

The first parameter in `dataContract.create('tasks', ...)` is used to handle, which contract factory shall be loaded. At this path the evan.network `TaskDataContractFactory` is deployed. This factory is derived from the DataContract factory and can handle two data lists (todos, todologs). View point four for more details on the DataContract list handling.

After the contract was created, we want to write the reference into our favorites. The favorites ƉApp cannot only handle ƉApps from ENS addresses, it is also possible to load contracts with an underlying DBCP definition. To do this, require the Angular-core bookmark service and run the following functions.

```ts
addToFavorites(task: any) {
  return this.bookmarkService
    .getBookmarkDefinition(task.address)
    .then(dapp => this.bookmarkService.queueAddBookmark(task.address, dapp))
}
```

## 3.2 Dispatcher
Depending on the block time and network connection, contract creation and interaction can leave a large gap in the usage time of the UI. To avoid a blocking frontend, so-called dispatchers are used. Dispatchers are defined and exported by the ƉApp as an Angular module. So the dispatchers themselves can use the services of the ƉApp, and at the same time the evan.network Angular framework can restart them even after a page load. For this purpose, the contract functions are not executed directly in the components, but only a new dispatcher task is inserted into the evan.network queue. The queue then independently handles the processing of the queued orders. The UI is provided with various options for listening to the processing of a queue.

If a dispatcher fails, the error is caught by the framework and an error is displayed in the top right corner of the UI. With this button, the task can be repeated or deleted via the synchronization details.

Create a new folder within your ƉApp and call it 'dispatcher'. Create a new file called `task-dispatcher.ts` and insert the following code:

```ts
import {
  QueueSequence,
  QueueDispatcher
} from 'angular-core';

import {
  translations
} from '../i18n/registry';

import {
  TaskService
} from '../services/task';

/**************************************************************************************************/

export const TaskCreateDispatcher = new QueueDispatcher(
  [
    new QueueSequence(
      '_tutorialtask.dispatcher.create-task',
      '_tutorialtask.dispatcher.create-task-description',
      async (service: TaskService, queueEntry: any) => {
        const tasks = queueEntry.data;
        const results = [ ];

        for (let task of tasks) {
          // create new task
          const newTask = await service.createNewTask(task.name);

          // reference to my favorites
          await service.addToFavorites(newTask._address);

          results.push(newTask._address);
        }

        return results;
      }
    )
  ],
  translations,
  'TaskService'
);

```

Some Angular-core classes for the queue are imported to create a new dispatcher with several sequences. Each dispatcher can have n* sequences that will be executed after another. If one sequence is solved, the return values are saved for the next sequence. So, when the user reloads the browser during the sequence 3/5, the queue will continue when the page is loaded with the step 3/5.

Only one service can be injected to a queue dispatcher. In this case, the task service will contain all the functions that our dispatcher needs.

After you created the new dispatcher, you need to export the service and dispatcher within the index-ts and you will need to create a new module with the name `DispatcherModule`. Now the meaning of the function `module(getConfig(true))` can also be explained. Components and some modules may only be added in an Angular module in a `zone.js` scope. If we took the standard module for the dispatcher and the queue would try to analyze this module again, we would run into various errors. To avoid this, we add another module here, the `DispatcherModul`. Only special modules and services are registered in it. Thus, not a single component can be displayed with this module. However, services for our dispatcher can be exported there and inserted into the dispatcher. We get Angular runtime data in our dispatcher, regardless of which ƉApp has just started. So while the queue is running, the user can change ƉApps and reload the page. However, our data will be synchronized.

Add the following code to your `index.ts:
```ts
import { TaskService } from './services/task';

import { TaskCreateDispatcher } from './dispatcher/task-dispatcher';

// export TaskService and TaskCreateDispatcher for dispatcher module runtime
export { TaskService, TaskCreateDispatcher }
```

```ts
@NgModule(getConfig(true))
export class DispatcherModule {
  constructor() { }
}
```

## 3.3 Contract Creation Component
In this case, we only need to specify a name for our task, no other metadata is needed. If you want to add more metadata in future, the blockchain-core has some utlity functions for this.

Before we create our component, it is important to create an easy bridge to trigger the task creation from anywhere. To do so, add the following code to your task service:

```ts
...
@Injectable()
export class TaskService implements OnInit {
  public createQueueID: QueueId;
  public ensAddress: string;

  constructor(
    public descriptionService: EvanDescriptionService,
    public queue: EvanQueue,
    public bccService: EvanBCCService,
    public coreService: EvanCoreService,
    public bookmarkService: EvanBookmarkService
  ) {
    this.ensAddress = this.descriptionService.getEvanENSAddress('tutorialtask');

    this.createQueueID = new QueueId(
      this.ensAddress,
      'TaskCreateDispatcher'
    );
  }

  /**
   * Trigger the creation of a new task.
   * @param name name of the task
   */
  triggerTaskQueue(name: string) {
    this.queue.addQueueData(
      this.createQueueID,
      { name, }
    );
  }
  ...
```

This is necessary so that the Angular queue recognizes, from which ƉApp the dispatcher must be loaded. This queue ID can be listened on immediately to see the end of processing.

So, navigate to the `task/src/components` folder and create the `create-task` folder, with the following structure:
- create-task
  - create-task.ts
  - create-task.html

create-task.ts
```ts
import {
  Component, ChangeDetectorRef, OnInit, OnDestroy  // @angular/core
} from 'angular-libs';

import {
  EvanQueue,
  AsyncComponent
} from 'angular-core';

import {
  TaskService
} from '../../services/task';

/**************************************************************************************************/

@Component({
  selector: 'task-create',
  templateUrl: './task-create.html'
})
export class TaskCreateComponent extends AsyncComponent {
  public taskName = '';
  public contractId: string;

  private onCreation: Function;

  constructor(
    public ref: ChangeDetectorRef,
    public taskService: TaskService,
    public queue: EvanQueue
  ) { }

  async _ngOnInit() {
    this.onCreation = await this.queue.onQueueFinish(this.taskService.createQueueID, async (reload, data) => {
      if (reload) {
        try {
          if (!(data[0] instanceof Error)) {
            await this.alertService.showSubmitAlert(
              '_tutorialtask.task-created',
              '_tutorialtask.task-created-description',
              '_tutorialtask.cancel',
              '_tutorialtask.ok',
            );

            this.routinService.navigate(`./${ data[0] }`);
          }

          this.loading = false;
          this.ref.detectChanges();
        } catch (ex) { }
      }
    });
  }

  /**
   * Unbind onCreation listener
   */
  async _ngOnDestroy() {
    this.onCreation && this.onCreation();
  }

  /**
   * Create a new contract instance.
   */
  createNewContract() {
    this.loading = true;
    this.taskService.triggerTaskQueue(this.taskName);
    this.taskName = '';
    this.ref.detectChanges();
  }
```

create-task.html
```html
<section class="todoapp">
  <header class="header">
    <h1>{{ '_tutorialtask.header-task-create' | translate }}</h1>

    <div text-center>
      <input class="new-todo"
        autofocus=""
        [placeholder]="'_tutorialtask.task-name' | translate"
        [(ngModel)]="taskName"
        (keyup.enter)="createNewContract()"
        (ngModelChange)="ref.detectChanges()">
      <button ion-button outline round
        (click)="createNewContract()"
        [disabled]="!taskName || loading">
        <ion-spinner *ngIf="loading" color="light"></ion-spinner>
        {{ '_tutorialtask.task-create' | translate }}
      </button>
    </div>
  </header>
</section>
```

We simply reference the task create service in our component, such that the code of the component is comparably lean. Also, we can use the `queue.onQueueFinish` and the `createQueueID` to listen for task creation finishing. When the task was created successfully, we will show an alert with I18N values, to ask the user to open the contract.

## 3.4 Routing
To handle the routing correctly for the creation and task details, we need to add some new routing. In the case that we are opening the ENS address of the ƉApp directly, the created component should be displayed. When the ƉApp is opened using a contract address, we should directly open the task detail component. Adjust the routing to the following:

```ts
function getRoutes(): Routes {
  // Defines the root route, fallback routes and applies the evan default routes to handle
  // queue, mailbox and anything else within this application
  return buildModuleRoutes(
    `${ dbcpOrigin }.${ getDomainName() }`,
    RootComponent,
    [
      {
        path: '',
        component: TaskCreateComponent,
        data: {
          state: 'task-create',
          navigateBack: true
        },
      },
      {
        path: ':address',
        component: TodoApp,
        data: {
          state: 'task-detail',
          navigateBack: true
        }
      },
    ]
  );
}
```

## 3.5 Create Task
After setting up the new components and the structures for the dispatcher, it is possible to create a new contract via our ƉApp.

If we would do that now, however, we would have a problem. The ƉApp is currently not deployed to any ENS path, so the `public.dapp.origin` IPFS path of `dbcp.json` does not point to the correct value. To fix this, we need a valid IPFS path. This can be based on the 'deploy to contract' manual of the Lerna project. Navigate to the root level of the Lerna project and execute the following command to start an IPFS daemon:
```sh
"./scripts/go-ipfs.sh".
```

After starting the IPFS, navigate to the `dapps/task` folder and execute the following command:
```sh
"ipfs add -r dist"
```

It should result in something similar:
```sh
dist/
added QmWFiejRGvoaihw9BKt41rVGH6E7FbueugXWjwAmtLStCD dist/components/app/app.d.ts
added QmanTufEFhHVy5YodSv3WKzLMKvEG9nTVjMR8CycgzbUyd dist/components/root/root.d.ts
added Qmdo2e8irJ2QSMN4JAsK6uBgoCfaiN8keqNNzQoJAiBzQn dist/components/task-create/task-create.d.ts
added QmYC6CMVmwVC21kMKn6hyJRdUTwXskeB5NwEcuMEtU7fBA dist/dispatcher/task-dispatcher.d.ts
added QmRR2nrSowiuYMhH7nWo9UJwKoLmm4hY7NSx16u1UpnZaw dist/i18n/de.d.ts
added QmP6BFpGSQEQmRdrAfvx86TLDQ3VHprvPpVVpyy9z79Jpy dist/i18n/en.d.ts
added QmZzR6jiYyfVtTJmh1RfnPsCdRRjjCCS4MVPn198zpZ29e dist/i18n/registry.d.ts
added QmdR5QxnR4aV14VZtcKm7Z5A8BSK6qDKrvWyhLccZLxN5N dist/index.d.ts
added QmcrZXEGPXEWsCQMiY2JLhZQ1DWRJy2o1RDhEhwD76dE9H dist/services/store.d.ts
added QmZ4VSCvpW5f7kbEQq53pvYnSYxwnxDc8wd2L3L91sMoob dist/services/task.d.ts
added QmVV4BwBZ82dXSJWYwTHDKFhwZWF6jYEWyGGJ8fqGdzQzd dist/tutorialtask.css
added QmTBKx4AXbgDJzcy629pcXpLuEJAL1fj9ehuWshjrB7WGH dist/tutorialtask.js
added Qmcd51qLgDUVTFBpe78ECbMHQQc2HrdjS52SCqTpS8AVwU dist/components/app
added QmVRHkXZJHu9iyjmm36isA6LzjhLEbrmZWabXWTavcw6k8 dist/components/root
added Qmaq11KKt82MAkjQDuwGkLeTqshC6jAouGZq1ZMQhHHm69 dist/components/task-create
added QmUXfWbiMmb68TpuutS66xPKVmAR5exeXK1vddYenZDwgE dist/components
added QmVPVmKAuqKpUXHWRJkvDhEDQNqKo8oQSNJ3oPJPYK8fFE dist/dispatcher
added QmPKUYZiKNtgbn2vNTy8qxyx2vdXVvogLm245oKfHS3MMi dist/i18n
added Qmc76vZsXE7rMukEtsyMxGucNxqcbFNMbVWGMUrQAkEsmD dist/services
added QmXCnDwasWd9JQ3rz7Rjc3uQt7SDiuryzWAXerPdL4KHTs dist
```

Copy the latest IPFS path for the dist folder ('QmXCnDwasWd9JQ3rz7Rjc3uQt7SDiuryzWAXerPdL4KHTs') and replace the origin within your `dbcp.json` file.

**Now you can create a new contract instance. Reload your browser and try it.**

## 3.6 Developing
For development purposes it is time consuming to publish your sources to the IPFS and to create a new contract every time you changed something. To handle this, the `buildModuleRoutes` function will do some magic. Using the evan.network frame multiple Angular application within another Angular application. So it is important to build dynamic routes corresponding to the specific parent Angular application. As a side effect, your defined routes are nested in any case within themselves. A routing tree is built as follows:

```json

[
  {
    "path": "dashboard.test/tutorialtask.test",
    "children": [
      {
        "path": "tutorialtask.test",
        "children": [
          ...
          {
            "path": "favorites.test",
            "data": {
              "state": "favorites",
              "navigateBack": true
            },
            "children": [
              {
                "path": "**",
                "data": {
                  "state": "favorites",
                  "navigateBack": true
                }
              }
            ]
          },
          {
            "path": "",
            "data": {
              "state": "task-create",
              "navigateBack": true
            }
          },
          {
            "path": ":address",
            "data": {
              "state": "task-detail",
              "navigateBack": true
            }
          }
        ]
      },
      {
        "path": "favorites.test",
        "data": {
          "state": "favorites",
          "navigateBack": true
        },
        "children": [
          {
            "path": "**",
            "data": {
              "state": "favorites",
              "navigateBack": true
            }
          }
        ]
      },
      ...
      {
        "path": "",
        "data": {
          "state": "task-create",
          "navigateBack": true
        }
      },
      {
        "path": ":address",
        "data": {
          "state": "task-detail",
          "navigateBack": true
        }
      }
    ],
    "runGuardsAndResolvers": "always",
    "data": {
      "evanDynamicRoutes": true,
      "dynamicRoutesConfig": {
        "dappEns": "tutorialtask.test",
        "routes": [
          {
            "path": "",
            "data": {
              "state": "task-create",
              "navigateBack": true
            }
          },
          {
            "path": ":address",
            "data": {
              "state": "task-detail",
              "navigateBack": true
            }
          }
        ]
      }
    }
  },
]
```

Do the following things to develop the details page using your local changes:
1. If you created a contract ID and navigated to it by submitting the alert, the contract ID will appear within the URL (e.g. `http://localhost:3000/dev.html#/dashboard.evan/0x08a76987Ac24750287Fcbf51378525aA62499228z).

2. Copy the contract ID and open you task creation ƉApp again on the following URL : `http://localhost:3000/dev.html#/dashboard.test/tutorialtask.test`.

3. Append the contract ID to your creation URL and the contract will be loaded with your local changes. `http://localhost:3000/dev.html#/dashboard.test/tutorialtask.test` =>  `http://localhost:3000/dev.html#/dashboard.test/tutorialtask.test/0x08a76987Ac24750287Fcbf51378525aA62499228`


# 4. Task Detail
After the task contract was created, the task instance can be openend, but it will save its todos and resolves into the browser's local storage. We need to answer the following changes to handle our data within the blockchain:

1. What should the detail component do?
2. Handling of DataContract list entries for todos and todo resolves
2. Adjust detail components to handle new list entry features

## 4.1 What should the detail component do?
Using the data contract API, we can add list entries to two, within the `TaskDataContractFactory` defined lists (todos, todo logs) that include list entries, which are defined within the `dbcp.json` data scheme. In our case, we specified that we can add todos with the properties 'title' and 'ID' to the todos and objects with the properties 'solved' and 'ID' to the todo logs. If we specify 'todoData' that not respect the DBCP description, the blockchain-core will check the description and return error codes by using wrong values.

But why splitting up into two lists? Technically it is possible to change and delete list entries. But if we want to handle the correct mind of blockchain logic, we should not change or delete any todo. On this way, we can save our history, unchanged and comprehensible. This is where the todo log list takes its role. New todos will be saved within the todos list. When we want to solve a todo, we will simply create a new todo log, with the same ID as the todo. In future, we can load both lists, so we can check which todo was solved.

## 4.2 List Entry Dispatcher & Service
Open the `services/task.ts` service and add the following function.

```ts
  /**
   * Adds a list entry to an specific list
   * @param listEntry list entry to add, includes data of the todo and the corresponding task contract id and the list name
   */
  async addListEntry(taskId: string, listName: string, todoData: any) {
    const dataContract = this.getDataContract();

    await dataContract.addListEntries(
      taskId,
      [ listName ],
      [ todoData ],
      this.coreService.activeAccount()
    );
  }
```

Add a new dispatcher to the `dispatchers/task-dispatcher.ts` file that uses this function to create new list entries:

```ts
export const ListEntryDispatcher = new QueueDispatcher(
  [
    new QueueSequence(
      '_tutorialtask.dispatcher.list-entry',
      '_tutorialtask.dispatcher.list-entry-description',
      async (service: TaskService, queueEntry: any) => {
        const listEntries = queueEntry.data;

        for (let entry of listEntries) {
          await service.addListEntry(entry.taskId, entry.listName, entry.data);
        }
      }
    )
  ],
  translations,
  'TaskService'
);
```

Don't forget to export the dispatcher within the `index.ts` file:
```ts
...
import { TaskService } from './services/task';

import { TaskCreateDispatcher } from './dispatcher/task-dispatcher';
import { ListEntryDispatcher } from './dispatcher/task-dispatcher';

// export TaskService and TaskCreateDispatcher for dispatcher module runtime
export { TaskService, TaskCreateDispatcher, ListEntryDispatcher }
...
```

## 4.3 Detail Component
Most functions that were defined within the todo service will be obsolete, because we don't want to delete or change any todo value. As a result of this, you can simply delete them. The detail component will need some special welfare. This gets a bit tricky, so we will start at the top of the new detail component.

At first, we will need a lot of evan.network services and some component class parameters. Each service will be used and explained within the component.

```ts
import {
	EvanRoutingService,
	EvanDescriptionService,
	EvanCoreService,
	EvanQueue,
	EvanTranslationService,
  AsyncComponent
} from 'angular-core';

import {
	TaskService
} from '../../services/task';

/**************************************************************************************************/

@Component({
	selector: 'todo-app',
	templateUrl: './app.html'
})
export class TodoApp extends AsyncComponent {
	newTodoText = '';

	public contractId: string;
	public description: any;
	public invalid: boolean;
	public loading: boolean;
	public todos: Array<any>;
	public todoLogs: Array<any>;
	public queueWatchTodos: Function;
	private queueId: any;

	constructor(
		public ref: ChangeDetectorRef,
		private routingService: EvanRoutingService,
		private descriptionService: EvanDescriptionService,
		private coreService: EvanCoreService,
		private queue: EvanQueue,
		private taskService: TaskService,
		private translationService: EvanTranslationService
	) { }
```

The component initialzation steps need asynchronious operations. As a result of this and because of Angular best practices, all initalization steps are included within the `ngOnInit` function. So have a look on the `ngOnInit` function.

```ts
async _ngOnInit() {
  this.contractId = this.routingService.getHashParam('address');

  if (this.contractId.indexOf('0x') !== 0) {
    this.invalid = true;
  } else {
    this.loading = true;
    this.ref.detectChanges();

    // load contract description and todos
    this.description = await this.descriptionService.getDescription(this.contractId);
    this.queueId = this.taskService.getListEntryQueueID(this.contractId);

    // set translation for dapp-wrapper title (contract-id => contract title)
    this.translationService.addSingleTranslation(this.contractId, this.description.name);

    // add a queue watcher for the current contract and the creation of new list entries
    this.queueWatchTodos = await this.queue.onQueueFinish(this.queueId, async () => {
      this.todos = await this.getListEntries('todos');
      this.todoLogs = (await this.getListEntries('todologs')).map(todoLog => todoLog.id);

      this.checkTodosFinished();
      this.ref.detectChanges();
    });
  }
}
```

We will check if a valid contract address is applied to the URL. If not, we can show an error within the frontend. After this, the contract description will be loaded and a translation string for the ƉApp-wrapper title will be added. If we don't run the `addSingleTranslation` function, the frontend will print out the full contract ID within the header. When the contract details were loaded, an `onQueueFinish` handler can be binded. So we can load todos and todologs initially and in case something is saved.

The `getListEntries` function uses the DataContract API to load all existing list values. After the todo logs were loaded, a completed flag will be written to the local todo instances, to check it more easier within the HTML template.

```ts
	/**
	 * Load the todos for the current selected contract
	 */
	async getListEntries(listName: string) {
		return await this.taskService.getDataContract().getListEntries(
			this.contractId,
			listName,
			this.coreService.activeAccount()
		);
	}

	/**
	 * Set completed flag on todos.
	 */
	checkTodosFinished() {
		this.todoLogs.forEach(todoLog => {
			for (let todo of this.todos) {
				if (todo.id === todoLog) {
					todo.completed = true;;
				}
			}
		});
	}
```

The `addTodo` and `addTodoLog` functions represents the core blockchain logic of the component. The `addTodo` generates a new todo data object, pushes it into the `AddListEntry` queue and adds a todo copy, including a loading flag, into the local todos. When the queue has finished saving, the todos will be reloaded and the correct todo, without the loading flag, is loaded. By solving a todo by adding a new todo log, the local todo is completed and loading the flag will be set to true and a new todo log will be added to the queue.
```ts
/**
 * Creates a new Todo with the current newTodoText
 */
addTodo() {
  if (this.newTodoText.trim().length) {
    // create todo data including a id, so we can identify it later
    const todoData: any = {
      id: this.coreService.utils.generateID(),
      title: this.newTodoText,
    };

    // save the todo using the queue
    this.queue.addQueueData(this.queueId, {
      taskId: this.contractId,
      data: todoData,
      listName: 'todos',
    });

    // add it already to the list and display it loading
    const todoCopy = JSON.parse(JSON.stringify(todoData));
    todoCopy.loading = true;
    this.todos.push(todoCopy);

    this.newTodoText = '';
  }

  this.ref.detectChanges();
}

/**
 * Adds an todo log and save the todo as solved.
 * @param todo todo to solve
 */
async solveTodo(todo: any) {
  if (!todo.completed) {
    todo.loading = true;
    todo.completed = true;

    // save the todo using the queue
    this.queue.addQueueData(this.queueId, {
      taskId: this.contractId,
      listName: 'todologs',
      data: {
        id: todo.id,
        solved: true,
      },
    });
  }

  this.ref.detectChanges();
}
```

At the bottom of the `app.ts`, we included two functions of the old todo service:

```ts
	/**
	 * Get all remaining todos.
	 */
	public getRemaining() {
		return this.todos.filter((todo) => !todo.completed);
	}

	/**
	 * Get all completed todos.
	 */
	public getCompleted() {
		return this.todos.filter((todo) => todo.completed);
	}
```

The HTML file hasn't changed significantly. Some change and delete functions were removed and some loading and error checks were added:

```html
<evan-loading *ngIf="loading"></evan-loading>
<section class="todoapp" *ngIf="!loading">
	<ng-container *ngIf="invalid">
		<header class="header">
			<h1>{{ '_tutorialtask.invalid-contract-address' | translate }}</h1>
		</header>
	</ng-container>
	<ng-container *ngIf="!invalid">
		<header class="header">
			<h1>{{ description.name }}</h1>
			<input class="new-todo" placeholder="What needs to be done?" autofocus="" [(ngModel)]="newTodoText" (keyup.enter)="addTodo()">
		</header>
		<section class="main" *ngIf="todos.length > 0">
			<ul class="todo-list">
				<li *ngFor="let todo of todos"
					[class.completed]="todo.completed">
					<div class="view" flex>
						<input class="toggle" type="checkbox"
							(click)="solveTodo(todo)"
							[readonly]="todo.completed"
							[checked]="todo.completed">
						<label>{{todo.title}}</label>
						<ion-spinner class="todo-loading" color="light" *ngIf="todo.loading"></ion-spinner>
					</div>
				</li>
			</ul>
		</section>
		<footer class="footer" *ngIf="todos.length > 0">
			<span class="todo-count"><strong>{{ getRemaining().length }}</strong> {{ getRemaining().length == 1 ? 'item' : 'items' }} left</span>
		</footer>
	</ng-container>
</section>
```

# 5. Finished
Now you can enjoy your task application.

[![Finished](/docs/4000_developers/4300_ui/4340_angular/img/todo_finished.png){:width="100%"}](/docs/4000_developers/4300_ui/4340_angular/img/todo_finished.png)
