# **Back-end theory**

## **Web server**

A web server is actually an application that can listen for requests and respond to them. The request is sent by a client (browser) when we enter a certain URL in it. Once the request hits the server, an event is fired, which triggers a response from the server. The server application is usually designed to respond in different ways to different request URLs (refer to [**Routing**](#routing)).

### **Routing**

Routing basically means implementing different actions for different URLs. So we should be able to detect differences in the request URL and act based on it.

In huge applications, routing can become very complicated, and for these situations, we might use a NodeJS library called [**Express**](#express-module).

For simpler routing in practice projects we can use NodeJS itself and also the [**URL**](#url-module) core module, which enables us to analyse the request URL.

### **HTTP headers**

an HTTP header is a piece of information about the response or the request. There are many different standard response headers that we can define to inform the client about the response and what should be done about it.

#### **Standard response headers**

1. **`'Content-type'`**: defines the format of the response that is being sent to the client. 'text/html' or 'application/json'.

### **Query**

Query is a series of characters inserted into the request URL after a `?` mark, determining different parameters in the URL that can be used by the server to decide and act upon.

```
Request URL:
127.0.0.1:8000/product?id=0
```

## **API**

An API is a service from which we can request some data.

## **JSON**

JSON is a text format that is very similar to a JavaScript object. It can include formats similar to JavaScript data structures, like arrays and objects. But in order for a JSON data to be usable in JavaScript, it should first be parsed into actual JavaScript data structures.

```js
const parsedData = JSON.parse(jsonData);
```

# **Introduction to NodeJS**

NodeJS is a **JavaScript runtime** built on Google's open-source **V8 JavaScript engine**.

- **JavaScript runtime:** when using JavaScript in a browser, the browser is the JavaScript runtime. NodeJS is another JavaScript runtime that allows us to execute JavaScript code outside of browser. It acts as an environment in which a JavaScript program can be executed.
- **V8 JavaScript engine**: Actually executes the JavaScript code in NodeJS runtime. It is where JavaScript code is parsed and executed.

Having JavaScript outside of a browser in a stand-alone environment (NodeJS), we can do things that are completely impossible when JavaScript is limited to the browser, like accessing the file system and networking capabilities. This makes NodeJS a great candidate to be used as a web server, and therefore on the server-side of web development.

## **NodeJS advantages**

1. NodeJS is **single-threaded** and based on an **event-driven**, **non-blocking I/O model**, making it very light-weight and efficient.

   - In NodeJS `process`, which is where our application runs, there is only one single thread (i.e. where our code is executed in the machine's processor). All users accessing our application will use the same single thread. In this situation, if one user make the application run a synchronous code, all other users would have to wait until that code is done executing before they could use the application. This is why we developers use lots of asynchronous code, and therefore, callbacks in NodeJS applications in order to implement the non-blocking I/O model. In this approach, we off-load heavy tasks to background processes, so that all users can use the application at the same time, without blocking each other. After the background processes are done, specified callbacks will be called to act in the main execution thread. This is what makes NodeJS applications hightly performant and scalable. However, while using lots of callbacks, we should always avoid **callback hell** using ES6 **promises** or ES8 **async/await**.

2. NodeJS is perfect for building fast and scalable data-intensive applications. Therefore, NodeJS can be used to build:

   - API with database behind it (preferably NoSQL)
   - Data streaming (like YouTube)
   - Real-time chat application
   - Server-side web application

> **_Note_** | In some cases, where the application needs to perform super heavey server-side processing, NodeJS is not a good choice. These include image manipulations, video conversion, file compression, etc. For these cases, we usually use Python, PHP, Rybu on Rails, etc.

> **_Note_** | Companies like Netflix, Uber, PayPal, Ebay, and many others have started using Node in production.

3. There is a huge library of open-source packages (NPM) available.
4. NodeJS has a very active developer community.

## **Running JavaScript outside the browser**

### **Interacting with Node in Terminal**

In order to start working with Node in the terminal (VS Code) we use the `node` command in the termina. This will open Node REPL (Read, Eval, Print, Loop).

```
node
```

This enables us to write normal JavaScript code in the terminal.

For instance, we can define a variable:

```
const name = 'omid'
```

Then we can retrieve the value of this variable by writing its name:

```
name
```

We can also do any type of expression:

```js
7 + 3; //returns 10
```

We can use `_` as a variable that holds our last numeric result. For instance, after the calculation example above, `_` holds 10.

To exit REPL, there are different ways. We can use `.exit` command or press `Ctrl+d`.

```
.exit
```

By pressing the Tab key on the keyboard, Node lists all the global variables that are available. We can also see `fs` and `crypto` in this list, which are two important Node modules.

Also, by pressing the Tab key after writing a constructor function like `String.` in the terminal, a list of methods available on this constructor will be printed.

### **Creating a Node application**

We create a JavaScript file where we then write some JavaScript code. In order to execute this JavaScript file, we need to type the `node` command in the terminal, and after that, write the name of the file that we want to execute.

**`index.js`:**

```js
const hello = "Hello world";
console.log(hello);
```

**Terminal**:

```
node index.js
```

After the file is executed, the execution process is stopped, simply because there is nothing left to run in this file. (This will be explained in detail later)

## **Introduction to NodeJS modules**

In NodeJS, we have 3 types of modules:

**1. Core modules:** these are modules that are already installed on NodeJS and we can use them simply by requiring them into a script file.

```js
const <variable-name> = require('<module-name>');
```

**2. Our own modules:** Every single JavaScript file in a NodeJS application is treated as a module. Modules are used in NodeJS to export functionalities form one module and import them into another module.

There are different ways of exporting from a module.

- **`module.exports`:** in each module, we have access to a variable called `module`, and then we have access to a property called `exports` on that variable. We can then set this property to whatever we want to export.

```js
// Exporting from 'module-1.js'
module.exports = (argument) => {
  console.log(`function that acts on ${arguments}`);
};
```

```js
// Importing to 'index.js'
const module1 = require("./modules/module-1");
```

**3. 3rd-Party modules:**

## **NodeJS core and 3rd-party modules**

### **FS module**

**`core`**

This core module allows us to interact with files in the file system using a Node application.

In order to use FS module in a Node application, we first need to `require` it in a specific JavaScript file.

```js
const fs = require("fs");
```

#### **Reading files**

In order to read files with the FS module, we can use two FS functions:

**`.readFileSync()`**: this is the synchronous version of FS reading functionality.

- Accpets two arguments:

  1. Path to the file that is going to be read.
  2. Character encoding of the file: this is usually `utf-8` if the file only contains english language characters.

- Returns the content of the file.

```js
const textIn = fs.readFileSync("./txt/input.txt", "uft-8");
```

**`.readFile()`**: this is the asynchronous version of FS reading functionality.

- Accpets two arguments:

  1. Path to the file that is going to be read.
  2. Character encoding of the file.
  3. Callback function: has access to two arguments.

     - error
     - data

- Returns the content of the file.

```js
const textIn = fs.readFile("./txt/input.txt", "utf-8", (err, data) => {
  if (err) return console.log(err);
  console.log(data);
});
```

> **_Note_** | the `./` characters at the beginning of the file path refers to the location where we are running the terminal. So if we run the terminal in the root folder of our project, everything is fine, but if we run it somewhere else, for instance, on the desktop, then `./` will represent the desktop location. The solution to this problem is a variable called `__dirname`. This variable always refer to the location where the script that is being executed is located.
>
> ```js
> fs.readFile(`${__dirname}/txt/input.txt`);
> ```
>
> Exception to this rule is the `require()` function. The `./` characters in the file path passed into this function always translates to the directory of the script that is being executed, and not to where we are running the terminal.

> **_Note_** | in case the content of a file should be sent back as a response to a request sent by the client, it is more efficient to perform the reading process **synchronously** before the server is even created. We would read and store the content of the file into a variable, and the web server would simply send the content that is already read.

#### **Writing files**

In this situation, we usually produce or already have a data that we want to write into a file.

**`.writeFileSync()`**: this is the synchronous version of FS writing functionality.

- Accpets two arguments:

  1. Path to the file that is going to be written into. If the output file does not exist in the file system, the function will automatically create it for us.
  2. Data that is going to be written. Can be a variable holding the data.

```js
const textIn = fs.writeFileSync("./txt/input.txt", "uft-8");
const textOut = `This is what we know about Avocado: ${textIn}\nCreated on ${Date.now()}`;

fs.writeFileSync("./txt/output.txt", textOut);
```

**`.writeFile()`**: this is the asynchronous version of FS writing functionality.

- Accpets two arguments:

1. Path to the file that is going to be written into. If the output file does not exist in the file system, the function will automatically create it for us.
2. Data that is going to be written. Can be a variable holding the data.
3. Character encoding of the output file
4. Callback function: has access to one argument, which is the error object, if an error happens in the writing process.

```js
const textOut = "This is what we know about Avocado";

fs.writeFile("./txt/output.txt", textOut, "utf-8", (err) => {
  console.log("File written.");
});
```

### **HTTP module**

**`core`**

This core module enables networking capabilities for us.

In order to use FS module in a Node application, we first need to `require` it in a specific JavaScript file.

```js
const http = require("http");
```

#### **Creating a web server**

A web server is actually an application that can listen for requests and respond to them. (refer to [web server](#web-server) and [Routing](#routing))

We should create a JavaScript file and in there, we create a web server. Creating a web server basically includes 2 steps:

1. Creating a server using the `.createServer()` method on the `http` module. The method accepts a callback function that gets called whenever a request hits the server. This callback function has access to 2 arguments:

   - Request object: includes all kinds of stuff like the request URL, request headers, etc.
   - Response object: includes a bunch of tools for sending out the response, like `.end()` method.

```js
const server = http.createServer((req, res) => {
  res.end("Hello from the server!");
});
```

The method finally returns the server that we can store in a variable.

2. Starting a server, so that we can listen to incomming requests. To do this we call the `.listen()` method on the server that we created. The method accepts three arguments:
   - Port number: the port is a sub-address on a certain host. We usually use 8000 or other numbers.
   - Host: it is the IP address of the host. If we skip defining this parameter, it will by default be set to local host, but we can also explicitly define the local host for it. The standard IP address for local host is `127.0.0.1`.
   - Callback function (optional): it is called as soon as the server starts.

```js
server.listen(8000, "127.0.0.1", () => {
  console.log("Listening to incoming requests");
});
```

Now we have to run this JavaScript file in the terminal.

```js
node index.js
// Listening to incoming requests
```

This will execute the server codes we wrote, and as a result, the file will keep running becasue we have told it to listen for requests. It is the **event loop** that prevents the execution from stopping. We can now go to the browser and enter URL `127.0.0.1:8000`. The browser will then show the respond we designed for any request that hits our server:

```
Hello from the server!
```

> **_Note_** | if now we change something in the code, we would have to use the terminal to stop the application from running (`Ctrl+c`), and then execute it again. This reset process can be done automatically by an NPM package called **nodemon**.

#### **Methods for sending response**

**`.writeHead()`**: used to set status code and setting response headers. (refer to [HTTP headers](#http-headers))

- Receives 2 arguments:

  1. status code
  2. response headers: should be passed into the method as an object.

```js
res.writeHead(404);
res.writeHead(404, {
  "Content-type": "text/html", // client will now expect an HTML response.
});
```

> **_Note_** | headers should always be defined before the response is sent, for example using the `.end()` method.

**`.end()`**: used to send plain text responses. Receives a string that will be sent to the client as response.

### **URL module**

**`core`**

This core module enables us to analyze the request URL, in order to parse different paramteres from the URL into an object.

In order to use URL module in a Node application, we first need to `require` it in a specific JavaScript file.

```js
const url = require("url");
```

#### **Inspecting the request URL**

Whenever a request hits the server, we have access to a `url` property on the request object. So we can inspect it wherever we have access to the request object, like in the callback function of the [`.createServer()`](#creating-a-web-server) method.

`req.url` contains the piece of URL after the host address, starting with a slash character. For instance, `127.0.0.1:8000/overview` will be represented by `req.url` as `/overview`.

```js
const server = http.createServer((req, res) => {
  console.log(req.url);
  // returns:
  // /
  // /favicon.ico
});
```

#### **Parse URL parameters**

In order capture URL paramaters and store them in variables in an object we can use the `.parse()` method from the `url` module. The method accepts first, the request URL, and second, a boolean value determining whether or not to parse the [query](#query) into an object.

```
Request URL:
127.0.0.1:8000/product?id=0
```

```js
const query = url.parse(req.url, true);
console.log(query);
// Query: {id: '0'}
// pathname: '/product'
```

This returns an object in which there are many properties including a `Query` property, which itself is an object, containing the parameters specified in the URL. It also includes a `pathname` property containing the path after the host address.

### **Express module**

Information will be added soon.

## **HTML templating**

HTML templating mainly includes updating parts of an HTML file based on data provided by a server. The updated HTML file is then sent back by the server to the client as a response to a specific request.

In practice, we implement some placeholders in the HTML file that will get replaced dynamically by data coming from the server. The placeholder can be any set of characters. It just has to be something that is unique throughout the HTML code, so that it could be detected and replaced easily with code.

For instance, If we have this HTML code:

```html
<h2 class="product__name">Fresh Avocados</h2>
```

We can implement placeholders like this:

```html
<h2 class="product__name">{%PRODUCTNAME}</h2>
```

> **_Note_** | replacements can be done all over the HTML file. There is no limit. It can also be done for class names. The HTML file is just a text file. So if we can detect a special string anywhere in the HTML, we can replace it with anything.

### **Replacing class names**

This is usually used to make an HTML element appear/disappear according to data coming from the server. In involves using placeholders for class names:

```html
<div class="product__organic"><h5>Organic</h5></div>
<div class="product__organic {%NOT_ORGANIC%}"><h5>Organic</h5></div>
```

### **Templating for unknown amount of data**

In case we want to render a webpage that presents a certain number of things, but we don't know how many things, we can make a template file for one single thing, and then implement a placeholder in the HTML file where all things are going to be rendered. This placeholder will be replaced by a string built through template-rendering one thing after another.
