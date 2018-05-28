---
title: "Angular - Task DApp Data-Contract"
---
# Angular - Task DApp Data-Contract
**Before performing this example, please go through the [Task DApp setup](/dapps/angular/task) tutorial, as this tutorial is based on this example.**

In this section you will create contracts, read from them and handle several data interactions with the contract by using the evan.network DataContract and the blockchain-core. So each data that is currently cached within the local storage will be moved into an contract.

For how to write the task dapp using your own contract implementation have a look at this: [Angular - Task DApp Custom Contract](/dapps/angular/task-custom).

If you dont want to code by yourself, you can simply read the docs and copy the final resulting src folder from [dapps/task-data-contract/src](https://github.com/evannetwork/dapps-tutorial-angular/tree/master/dapps/task-data-contract) to the [dapps/task/src](https://github.com/evannetwork/dapps-tutorial-angular/tree/master/dapps/task) folder.

# 1. Contract Implementation
Before your start your implementation, its important to decide what functionallities you need. You need to think about data parameters, user roles inclusive security restrictions and so on...

For this example we need a contract that handles some contract metadata and a list of todos. This is the perfect case for the [evan.network data contract](https://evannetwork.github.io/dev/data-contract) / [data contract wiki](https://github.com/evannetwork/blockchain-core/blob/feature/readthedocs-test/docs/data-contract.rst).

When you use a self implemented contract, its important to add the contract implementation abi to our dbcp.json definition file. In this case we can simply use the blockchain-core data-contract wrapper implementation to handle our contract calls. For documentation reasons, you should still put the abi definition of the data contract into the DBCP definition. So other people that read the DBCP definition of the created contract, automaticaly gets your contract definition and functions. So you can program against the contract from anywhere, also outside of your application.

So insert the abi definition into your dbcp.json file from the following [dbcp.json](https://github.com/evannetwork/dapps-tutorial-angular/blob/master/dapps/task-complete/dbcp.json) (its a bit large to insert the full abi here in the documentation).

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

# 2. Data Schema
The data schema is also a property of the dbcp.json, that describes the data structure of our contract in deep. In our case, the data schema will describe the data that is saved within our data contract's todo list.

```json
{
  ...
  "dataSchema": {
    "todo_list": {
      "$id": "todo_list_schema",
      "type": "array",
      "additionalProperties": false,
      "items": {
        "type": "object",
        "properties": {
          "completed": {
            "type": "boolean"
          },
          "_title": {
            "type": "string"
          }
        }
      }
    }
  }
  ...
}
```

# 3. Create and Read the Data Contract
The DApp will be designed to handle both side, the contract creation and the data consuming. The evan.network dashboard includes a dynamic parameter routing to open unregistered ens and contract addresses. So the DApp can check the current opened url, if a contract id or the normal ens address is opened. When the ens address is opened, we will redirect to an contract creation page. When a contract id is opened, the user gets redirected to the TodoMVC component.

To do this, you will need some new structures within your code:
  1. Contract service that handles contract creation
  2. Dispatcher to handle asynchroniously and page reload save contract interactions
  3. Contract creation component
  4. Routing for create and detail
  5. Create a new Task

## 3.1 Contract service
Create a new file within the services folder and name it "task.ts". Within this file we will declare all the functions that are needed to interact with "task contracts". To create a new data contract using the DBCP definition of our tutorial task only a view lines of code are needed. We will create a new dataContract instance and applying the loaded description to the dataContract create function.

```ts
  /**
   * Create a new task data contract instance.
   * @param name name of the task data contract
   */
  async createNewTask(name: string) {
    // create new data contract instance
    const dataContract = new DataContract({
      cryptoProvider: this.bccService.description.cryptoProvider,
      dfs: this.bccService.dfs,
      executor: this.bccService.executor,
      loader: this.bccService.contractLoader,
      nameResolver: this.bccService.nameResolver,
      sharing: this.bccService.sharing,
      web3: this.bccService.web3,
      description: this.bccService.description,
    });

    // load dapp description to add contract metadata
    const dappDescription = await this.descriptionService.getDescription(this.ensAddress, true);
    dappDescription.name = name;

    return await dataContract.create(
      'tasks',
      this.coreService.activeAccount(),
      this.descriptionService.getContractusENSAddress('taskboard'),
      { public: dappDescription }
    );
  }
```

After the contract was created, we want to write the reference into our favorites. The favorites DApp can not only handle DApps from ens addresses, it's also possible to load contracts with an underlying dbcp definition. To do this, require the angular-core "bookmark-service" and run the following functions. 

```ts
addToFavorites(task: any) {
  return this.bookmarkService
    .getBookmarkDefinition(task.address)
    .then(dapp => this.bookmarkService.queueAddBookmark(task.address, dapp))
}
```

## 3.2 Dispatcher
Depending on the block time and network connection, contract creation and interaction can leave a large gap in the usage time of the UI. To avoid a blocking frontend, so-called "dispatchers" are used. Dispatchers are defined and exported by the DApp as an angular module. So the dispatchers themselves can use the services of the DApp and at the same time the evan.network Angular framework can restart them even after a page load. For this purpose, the contract functions are not executed directly in the components, but only a new dispatcher task is inserted into the evan.network queue. The queue then independently handles the processing of the queued orders. The UI is provided with various options for listening to the processing of a queue.

If a dispatcher fails, the error is caught by the framework and an error is displayed in the top right corner of the UI. With this button the task can be repeated or deleted via the synchronization details.

Create a new folder within your DApp and call it "dispatcher". Create new file called "task-dispatcher.ts" and insert the following code:

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
      '_dapptaskboard.dispatcher.create-task',
      '_dapptaskboard.dispatcher.create-task-description',
      async (service: TaskService, queueEntry: any) => {
        const tasks = queueEntry.data;
        const results = [ ];
        
        for (let task of tasks) {
          // create new task
          const newTask = await service.createNewTask(task.name);

          // reference to my favorites
          await service.addToFavorites(newTask);

          results.push(results);
        }

        return results;
      }
    )
  ],
  translations,
  'TaskService'
);
```

Some "angular-core" classes for the queue are imported to create a new dispatcher with several sequences. Each dispatcher can have n* sequences, that will be runned after another. If one sequence is solved, the return values are saved for the next sequence. So when the user reloads the browser during the sequence 3/5, the queue will continue when page is loaded with the stept 3/5.

Only one service can be injected to a QueueDispatcher. In this case, the TaskService will contain all the functions that our Dispatcher needs.

After you create the new awesome Dispatcher, you need to export the service and dispatcher within the index ts and you will need to create a new module with the name "DispatcherModule". Now the meaning of the function "module(getConfig(true))" can also be explained. Components and some modules may only be added in an angular module in a zone.js scope. If we took the standard module for the dispatcher and the queue would try to analyze this module again, we would run into various errors. To avoid this, we add another module here, the "DispatcherModul". Only special modules and services are registered in it. Thus, not a single component can be displayed with this module. However, services for our dispatcher can be exported there and inserted into the dispatcher. We get Angular runtime data in our dispatcher, regardless of which DApp has just started. So while the queue is running, the user can change DApps and reload the page. However, our data will be synchronized.

Add the following code to your index.ts:
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

## 3.3 Contract creation component
In this case, we only need to specify a name for our task and no other metadata is needed. If you want to add more metadata in future, the blockchain-core has some utlity functions for this.

Before we create our component, its important to create a easy bridge to trigger the task creation from anywhere. To do so, add the following to your TaskService:

```ts
...
@Injectable()
export class TaskService implements OnInit {
  public createQueueID: QueueId;
  public ensAddress: string;

