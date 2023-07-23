- [**Working with Part framework**](#working-with-part-framework)
  - [**Project file structure**](#project-file-structure)
  - [**Defining controllers**](#defining-controllers)
    - [**`package.json`**](#packagejson)
    - [**`index.js`**](#indexjs)
    - [**`config.js`**](#configjs)
      - [**Access request and response objects**](#access-request-and-response-objects)
      - [**Access data coming from request body**](#access-data-coming-from-request-body)
      - [**Access URL parameters**](#access-url-parameters)
      - [**All access options**](#all-access-options)
  - [**Defining routes**](#defining-routes)
  - [**Starting a server**](#starting-a-server)

# **Working with Part framework**

In a very brief introduction, working with Part framrwork involves 4 main steps:

1. Installing the Part framework using the company's local NPM registery:

```
npm install partFramework@10.15.0-alpha.3 --registry http://npm.partdp.ir
```

2. Defining [**controllers**](#defining-controllers).
3. Defining [**routes**](#defining-routes).
4. Starting a [**server**](#starting-a-server).

Let's now dive a bit deeper into each step, but before that, let's take a look at a regular file structure that we may need to follow in any project that is going to be developed using the Part framework.

## **Project file structure**

In order to start a project that is going to be developed using the Part framework, we need to create a root folder in which a list of other necessary folders should be included:

- configs [folder]
- controllers [folder]
  - testController [folder]
    - config.js [file]
    - index.js [file]
    - package.json [file]
- logs [folder]
- middleware [folder]
- models [folder]
- node_modules [folder]
  - partFramework [folder]
- test [folder]
- index.js [file]
- package.json [file]
- package-lock.json [file]
- pfw-config.js [file]
- routes.js [file]
- External Libraries [folder]
- Scratches and Consoles [folder]

The _controllers_ folder will contain other sub-folders, each defining a specific controller as a separate **package**. Each controller (sub-folder) should contain a `config.js` file, an `index.js` file, and a `package.json` file. Remember that these file should be able to automatically locate each other using identical names.

The `node_modules` folder will contain the Part framework package along with any other package that we will need throughout the development process, such as `@partFramework/http`.

The `index.js` file in the root folder will contain all the code related to initializing the Part framework. The `routes.js` file will contain all route definitions of our project.

> The `pfw-config.js` file is a configuration file for Part framework that we normally leave it untouched and just pass it into the Part framework instantiation process.

## **Defining controllers**

As explained before, each controller should be defined as a sub-folder inside the `controllers` folder of the project. This sub-folder should have a fully lowercase name. (e.g. `userscontroller`)

Let's now see what should each controller (sub-folder) contain.

### **`package.json`**

This file should refer to the exact same controller folder name in the `name` field. Also, its `main` field should refer to the file which is intended to act as the entry point of the controller (usually `index.js`).

```json
{
  "name": "userscontroller",
  "version": "1.0.0",
  "description": "Some description",
  "main": "index.js",
  "scripts": {},
  "author": "",
  "license": "ISC"
}
```

### **`index.js`**

Within this file, Part's `baseController` is usually required, and then **extended** by another class that has the exact same name of the controller folder name. Inside this extending class, we should define all controller functions related to this controller.

Finally, an object should be exported from this file. This object should contain a `controller` field set to the extending class, and an `introduceToLoader` field that uses the `.setProperties()` method on the `baseController` and passes a `config.js` filem, located in the controller folder.

```js
const baseController = require("@partFramework/baseController");

class usercontroller extends baseController {
  createUser(inputs) {}
  getUsers() {}
  getUser(inputs) {}
  updateUser(inputs) {}
  deleteUser(inputs) {}
}

module.exports = {
  controller: usercontroller,
  introduceToLoader: baseController.setProperties({
    config: require("./config.js"),
  }),
};
```

### **`config.js`**

The only thing we do in this file is to export an object that defines the controller name in a `name` field, and then in a `handlers` field, specifies the behavior of each controller function defined in the `index.js` file. What we mean by _behavior_ is that how will each controller function be able to act on data coming from the client.

A general structure of the object exported from this file will look like this:

```js
module.exports = {
  name: 'usercontroller', // exact same name as the controller folder
  handlers: {
    createUser: {
      needProtocolRef: false,
      params: ["_protocolRef.request.data"],
    },

    getUsers: {
      needProtocolRef: true,
      params: [],
    }

    getUser: {
      needProtocolRef: false,
      params: ["_inputData.params"]
    }

    updateUser: {
      needProtocolRef: false,
      params: ["_protocolRef.request.data"]
    }

    anyOtherFunction: {
      needProtocolRef: false,
      params: ["_protocolRef.request", "_protocolRef.response"]
    }
  }
}
```

#### **Access request and response objects**

In order for a controller function to have access to the request and response objects, we should set the `params` property for the handler to `["_protocolRef.request", "_protocolRef.response"]`.

| handler property  | value                                               |
| ----------------- | --------------------------------------------------- |
| `needProtocolRef` | false                                               |
| `params`          | `["_protocolRef.request", "_protocolRef.response"]` |

#### **Access data coming from request body**

In order for a controller function to have access to the data sent by the client in the request body, we should set the `params` property for the handler to `["_protocolRef.request.data"]`.

| handler property  | value                           |
| ----------------- | ------------------------------- |
| `needProtocolRef` | false                           |
| `params`          | `["_protocolRef.request.data"]` |

#### **Access URL parameters**

In order for a controller function to have access to the parameter values specified in the request URL, we should set the `params` property for the handler to `["_inputData.params"]`.

| handler property  | value                   |
| ----------------- | ----------------------- |
| `needProtocolRef` | false                   |
| `params`          | `["_inputData.params"]` |

#### **All access options**

Actually, there is a list of options that we can specify in the `params` field.

1. `_id`
2. `_protocolName`
3. `_protocolRef`:
   - request
     - data
   - response
4. `_route`
5. `_inputData`
   - params
6. `_ip`
7. `_domain`
8. `_hostName`
9. `_port`
10. `_session`

## **Defining routes**

Defining routes is normally done in the `routes.js` file located in the root of our project. The only thing we need to do in this file is to export a function that actually performs the routing job. This function receives a `router` object as its only argument. On this object we have access to a couple of methods:

- **`.setRoute()`:** This method accepts 2 arguments; first, a route defined as a string. Second, a callback function or the corresponding handler function defined in the controller. If it is going to refer to the corresponding handler function defined in the controller, it should be defined as a **string**.
- **`.method()`:** This method accepts 1 argument which is the HTTP method defined as a string.

This is how a simple `routs.js` file will look like:

```js
module.exports = (router) => {
  router.setRoute("/users", "usercontroller.createUser").method("POST");
  router.setRoute("/users/:id", "userscontroller.getUser").method("GET");
};
```

- **`.setGroup()`, `.prefix()`, `.controller()`:** These methods are used to group routes with the same root.

```js
module.exports = (router) => {
  router
    .setGroup(function () {
      router.setRoute("/", "testMethod_1").method("GET");
      router.setRoute("/:team/:name/:id", "testMethod_2").method("GET");
      router.setRoute("/", "testMethod_3").method("POST");
    })
    .prefix("/test")
    .controller("testcontroller");
};
```

## **Starting a server**

Operations needed for starting a server is usually implemented in a `index.js` file located inside the root of our project. This file should be referred to by a `package.json` file, also located at the root of our project. Inside the `index.js` file we need to use a **configuration file** which is called `pfw-config.js`. This file should also be located at the root of our project.

The `package.json` file will have to indicate our dependencies which are initially the two main packages that we need:

1. `partFramework`: currently at version 10.15.0-alpha.3
2. `@partFramework/http`: currently at version 1.11.4

In order to initialize the Part framework we should perform these steps:

1. `require('./partFramework')`.
2. `require('./pfw-config')`.
3. Create an instance of partFramework class, usually called `core`, by passing the pfw-config file into it.
4. Implement an `async` function, usually called `loadComponents` to pass the `controllers` folder of our project to the Part framework instance created in the previous step.
5. Implement an `async` function, usually called `start`, which first, initializes the Part frame work instance, second, passes the `servers` list from the `pfw-config.js` file into the `core`, and finally, loads our components by calling the `loadComponents` function defined in steo 4.
6. Finally we call the `start` function defined in step 5.

Here is a code example of all the steps above:

```js
const partFramework = require("partFramework");
const pfwConfig = require("./pfw-config");

const core = new partFramework(pfwConfig);

async function loadComponents() {
  await core.loader.loadControllersByPath("./controllers");
}

async function start() {
  await core.init();
  await core.loader.loadServers(pfwConfig.servers);
  await loadComponents();
}

start();
```
