---
title: "Advanced: Angular Task"
---
# Task DApp
This example shows how an evan.network featured DApp behaves and how it can interact with contracts. With the help of a Task DApp it is easy to show how a contract can be created, read out, adapted and how different data sets can be saved.

This example is explained using [TodoMVC Angular](http://todomvc.com/examples/angular2), to focus on functional implementations of blockchain interactions and less with angular. It also shows, how to migrate a classicaly angular application to an evan.network featured DApp.

**Before performing this example, please go through the [Angular - Hello World](/dapps/angular/hello-world) tutorial, as this tutorial is based on the Hello World example.** 

## 1. Project Setup
So, where do we start?

In the [Angular - Hello World](/dapps/angular/hello-world) it was already shown how evan.network apps are structured and how they are built and deployed. We will now integrate the TodoMVC example into this project structure. If you don't want to play the complete example yourself, you can find the finished application in the folder "dapps/task-complete".

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