  constructor(
    public descriptionService: ContractusDescriptionService,
    public queue: ContractusQueue,
    public bccService: ContractusBCCService,
    public coreService: ContractusCoreService,
    public bookmarkService: ContractusBookmarkService
  ) {
    this.ensAddress = this.descriptionService.getContractusENSAddress('tutorialtask');

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

This is required that the Angular Queue recognizes from which DApp the dispatcher must be loaded. This queue ID can be listened on immediately to see the end of processing.

So, navigate to the "task/src/components" folder and create the "create-task" folder, with the following structure:
- create-task
  - create-task.ts
  - create-task.html
  - create-task.scss

create-task.ts
```ts
import {
  Component, ChangeDetectorRef, OnInit, OnDestroy  // @angular/core
} from 'angular-libs';

import {
  ContractusQueue
} from 'angular-core';

import {
  TaskService
} from '../../services/task';

/**************************************************************************************************/

@Component({
  selector: 'task-create',
  templateUrl: './task-create.html'
})
export class TaskCreateComponent implements OnInit, OnDestroy {
  public taskName = '';
  public contractId: string;
  
  private onCreation: Function;
  
  constructor(
    public ref: ChangeDetectorRef,
    public taskService: TaskService,
    public queue: ContractusQueue
  ) { }

  async ngOnInit() {
    this.onCreation = await this.queue
      .onQueueFinish(this.taskService.createQueueID, (reload) => {
        this.contractId = reload;
      });
  }

  ngOnDestroy() {
    this.onCreation && this.onCreation();
  }
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
        (ngModelChange)="ref.detectChanges()">
      <button ion-button outline round
        (click)="taskService.triggerTaskQueue(taskName)"
        [disabled]="!taskName">
        {{ '_tutorialtask.task-create' | translate }}
      </button>
    </div>
  </header>
</section>
```

We just reference the TaskCreate service in our component, so the code of the componet is very small. Also, we can use the queue.onQueueFinish and the createQueueID to listen for task creation finish.

## 3.4 Routing
To handle the routing correctly for the creation and task detail, we need to add some new routing. In the case, that we are opening the ens address of the DApp directly, the create component should be displayed. When the DApp is opened using a contract address, we should directly open the task detail component. Adjust the routing to the following:

```ts
function getRoutes(): Routes {
  // Defines the root route, fallback routes and applies the contractus default routes to handle
  // queue, mailbox and anything else within this application
  return RoutesBuilder.buildModuleRoutes(
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

## 3.5 Create task
After setting up the new components and the structures for the dispatcher, it is possible to create a new contract via our DApp.

If we were to do that now, however, we would have a problem. The DApp is not currently deployed to any ENS path, so the public.dapp.origin ipfs path of dbcp.json does not point to the correct value. To fix this, we need a valid IPFS path. This can be based on the "Deploy to contract" manual of the lerna project. Navigate to the root level of the Lerna project and execute the following command to start an IPFS deamon:
```sh
"./scripts/go-ipfs.sh".
```

After starting the ipfs, navigate to the "dapps/task" folder and execute the following command:
```sh
"ipfs add -r dist"
```

It should result something similar:
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

Copy the latest ipfs path for the dist folder ("QmXCnDwasWd9JQ3rz7Rjc3uQt7SDiuryzWAXerPdL4KHTs") and replace the origin within your dbcp.json file.

**Now you can create a new contract instance. Reload your browser and try it.**


# 4. Task detail

