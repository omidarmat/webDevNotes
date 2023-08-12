# **A first look at react**

We will talk about:

1. Why we need something like React?
2. What React is and how it compares to Vanilla JavaScript?
3. What are different options for setting up a new React application?
4. Use a tool called `Create-React_App` to build our very first React project.

## **Why do front-end frameworks exist?**

So why not simply use Vanilla JavaScript to build our applications?

Before around 2010 all websites were **server-side rendered** websites. A website is assembled on the backend based on data and templates. The resulting HTML, CSS, and JavaScript code is then sent to the client-side. The browser then takes this code and paints it to the screen. All websites built with Wordpress are of this kind. The JavaScript used in this kind of websites was initially only to add some simple dynamics to the page, like simple animations, hover effects, and other stuff. Usually a popular library called **jQuery** was used for this purpose.

However, developers started to write more and more JavaScript code to be executed by the browser, and this led to fully fledged web applications which then led to the rise of so-called **single-page applications**. These are webpages that are rendered on the client and not on the server.

In client-side rendering, the process of rendering a webpage is shifted from the server to the client. We call these not webpages anymore, but **web applications**. A web application gets its data from the backend, usually by consuming an **API**. The application renders the screen for each view of the application. This single-page application feels as if you were using a native desktop or phone application.

There are several problems with using Vanilla JavaScript for building large-scale applications. Keep in mind that building any front-end web application is all about **handling data** and **displaying data** in a user interface. The most important task of a single-page application (and really of any application and website) is to keep the user interface in sync with the data, or in other words, to make sure that the UI always displays the current state of the data. This have proved to be a hard task to perform! Without a framework, it would be virtually impossible to keep the huge amount of data in an application in sync with a super-complex UI. Why?

1. Building a complex front-end with Vanilla JavaScript alone requires large amount of direct **DOM traversing and manipulation**, and this will lead to a huge mess of spaghetti code.
2. In Vanilla JavaScript apps, **states** such as simple text or numbers are often simply **stored right in the DOM**, right in the HTML elements themselves rather in a central place in the application. This results in many part of the app accessing and changing that DOM state directly. This will introduce many bugs into our application.

So in conclusion, this is manly why framworks exist:

1. Keeping a user interface in sync with data is really hard and takes a lot of work.
2. Frameworks enforce a correct way of structuring and writing code, therefore contributing to solving the problem of spaghetti code.
3. Frameworks give developers and teams a consistent way of building front-end applications.

## **What is React?**

React is a JavaScript library for building user interfaces. But let's extend this definition. React is an extremely **popular**, **declarative**, **component-based**, **state-driven** JavaScript library for building user interfaces, created by Facebook.

- **Based on components:** components are the building blocks of user interfaces in React, such as buttons, input fields, search bars and so on. Basically, what React does is to take components and draw them on webpages. We build complex UIs by building and combining multiple components.
- **Declarative:** We describe how components look like and how they work using a declarative syntax called **JSX**. So React is a huge abstraction away from the DOM, we never touch the DOM. JSX is a syntax that combines HTML, CSS, JavaScript, as well as referncing other components. If we never touch the DOM, how does React update the UI? This is where state comes to play.
- **State-driven:** React keeps the data in sync with the UI. Let's call this data "state" from now on. Whenever the state changes, we manually update the state in our application, and React will automatically re-render the UI to reflect the latest state. In other words, React actually reacts to state changes by re-rendering the UI.
- **JavaScript library:** React is actually just a JavaScript library. React is only the **view** layer. We need to pick multiple external libraries to build a complete application, for instance, for routing or for data fetching. To address this issue, multiple frameworks have been built on top of React, such as **NextJS** and **Remix**.

## **Setting up a new React project: The options**

The two options that are available for setting up a react project:

1. **Create-React-App tool:** a complete starter kit for React applications. The nice thing about this is that everything is already configured in it: An app created with this tool automatically comes with a development server, webpack for module bundling, and important developer tools such as ESLint, Prettier, Jest, Babel, etc. The problem with this tool is that it was built many years ago, and uses some slow and **outdated technologies** like webpack. So don't use this tool for real-world projects anymore. Only use for tutorials or experiments.
2. **Vite build tool:** use this tool for **real-world applications**. It is a modern build tool that contains a template for setting up React applications. This needs you to manually set up ESLint and other things. This can go wrong sometimes. So why use Vite? For its extremely fast page refreshment when the code changes. This is called **Hot Module Replacement (HMR)**. Also bundling is extremely fast in Vite.

But we also have other options in addition to the two options mentioned above. It is to use a React framework like **NextJS** or **Remix**. A framework like NextJS contains solutions for things like routing, data fetching, and server-side rendering, which are things that React itself does not provide easily out of the box. So a React framework is something built on top of React and makes it even easier to build applications.

This sounds great, but only for some applications. **Vanilla React applications** are still very important. It only makes sense to use React frameworks for building actual products, not for learning React.

### **Setting up a project with `create-react-app`**

Here are the steps you should follow:

1. Open up the command prompt and navigate to the directory where you want to start your project. Then type this command:

```
npx create-react-app@5 <project-name>
```

This will create a new folder with the project name defined in the command. It will also download a lot of files which will take a few minutes. As a result, you will see in the newly created folder a structured set of files and folders. This structure is designed in this way because developers thought it was the best possible structure. But it could be completely different.

```
- node_modules (dir)
- public (dir)
- src (dir)
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
    reportWebVitals.js
    setupTests.js
.gitignore
package.lock.json
package.json
```

In the `src` folder we have some files that we don't need and we will get rid of.

The `public` folder contains all the assets that will end up in the final application, such as all the images and an `index.html` file that contains a `<div>` element with the id `root`.
