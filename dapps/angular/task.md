---
title: "Advanced: Angular Task"
---
# Task DApp
**Before performing this example, please go through the [Angular - Hello World](/dapps/angular/hello-world) tutorial, as this tutorial is based on the Hello World example.** 

This example shows how an evan.network featured DApp behaves and how it can interact with contracts. With the help of a Task DApp it is easy to show how a contract can be created, read out, adapted and how different data sets can be saved.

This case is explained using [TodoMVC Angular](http://todomvc.com/examples/angular2).

The Project Setup will explain how to integrate an existing Angular application into the existing evan.network structure. If you focus on functional implementations of blockchain interactions and less on angular, you can skip the first chapter by copying the src folder from [dapps/task-todomvc-integrated/src](https://github.com/evannetwork/dapps-tutorial-angular/tree/master/dapps/task-todomvc-integrated) to the [dapps/task/src](https://github.com/evannetwork/dapps-tutorial-angular/tree/master/dapps/task) folder.

If you dont want to code by yourself, you can simply read the docs and copy the final resulting src folder from [dapps/task-complete/src](https://github.com/evannetwork/dapps-tutorial-angular/tree/master/dapps/task-complete) to the [dapps/task/src](https://github.com/evannetwork/dapps-tutorial-angular/tree/master/dapps/task) folder.

## 1. Project Setup
So, where do we start?

In the [Angular - Hello World](/dapps/angular/hello-world) it was already shown how evan.network apps are structured and how they are built and deployed. We will now integrate the TodoMVC example into this project structure.

## 1.1 Seed project
To handle a smarter startup for you, a seed project already exists within the dapps folder. By having a look into the "dapps/task" folder, you will find a clear project with all configurations you will need. Its nearly the same as the Hello World sample, but without any components or services. This application is ready to use and you can already start it. Open two command lines and start the development environment:

```sh
npm run serve
```

```sh
npm run dapps-build
npm run dapps-serve
```

Before you have look into the application, add a cool img into public.imgSquare (use [https://www.base64-image.de/](https://www.base64-image.de) to format your img into a base64).

Now you can navigate to [http://localhost:3000/dev.html#/dashboard.evan/favorites](http://localhost:3000/dev.html#/dashboard.evan/favorites) to add your application as a new favorite. Click on "Add bookmark" and insert the name of your DApp, that is specified within the dbcp.json file (in this case "tutorialtask") and open it. There you will find an empty DApp that displays nothing more than an empty application. At this point we can start developing.


## 1.2 Insert TodoMVC
Download the [TodoMVC app](https://github.com/tastejs/todomvc/tree/master/examples/angular2) and have a look into the "examples/angular2" folder.
- services
  - store.js
  - store.ts
- app.html
- app.js
- app.ts
- bootstrap.js
- bootstrap.ts

At first, we see that the application is represented by one component and one service. We can ignore the js files, because the development environment build them for us together into one file. To migrate the componentent into our task, create a new folder "app" within the "task/src/components" folder and copy the "app.ts" and "app.html" into this folder. Also, copy the "services/store.ts" file into "task/src/services" folder.

## 1.3 Correct requirement loading and Angular 5
To load angular over the evan.network core libraries from IPFS you need to adjust the import command within the app component. Also, the path to our Todo service has changed. Take the following adjustments

```js
import {Component} from 'angular2/core';
import { TodoStore, Todo } from './services/store';
```

to 

```js
import {
	Component						  // @angular/core
} from 'angular-libs';

import {
	TodoStore,
	Todo
} from '../../services/store';
```

The angular-libs are existing within the node_modules of the task or rather within the lerna root node_modules. This folder is mapped within the tsconfig.json. Within the evan.network framework, the dapp-browser has the possibility during runtime to load the "angular-libs" from the ens path "angularlibs.evan". As a result of this, the libraries will not be build into your application to reduce redundant source code loading. The library will loaded from IPFS.

```json
{
  ...
  "paths": {
    ...
    "angular-libs": [
      "../node_modules/@evan.network/angular-libs/dist/angularlibs.js",
      "../../../node_modules/@evan.network/angular-libs/dist/angularlibs.js"
    ],
    ...
  }
  ...
}
```

To update the service for Angular 5 with more usage comfort, we will add the "@Injectable()" decorator to the service, change the "export default class TodoApp" of the TodoApp to "export class TodoApp" and also add the correct templateUrl. The headers of the two files will look like the following:

store.ts
```ts
import {
	Injectable						  // @angular/core
} from 'angular-libs';

...

@Injectable()
export class TodoStore {
  todos: Array<Todo>;
  
  ....
```

app.ts
```ts
@Component({
	selector: 'todo-app',
	templateUrl: './app.html'
})
export class TodoApp {
	newTodoText = '';

	constructor(
		public todoStore: TodoStore
  ) { }
...
```

A difference between Angular 2 and Angular 5 is the *ngFor statement. We need to change the *ngFor statement from

```html
*ngFor="#todo of todoStore.todos"
```

to

```html
*ngFor="let todo of todoStore.todos"
```

## 1.4 Add component and service to task module
Your console will log tons of errors. This is because the component and service are not registered in the Task Module. Open the "task/src/index.ts" file and add the imports.

index.ts
```ts
...
import { RootComponent } from './components/root/root';
import { TodoApp } from './components/app/app';

import { Translations } from './i18n/registry';
import { TodoStore } from './services/store';
...

function getConfig(isDispatcher?: boolean) {
  let config: any = {
    imports: [
      CommonModule,
      AngularCore
    ],
    // reference your services
    providers: [
      Translations,
      TodoStore // <======== add TodoStore
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
      TodoApp // <======== add TodoApp
    ];
  }

  return config;
}

...
```

## 1.5 Fix styling
After you applied this changes, the TodoMVC should run. Have a look at [tutorialtask](http://localhost:3000/dev.html#/dashboard.evan/tutorialtask).

[![TodoMVC first](/public/dapps/angular/task/todo_mvc_first.png){:width="200px"}](/public/dapps/angular/task/todo_mvc_first.png)

But wait, it looks like shit and its not working? Correct! We forgot to add the TodoMVC styling. Within the node_modules folder of the original TodoMVC folder, you will find a file "todomvc-app-css/index.css". Copy this file into the "task/src/scss" folder and rename it to "index.scss", so the build job will recognize it and will build it into the combined css file.

**Please keep in mind: This application runs integrated within the evan.network dashboard without any iframe. So global styles, will be realy global! So remove html, body styles and wrap the whole index.scss file within an selector that only select the TodoApp component. Its selector is "todo-app", so wrap the whole scss into this selector, so its only effective within your component.**

remove:
```scss
html, body {
  margin: 0;
  padding: 0;
}

body {
  font: 14px 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-weight: 300;
  line-height: 1.4em;

  min-width: 230px;
  max-width: 550px;
  margin: 0 auto;

  color: #4d4d4d;
  background: #f5f5f5;

  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

add:
```scss
todo-app {
  button {
    font-family: inherit;
    font-size: 100%;
    font-weight: inherit;
  
  ...
}
```

Add the following style at the start of the scss file for more evan.network compatibility:
```scss
@import '@evan.network/angular-sass/src/variables/colors';

todo-app {
  & {
    display: block;

    padding: 16px;

    @media (min-width: 1200px) {
      width: 70%;
      margin-left: 15%;
    }

    @media (min-width: 1500px) {
      width: 50%;
      margin-left: 25%;
    }
  }

  h1 {
    color: $text-color !important;
  }

  .new-todo, section, footer {
    background-color: $background-color !important;
  }

  section.main, footer.footer {
    border-top: 1px solid $background-color-2;
  }

  .todo-list {
    li {
      border-bottom: 1px solid $background-color-2 !important;

      .destroy {
        color: $text-color;

        &:hover {
          color: $red;
        }
      }
    }
  }

  footer.footer {
    height: 40px;

    background-color: $background-color !important;

    &:before {
      box-shadow: 0 1px 1px $background-color-2, 0 8px 0 -3px #023845, 0 9px 1px -3px $background-color-2, 0 16px 0 -6px #023845, 0 17px 2px -6px $background-color-2;
    }
  }

  .clear-completed {
    color: $text-color;
  }
}

...
}
```

## 1.6 Fix functionality
After you applied the correct styling, the application looks very good. But when you try to use it nothing will happen? This is correct! Try to add a new Todo and reload the browser and the new todos will be appear.

What is that? The evan.network Angular has a large list of dependencies and a the browser must perform a lot of heavy operations. To reduce performance issues, especially on mobile devices, the automatic change detection is disabled. So you can create maximum dynamic applications without any restrictions of AOT compiling. You can run any component directly, the evan.network Angular framework will create ng.factories during runtime and it will cache them for you for late usage, to speed up anything.

To keep the application running, you need to apply the Angular ChangeDetectorRef Service and enable the whole change detection for your application or you take the performance friendly way and implements manually change detection.

### 1.6.1 Enable Change Detection
Open the "task/src/components/root/root.ts" and remove the following line:

```ts
this.ref.detach();
```

### 1.6.2 Enable performance optimizations
Require the "ChangeDetectorRef" service from the angular-libs and implement the "this.ref.changeDetection()" call to any function that changes something within the ui.

```ts
import {
	Component, ChangeDetectorRef, OnInit  // @angular/core
} from 'angular-libs';

import {
	TodoStore,
	Todo
} from '../../services/store';

/**************************************************************************************************/

@Component({
	selector: 'todo-app',
	templateUrl: './app.html'
})
export class TodoApp {
	newTodoText = '';

	constructor(
		public todoStore: TodoStore,
		public ref: ChangeDetectorRef
	) { }

	stopEditing(todo: Todo, editedTitle: string) {
		todo.title = editedTitle;
		todo.editing = false;

		this.ref.detectChanges();
	}

	cancelEditingTodo(todo: Todo) {
		todo.editing = false;
		
		this.ref.detectChanges();
	}

	updateEditingTodo(todo: Todo, editedTitle: string) {
		editedTitle = editedTitle.trim();
		todo.editing = false;

		if (editedTitle.length === 0) {
			this.todoStore.remove(todo);

			return this.ref.detectChanges();
		}

		todo.title = editedTitle;
	}

	editTodo(todo: Todo) {
		todo.editing = true;

		this.ref.detectChanges();
	}

	removeCompleted() {
		this.todoStore.removeCompleted();

		this.ref.detectChanges();
	}

	toggleCompletion(todo: Todo) {
		this.todoStore.toggleCompletion(todo);

		this.ref.detectChanges();
	}

	remove(todo: Todo){
		this.todoStore.remove(todo);

		this.ref.detectChanges();
	}

	addTodo() {
		if (this.newTodoText.trim().length) {
			this.todoStore.add(this.newTodoText);
			this.newTodoText = '';
		}

		this.ref.detectChanges();
	}
}

```

## 1.7 Test it
Now the application is finally integrated and you can watch the result on the following URL: 
(http://localhost:3000/dev.html#/dashboard.evan/tutorialtask)

[![TodoMVC integrated](/public/dapps/angular/task/todo_mvc_integrated.png){:width="200px"}](/public/dapps/angular/task/todo_mvc_integrated.png)
