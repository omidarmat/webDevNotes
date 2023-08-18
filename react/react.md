- [**A first look at react**](#a-first-look-at-react)
  - [**Why do front-end frameworks exist?**](#why-do-front-end-frameworks-exist)
  - [**What is React?**](#what-is-react)
  - [**Setting up a new React project: The options**](#setting-up-a-new-react-project-the-options)
    - [**Setting up a project with `create-react-app`**](#setting-up-a-project-with-create-react-app)
- [**Core concepts of building React apps**](#core-concepts-of-building-react-apps)
  - [**JSX**](#jsx)
    - [**Declarative JSX**](#declarative-jsx)
      - [**Imperative appraoch**](#imperative-appraoch)
      - [**Declarative appraoch**](#declarative-appraoch)
    - [**Rules of JSX**](#rules-of-jsx)
    - [**Extracting JSX into a new component**](#extracting-jsx-into-a-new-component)
  - [**Components**](#components)
    - [**Rendering the `root` component and strict mode**](#rendering-the-root-component-and-strict-mode)
    - [**Creating and reusing a component**](#creating-and-reusing-a-component)
      - [**Using public assets in components**](#using-public-assets-in-components)
      - [**Implementing JavaScript logic in components**](#implementing-javascript-logic-in-components)
    - [**Moving components into separate files**](#moving-components-into-separate-files)
  - [**Props**](#props)
    - [**Props make one-way data flow**](#props-make-one-way-data-flow)
    - [**Passing and reciving props**](#passing-and-reciving-props)
      - [**Rendering lists with props**](#rendering-lists-with-props)
      - [**Conditional rendering**](#conditional-rendering)
        - [**With `&&`**](#with-)
        - [**With ternary operator**](#with-ternary-operator)
        - [**With multiple `return` statements**](#with-multiple-return-statements)
  - [**React Fragments**](#react-fragments)
  - [**Styling React applications**](#styling-react-applications)
    - [**Inline styling**](#inline-styling)
    - [**External CSS or Sass**](#external-css-or-sass)
    - [**CSS modules**](#css-modules)
    - [**Tailwind CSS**](#tailwind-css)
  - [**Separation of concerns in React**](#separation-of-concerns-in-react)
- [**State, Events and Forms interactive components**](#state-events-and-forms-interactive-components)
  - [**Handling events**](#handling-events)
  - [**State in React**](#state-in-react)
    - [**Mechanics of state**](#mechanics-of-state)
    - [**State guidelines**](#state-guidelines)
    - [**Working with a state variable**](#working-with-a-state-variable)
    - [**Forms and handling submissions**](#forms-and-handling-submissions)
      - [**Creating a form**](#creating-a-form)
      - [**Form Events**](#form-events)
      - [**Controlled elements**](#controlled-elements)
  - [**Review: State vs. Props**](#review-state-vs-props)
- [**React developer tools**](#react-developer-tools)
- [**Thinking in React**](#thinking-in-react)
  - [**State management**](#state-management)
    - [**Types of state**](#types-of-state)
    - [**When and where?**](#when-and-where)
    - [**Lifting state**](#lifting-state)
    - [**Derived state**](#derived-state)
  - [**Components**](#components-1)
    - [**Splitting a UI into components**](#splitting-a-ui-into-components)
      - [**When to create a new component?**](#when-to-create-a-new-component)
      - [**General guidelines**](#general-guidelines)
    - [**Component categories**](#component-categories)

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

1. **Create-React-App tool:** a complete starter kit for React applications. The nice thing about this is that everything is already configured in it: An app created with this tool automatically comes with a development server, Webpack for module bundling, and important developer tools such as ESLint, Prettier, Jest, Babel, etc. The problem with this tool is that it was built many years ago, and uses some slow and **outdated technologies** like Webpack. So don't use this tool for real-world projects anymore. Only use for tutorials or experiments.
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
    App.css //delete
    App.js
    App.test.js //delete
    index.css //delete
    index.js
    logo.svg //delete
    reportWebVitals.js //delete
    setupTests.js //delete
.gitignore
package.lock.json
package.json
```

In the `src` folder we have some files that we don't need and we will get rid of. So in order to create a project from scratch, we will select all files in this folder and delete them. This will make the application show you an error.

We will then create an `index.js` file in this folder. Remember that this file needs to be named `index.js` because **Webpack** expects the entry points to be called that. Inside this file, we will first import React:

```js
import React from "react";
import ReactDOM from "react-dom/client";
```

Next up, we will create our `App` component. It is not necessary to call it App, but it is necessary to start its name with a capital letter. From here on, you can go on to the [Core Concepts](#core-concepts-of-building-react-apps) section of this file.

The `public` folder contains all the assets that will end up in the final application, such as all the images and an `index.html` file that contains a `<div>` element with the id `root`. Remember that Webpack, which is the module bundler here, will automatically look into the `public` folder to find the assets of our application, such as images, etc.

# **Core concepts of building React apps**

We will talk about **Components**, **Props**, and **JSX**. We will learn how components are the building blocks of React applications and how to create and reuse them using the powerfull JSX syntax.

We will also share data between components using Props and learn about rendering **lists**, **conditional rendering**, and more. Looking at a React app, there is nothing that is not a component, or at least not inside of some component. As mentioned before, what React does is to basically take components and draw them on to a webpage. In technical terms, React renders a "View" for each component, and all these views together make up the UI.

It is important to remember that each component has its own:

1. Data (props)
2. JavaScript Logic
3. Appearance (JSX)

## **JSX**

JSX is a declarative syntax to describe how components look like and how they work based on their data and logic. In practice, this means that each component must return one block of JSX, which React will then use to render the component on the UI.

JSX is similar to HTML, but it is actually an extension of JavaScript that allows us to embed JavaScript, CSS, and React components into HTML.

If react is a JavaScript framework, how does it understand this HTML-looking code? Remember that JSX is an extension of JavaScript, which means that there is a simple way of converting JSX to JavaScript. This is done by **Babel**, which was automatically included in our application by `create-react-app`.

Each JSX element is converted to a `React.createElement()` function call. Remember that browsers don't understand JSX, they only understand HTML. So our JSX is converted into `createElement()` function calls, which in the end creates the HTML elements that we see on the screen.

### **Declarative JSX**

Let's first review what is imperative, in order to understand what is declarative.

#### **Imperative appraoch**

When we try to build UIs using Vanilla JavaScript we use an imperative approach. It means that we manually select elements, traverse the DOM, and attach event handlers to elements. Then as soon as an event happens, we give the browser a step-by-step instruction on how to mutate DOM until we reach the desired UI.

So in the imperative approach, we tell the browser exactly **how to do things**. However, doing this in a complex app is virtually impossible! So we use React in order to implement a declarative approach.

#### **Declarative appraoch**

Declarative approach means to describe what the UI should look like at all times, always based on the current data that is in the component. We know that this data is actually **props** and **state**. So basically, we JSX to describe the UI based on props and state. All this, happens without any DOM manipulation at all!

So in the declarative approach, we tell the browser **what we want to achieve**. It helps us developers to never think of touching the DOM. Instead, we should only think of the UI as a reflection of the current data.

### **Rules of JSX**

1. JSX works essentially like HTML, but we can enter JavaScript mode by using `{}`.
2. Inside the JavaScript mode, we can place any JavaScript expressions. Example: reference variables, create arrays or objects, `.map()`, ternary opertor. But statements are not allowed (`if/else`, `for`, `switch`)
3. A piece of JSX produces a JavaScript expression. By that we mean that this:

```js
const el = <h1>Hello React!</h1>;
```

is converted to:

```js
const el = React.createElement("h1", null, "Hello React!");
```

This fact has 2 important implications:

- We can place other pieces of JSX inside `{}`
- We can write JSX anywhere inside a component (in `if/else`, assign to variables, pass it into functions)

4. A piece of JSX can only have one, and exactly one root element. If you need more, use `<React.Fragment>`. Also note that when you open a `return` statement to return a JSX, you must always start with a JSX element. You cannot immediately enter JavaScript mode by `{}`. You will have to first open a `<div>` element, and then inside that, you can enter JavaScript mode.

### **Extracting JSX into a new component**

Let's talk on the `Footer` component example. As we notice that the JSX inside this component is growing too much, we can extract JSX into another component. We simply define another component that returns a JSX.

```js
function Order(props) {
  return (
    <div className="order">
      <p>
        We're open until {props.closeHour}:00. Come visit us or order online.
      </p>
      <button className="btn">Order</button>
    </div>
  );
}
```

We would obviously have to udpate the `Footer` component like this:

```js
function Footer() {
  const hour = new Date().getHours();
  const openHour = 12;
  const closeHour = 22;
  const isOpen = hour >= openHour && hour <= closeHour;
  console.log(isOpen);

  return (
    <footer className="footer">
      {isOpen ? (
        <Order closeHour={closeHour} />
      ) : (
        <p>
          We're happy to welcome you between {openHour} and {closeHour}
        </p>
      )}
    </footer>
  );
}
```

So we take out a part of the JSX, and replace it with the result of calling the `Order` component by passing the `closeHour` prop into it, because it depends on it.

## **Components**

Components are the most fundamental concepts in React. React applications are entirely made out of components. Each component is a self-contained piece of the UI which contains its own data, JS logic, and appearance (JSX).

In a real-world application, we can identify main components, and if we look with more precision, we can also identify some smaller components inside other major components. In React applications, it is very normal to **nest** components inside other components.

These nested components may be of the **list** type, which means that their appearance is the same, but their data is different. So they are actually the same component that is being reused to display varying information. This can be handled using **props** which enables us to pass data between components.

One thing that can help to analyze our components is the component tree which clarifies the hierarchy that exists between the components (parent and child components).

### **Rendering the `root` component and strict mode**

Inside the `index.js` file which we normally place inside the `src` folder of our project, we first import `React` and `ReactDOM` libraries.

```js
import React from "react";
import ReactDOM from "react-dom/client";
```

Then we add the first component which is usually called `App` and its name needs to start with a capital letter.

```js
function App() {
  return <h1>Hello React!</h1>;
}
```

Now in order to render this component to the DOM, we would have to use the `createRoot` method that is available on `ReactDOM`. This method receives as argument the `<div>` element with the ID `root` in the `index.html` file which is currently located in the `public` folder.

> We are not allowed to return more than one element in a single JSX. If we want to include more than one element, we would have to wrap them in one single parent element, like a `div`. This can also be handled using React [fragments]().

```js
const root = ReactDOM.createRoot(document.getElementById("root"));
```

Now this `root` object has the `render` method available on it, and we can use it to render our `App` component. The `render` method accepts JSX as argument.

```js
root.render(<App />);
```

Now to activate **strict mode**, we can do the rendering in another way. So instead of directly rendering the `App` component as the root component, we can wrap the `App` component inside a `React.StrictMode` component.

```js
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

The only thing that strict mode does is that during development, it will render our components twice to find certain bugs and to check if we are using outdated parts of the React API.

We can now start our project using the NPM command below, since it is already defined as an NPM script in the `package.json` file.

```
npm run start
```

### **Creating and reusing a component**

In React, we write new components using functions. Also, there are 2 important rules as we define components as functions.

1. The function name needs to start in **uppercase**.
2. The function needs to return some **markup**, usually in the form of JSX, but we can also return nothing, like `null`.

```js
function Pizza() {
  return <h2>Pizza</h2>;
}
```

Up until this point this component cannot appear in the UI since we are not incluing this new component anywhere. We can include this in our main component which is usually called `App`. This way we are actually **nesting** the `Pizza` component inside the `App` component.

```js
function App() {
  return <h1>Hello React!</h1><Pizza />;
}
```

> Nesting a component inside another component never means to write the child component's function inside the parent component function. The two functions should be written separately, but the child component will be called or inserted into the parent component as an element. Of course, React will still work if we put the child function inside the parent function, but it is a really bad practice.

But remember that each component can only return one element. So the `<h1>` and the `<Pizza />` element should be wrapped in another element, like a `<div>`.

```js
function App() {
  return (
    <div>
      <h1>Hello React!</h1>
      <Pizza />
    </div>
  );
}
```

The `Pizza` component is now **reusable**, meaning that we can include its returned JSX in any of our other components simply by inserting the `<Pizza />`. For now, this will re-render the `Pizza` component with the same data over and over, but we can update it each time we insert it by using [**props**](#using-props-in-a-component).

#### **Using public assets in components**

In order to use an image inside a component we include an `<img/>` tag in the `return` statement of the component. Note that if we are actually returning more than one elements, we should wrap them all in another whole `<div>` element.

```js
function Pizza() {
  return (
    <div>
      <img src="pizzas/spinaci.jpg" alt="Pizza spinaci" />
      <h2>Pizza Spinaci</h2>
      <p>Tomato, mozarella, spinach, and ricotta cheese</p>
    </div>
  );
}
```

> When writing the address to a specific image, you should consider the `public` folder as the root directory and start the image file path from that root.

#### **Implementing JavaScript logic in components**

This will include writing JavaScript logic in components. Until this point, we have already written some JavaScript logic, but it was only inside JSX. But since components are JavaScript functions, we can do any JavaScript code inside them.

```js
function Footer() {
  const hour = new Date().getHours();
  const openHour = 12;
  const closeHour = 22;
  const isOpen = hour >= openHour && hour <= closeHour;
  console.log(isOpen);

  return (
    <footer>{new Date().toLocaleTimeString()}, We're currently open!</footer>
  );
}
```

Notice how we have used regular JavaScript logic before returning the JSX. Also keep in mind that in order to implement JavaScript logic in JSX, we should always insert the JavaScript code inside `{}`.

> You will probably receive every result twice, and that is becasue of the strict mode.

### **Moving components into separate files**

We take the component code from the main `App.js` file and put it in a separate file in the `src` folder of our project. It is a good practice to call the new file with the same name as the component. For instance, if we are taking the `Logo` component to a separate file, we call the new file `Logo.js`.

Inside the `Logo.js` file we `export default` the component, and then import it in the main `App.js` file.

## **Props**

Up until this point, we have learned about a component's appearance and logic. We also know that React renders a component based on its current data and that the UI will always be in sync with that data. This data is made out of **props** and **state**. There are actually more, but for now these two matter.

State is **internal component data** that can be updated by the component's **logic**, while props is the data coming from the **parent component**, so from outside. So it is the parent component that owns the data, and therefore it cannot be modified by the child component. Props can only be updated by the parent component itself. So keep in mind that **Props are read-only, they are immutable**. Therefore, if you need to mutate props, you actually need state.

Why props are immutable? Because props are just simple objects. Mutating props would affect the parent component, that is how objects work in JavaScript. If you change an object that is located outside a function, that function has then created side effects. React is all about pure functions that don't produce side effects. Components have to be pure in terms of their props and state, because this allows React to optimize apps, avoid bugs, and make apps predictable.

Props essentially defines how we pass data between components, in particular, from parent components to child components. Props are an essential React tool to configure and to customize components. You can imagine props as settings that we can use to make a parent component control how its child components should look like. Props are just like function arguments passed to regular JavaScript functions.

### **Props make one-way data flow**

This means that in React applications, data can only be passed from parent to child components which happens by using props. There are multiple reasons thar React uses this one-way data flow:

1. Makes applications more predictable and easier to understand for developers.
2. Makes applications easier to debug, as we have more control over the data
3. This is more performant.

Now you might ask, what if I actually wanted to pass some state up to a parent component? There is a very clever way to do that, but we will learn that later.

### **Passing and reciving props**

To define props we do it in 2 steps:

1. Pass the props
2. Receive the props

Imagine we have a `Menu` component that is going to pass props into a `Pizza` component. This would the most basic way to implement:

```js
function Menu() {
  return (
    <main className="menu">
      <h2>Our menu</h2>
      <Pizza
        name="Pizza Spinaci"
        ingredients="Tomato, mozarella, spinach, and ricotta cheese"
        photoName="pizzas/spinaci.jpg"
        price={10}
      />
    </main>
  );
}
```

Notice how we have defined props similar to regular attributes in HTML.

> The order in which we define props as attributes is not important. Also note that you can insert anything as props. It is limited to strings or numbers. It can be objects, or even other React components. However, if you want to insert anything but strings, you should first enter JavaScript mode by typing `{}`.

Now the `Pizza` component will be able to receive these props in an object called `props`. The attributes will be available as properties on the `props` object.

```js
function Pizza(props) {
  return (
    <div>
      <img src={props.photoName} alt={props.name} />
      <h2>{props.name}</h2>
      <p>{props.ingredients}</p>
    </div>
  );
}
```

> The `props` object is always available on all components, but if we don't pass anything into a component as argument, it will simply be an empty object.

> We normally call a component in a JSX as a single-tag element. But we can call a component with opening and closing tags and also insert some text in between. This text is received by the component function as a parameter called `children`. Take the code below as an example. Here, the `Select` text content passed in between the opening and closing tags of `<Button>` is received by the `Button` component as the `children` parameter. This basically allows you to reuse a component multiple times throughout your project with different text contents.

```js
function Friend({ friend }) {
  return <Button>Select</Button>;
}

function Button({ children }) {
  return <button className="button">{children}</button>;
}
```

#### **Rendering lists with props**

Rendering a list is when we have an array and we want to render an element for each component of the array. We will continue the example mentioned above for this use case.

We should now update the `Menu` component we defined in the example above:

```js
function Menu() {
  return (
    <main className="menu">
      <h2>Our menu</h2>
      <ul>
        {pizzaData.map((pizza) => (
          <Pizza pizzaObj={pizza} key={pizza.name} />
        ))}
      </ul>
    </main>
  );
}
```

> This is the conventional practice in React that in these cases, the parent component passes the whole data object as props to the child component.

We would also have to update the `Pizza` component to receive the whole pizza object for each pizza on the menu.

```js
function Pizza(props) {
  return (
    <li className="pizza">
      <img src={props.pizzaObj.photoName} alt={props.pizzaObj.name} />
      <div>
        <h3>{props.pizzaObj.name}</h3>
        <p>{props.pizzaObj.ingredients}</p>
        <span>{props.pizzaObj.price}</span>
      </div>
    </li>
  );
}
```

> Note how we also defined a `key` prop in the `Menu` component. If we didn't do it, React would give us an error in the console saying that "Each child in a list should have a unique "key" prop." This means that each time we render a list, as we did in the `Menu` component using the `.map()` method, each of the items that gets rendered needs also a `key` property or attribute. This is a prop that is internal to React and it uses it to do some performance optimization. We should pass a unique value for the `key` prop. In this example, we used the pizza name as the key for each pizza.

> Also keep in mind that we should still keep using semantic HTML in React. Notice how we did that by using `ul` and `li` tags in the `Menu` and `Pizza` components respectively.

> It is a good practice to destructure props immediately when they are received in a component. This lets us quickly figure out what props the component is receiving, without having to look at the parent component in the chain. For instance, for the `Pizza` component mentioned above, we can do it like this:

```js
function Pizza({ pizzaObj }) {
  if (pizzaObj.soldOut) return null;

  return (
    <li className="pizza">
      <img src={pizzaObj.photoName} alt={pizzaObj.name} />
      <div>
        <h3>{pizzaObj.name}</h3>
        <p>{pizzaObj.ingredients}</p>
        <span>{pizzaObj.price}</span>
      </div>
    </li>
  );
}
```

#### **Conditional rendering**

This is a very important technique that we use all the time in React. There are 3 ways of rendering some JSX or an entire component in React.

Keep these notes in mind:

1. Use the ternary operator when you need to return some piece of JSX based on a condition.
2. Sometimes you may need to return something entirely different in a certain condition. In these situations you may use multiple `return` statements based on conditions.

##### **With `&&`**

This basically involves using the short circuiting technique of JavaScript. Short circuiting means that you combine a condition with something that should be returned. If the condition becomes `true` or if it contains a truthy value, the second thing will actually be returned.

In this example, we want to render the footer content if the `isOpen` variable contains `true`.

```js
function Footer() {
  const hour = new Date().getHours();
  const openHour = 12;
  const closeHour = 22;
  const isOpen = hour >= openHour && hour <= closeHour;
  console.log(isOpen);
  return (
    <footer className="footer">
      {isOpen && (
        <div className="order">
          <p>We're open until {closeHour}:00. Come visit us or order online.</p>
          <button className="btn">Order</button>
        </div>
      )}
    </footer>
  );
}
```

As another example, take the `Menu` component that we previously mentioned. We want to render the `ul` only if there are some pizzas avilable on the `pizzaData` array.

```js
function Menu() {
  const numPizzas = pizzaData.length;
  return (
    <main className="menu">
      <h2>Our menu</h2>
      {numPizzas > 0 && (
        <ul className="pizzas">
          {pizzas.map((pizza) => (
            <Pizza pizzaObj={pizza} key={pizza.name} />
          ))}
        </ul>
      )}
    </main>
  );
}
```

This will make it so that if the `pizzaData` array is empty, then the whole `ul` won't be rendered.

> We should not implement the condition by simply writing `numPizzas` as a truthy/falsey value. In this case, if `numPizzas` is 0, then it would be a falsey value and short circuiting will happen. Therefore, what will be returned is not what we wrote after the `&&`. Instead, the value of `numPizzas` will be returned and rendered on the page. We don't want that. So we should actually write the condition in a way that becomes `true` or `false`.

##### **With ternary operator**

We are now going to do the same thing with the ternary operator. The advantage of using ternary operator is that we can display some alternative.

```js
function Menu() {
  const pizzas = pizzaData;
  const numPizzas = pizzas.length;
  return (
    <main className="menu">
      <h2>Our menu</h2>
      {numPizzas > 0 ? (
        <ul className="pizzas">
          {pizzas.map((pizza) => (
            <Pizza pizzaObj={pizza} key={pizza.name} />
          ))}
        </ul>
      ) : null}
    </main>
  );
}
```

Let's also use this for the `Footer` component:

```js
function Footer() {
  const hour = new Date().getHours();
  const openHour = 12;
  const closeHour = 22;
  const isOpen = hour >= openHour && hour <= closeHour;
  console.log(isOpen);

  return (
    <footer className="footer">
      {isOpen ? (
        <div className="order">
          <p>We're open until {closeHour}:00. Come visit us or order online.</p>
          <button className="btn">Order</button>
        </div>
      ) : (
        <p>
          We're happy to welcome you between {openHour} and {closeHour}
        </p>
      )}
    </footer>
  );
}
```

> We can use ternary operator to render the text content of a JSX element based on a condition. We can also use the ternary operator to insert class names based on a condition. Take the `Pizza` component for instance where we want to add the `sold-out` class name to any of the pizzas that are sold out. We also want to show the "SOLD OUT" text content instead of pizza's price in the `<span>` element that we defined in the JSX.

```js
function Pizza({ pizzaObj }) {
  return (
    <li className={`pizza ${pizzaObj.soldOut ? "sold-out" : ""}`}>
      <img src={pizzaObj.photoName} alt={pizzaObj.name} />
      <div>
        <h3>{pizzaObj.name}</h3>
        <p>{pizzaObj.ingredients}</p>
        <span>{pizzaObj.soldOut ? "SOLD OUT" : pizzaObj.price}</span>
      </div>
    </li>
  );
}
```

##### **With multiple `return` statements**

Up until this point, all our components only ever had one `return` statement. But as JavaScript allows us, we can use multiple return statements based on some condition. Of course, only one of the `return` statements would be executed in the component, and that is why we implement this based on some condition.

For instance, if we want to render a `Pizza` component if only it is not sold out, we can do this:

```js
function Pizza(props) {
  if (props.pizzaObj.soldOut) return null;

  return (
    <li className="pizza">
      <img src={props.pizzaObj.photoName} alt={props.pizzaObj.name} />
      <div>
        <h3>{props.pizzaObj.name}</h3>
        <p>{props.pizzaObj.ingredients}</p>
        <span>{props.pizzaObj.price}</span>
      </div>
    </li>
  );
}
```

## **React Fragments**

Basically, a React fragment lets us group elements without leaving any trace in the DOM.

Remember that a piece of JSX, no matter where it is defined, can only have one root element. Previously, we said that one way to fix this is to wrap our elements in a single parent element, like a `div`. This can potentially mess up the styles and appearances that we defined for the page. So we can use fragments.

You will again wrap the elements that you want to return as JSX in a parent element, but this parent element will not be an actual HTML element. It won't be inserted into the HTML code of the page. Only React will know about this. The parent element's opening would be `<>` and its closing would be `</>`.

```js
function Menu() {
  const pizzas = pizzaData;
  const numPizzas = pizzas.length;
  return (
    <main className="menu">
      <h2>Our menu</h2>

      {numPizzas > 0 ? (
        <>
          <p>
            Authentic Italian cuisine. 6 creative dishes to choose from. All
            from our stone stove, all organic, all delicious.
          </p>
          <ul className="pizzas">
            {pizzas.map((pizza) => (
              <Pizza pizzaObj={pizza} key={pizza.name} />
            ))}
          </ul>
        </>
      ) : (
        <p>We're still working on our menu. Please come back later.</p>
      )}
    </main>
  );
}
```

> Sometimes we need to add a `key` to the React fragment, for instance, when we are using it to render a list. Then the fragment would have to be written in a different way. The wrapper element will now be `<React.Fragment>` and then we would be able to add a `key` prop to it.

## **Styling React applications**

There are several ways to style components. React does not really care about how we do it. React is more of a library than a framework.

### **Inline styling**

In HTML, we can style elements using the `style` attribute. But it works a bit different in JSX. We cannot assign a string to the style attribute as we did with the normal HTML syntax. The style attribute in JSX should receive a JavaScript object containing the styles defined as properties.

```js
function Header() {
  return (
    <h1 style={{ color: "red", fontSize: "48px" }}>Fast React Pizza Co.</h1>
  );
}
```

Note how we used the first set of `{}` to enter JavaScript mode in the JSX, and then used another set of `{}` which indicates the JavaScript object that is used to define style properties.

> There is no problem in using inline styles in JSX, but this can easily get out of control when designing large-scale applications.

> Some style properties that we type their names with dashes in CSS, should be written in cammelCase in JavaScript. For instance, `font-size` in CSS should be written as `fontSize` in JSX.

> The JavaScript object inserted into the style attribute can be defined separately outisde the JSX.

### **External CSS or Sass**

We should first import the external CSS file into the JavaScript file where our components and their JSX are declared.

```js
import "./index.css";
```

We then have to insert class names that we used in the external CSS file. Keep in mind that in JSX, we cannot use the `class` attribute as we do it in HTML. Instead, we should use `className`.

```js
function App() {
  return (
    <div className="container">
      <Header />
      <Menu />
      <Footer />
    </div>
  );
}
```

> The external CSS file should normally be located in the `src` folder.

> Styles included here as an external CSS file are global styles, they are not scoped to the components where they are used.

### **CSS modules**

### **Tailwind CSS**

## **Separation of concerns in React**

[Notes will be added later.]

Before React we had one technology per file, but with React we have one component per file. So separation of concerns is still there, but in a different paradigm.

# **State, Events and Forms interactive components**

In this section, we will be working on a steps component as an example. We initialized the a new project using the `npx create-react-app@5 steps` command, then deleted everything in the `src` folder except the `App.js` and `index.js` files. Inside the `App.js` file we define the `App` component and export it so that the `root` element defined in the `index.js` file can have access to it.

**`App.js`**

```js
const messages = [
  "Learn React ⚛️",
  "Apply for jobs 💼",
  "Invest your new income 🤑",
];

export default function App() {
  const step = 1;
  return (
    <div className="steps">
      <div className="numbers">
        <div className={`${step >= 1 ? "active" : ""}`}>1</div>
        <div className={`${step >= 2 ? "active" : ""}`}>2</div>
        <div className={`${step >= 3 ? "active" : ""}`}>3</div>
      </div>

      <p className="message">
        Step {step}: {messages[step - 1]}
      </p>

      <div className="buttons">
        <button style={{ backgroundColor: "#7950f2", color: "#fff" }}>
          Previous
        </button>
        <button style={{ backgroundColor: "#7950f2", color: "#fff" }}>
          Next
        </button>
      </div>
    </div>
  );
}
```

## **Handling events**

To handle events in React, we don't use the `.addEventListener()` method, because that is the imperative way of responding to event. But in React, we use a **declarative** approach, meaning that we don't manually select DOM elements. Instead, we use something similar to the **HTML inline event listener**.

To listen for a click event on a certain element, we use the `on<Event>` prop or attribute on the element in the JSX. This prop accepts a JavaScript function. For instance, if we want to listen for a click event on a button:

```js
export default function App() {
  const step = 1;

  return (
    <div className="steps">
      <div className="numbers">
        <div className={`${step >= 1 ? "active" : ""}`}>1</div>
        <div className={`${step >= 2 ? "active" : ""}`}>2</div>
        <div className={`${step >= 3 ? "active" : ""}`}>3</div>
      </div>

      <p className="message">
        Step {step}: {messages[step - 1]}
      </p>

      <div className="buttons">
        <button
          style={{ backgroundColor: "#7950f2", color: "#fff" }}
          onClick={() => alert("previous")}
          onMouseEnter={() => alert("previous")}
        >
          Previous
        </button>
        <button style={{ backgroundColor: "#7950f2", color: "#fff" }}>
          Next
        </button>
      </div>
    </div>
  );
}
```

> Notice how we have listened for two events (`onClick` and `onMouseEnter`) at the same time on one element.

> We don't usually define the callback function inside the event listener prop. Instead, we define a separate function inside the current component, and pass it into the prop.

```js
export default function App() {
  const step = 1;

  function handlePrevious() {
    alert("previous");
  }

  function handleNext() {
    alert("next");
  }

  return (
    <div className="steps">
      <div className="numbers">
        <div className={`${step >= 1 ? "active" : ""}`}>1</div>
        <div className={`${step >= 2 ? "active" : ""}`}>2</div>
        <div className={`${step >= 3 ? "active" : ""}`}>3</div>
      </div>

      <p className="message">
        Step {step}: {messages[step - 1]}
      </p>

      <div className="buttons">
        <button
          style={{ backgroundColor: "#7950f2", color: "#fff" }}
          onClick={handlePrevious}
        >
          Previous
        </button>
        <button
          style={{ backgroundColor: "#7950f2", color: "#fff" }}
          onClick={handleNext}
        >
          Next
        </button>
      </div>
    </div>
  );
}
```

We usually handle events in order to work with **states**.

## **State in React**

State is the most important concept in React. Mastering state is the most difficult part of learning React. Everything revolves around the concept of state in React. Here is what React developers need to learn about state:

1. What is state and why we need it?
2. How to use state in practice?
   - `useState`
   - `useReducer`
   - Context API
3. Thinking about state
   - When to use state
   - Where to place state
   - Types of state

We know how to pass data into a component using props, which is data coming from outside the component. But what if a component needs to **hold its own data**, especially **over time**? Also, what if we want to make our application interactive and change the UI as a result of an action? This is where state comes in.

State is data that a component can hold over time. It is necessary for information that the component needs to remember throughout the application's lifecycle. So we can think of state as the **memory of a component**.

Examples of state:

- Notification count
- Text content of an input field
- Active tab in a tabbed component
- Content of a shopping cart

The common thing between all kinds of state is that the user can easily change the state value in the application. For instance, when they read a notification, the count will decrease. So each component needs to be able to hold this data, which is **a piece of state**, over time.

A piece of state or a state variable is a single variable in a component, which is also called a component state.

Keep in mind that **updating** the state triggers React to **re-render** the component in the UI. So state is how React keeps the user interface in sync with data. Therefore, state allows developers to do 2 important things:

1. Update the component's view by re-rendering the component.
2. Persist local variables between renders and re-renders

So state is actually a tool. Mastering the state will unlock the power of React development.

### **Mechanics of state**

Let's start from a fundamental React principle that we learned earlier.

1. **PRICIPLE:** In react, we do NOT manipulate the DOM directly when we want to update a component's view. React is declarative, not imperative.

So how do we update a component on the screen when some data changes or when we need to respond to some event like a click?

2. **PRICIPLE:** React updates a component view by re-rendering the entire component whenever the underlying data changes. Re-rendering means that React calls the component function again. React removes the entire component view and replaces it with a new view each time a re-render needs to happen. React preserves the component state throughout re-renders, unless the component disappears from UI entirely which we call **unmounting**.
3. It is when the state is update that a component is automatically re-rendered.

Now here is a flow of what happens in this process in the actually application. Imagine there is an event handler in the view, for instance, on a button that the user can click:

1. The moment that button is clicked, we can update a piece of state using the **setter function** coming from the `useState()` hook.
2. When React notices that a state has changed, it will automatically re-render the component, which will result in the updated view for the component.

**REACT REAECTS TO STATE CHANGES BY RE-RENDERING THE UI.**

### **State guidelines**

There is one important technical detail to remember: **Each component has and manages its own state, no matter how many times we render the same component, and no matter if there are multiple components of the same type (like a list) but for different contents.** For instance, imagine a list of score componentes for multiple football teams. State is isolated inside each component.

Therefore, we can think of the entire Application (UI) as a function of the state. In other words the entire UI is always a representation of all the current states in all components.

Taking it one step further, we can say that a React application is fundamentally all about **changing state over time**. Instead of viewing a UI as explicit DOM manipulations, with state, we now view a **UI as a reflection of data changing over time**.

Here are a few practical guidelines about state:

1. Use a state variable variable for any data that the component should keep track of or remember over time. This is data that will change at some point.
2. Whenever you want something in the component to be dynamic, create a piece of state related to that thing, and update the state when that thing should change. For instance, you can create an `isOpen` state variable that tracks whether a model window is open or not. Then when `isOpen` is `true` we display the window, and if `false`, we hide it.
3. When building a component, imagine its view as a reflection of state changing over time.
4. For data that should not trigger component re-renders, don't use state. Use a regular variable instead.

### **Working with a state variable**

Following the example mentioned earlier, we now want to implement a functionality that causes the step to change as we click on the next and previous buttons.

To do this, we no longer define the `state` variable as we did before like this:

```js
const step = 1;
```

Instead, in order to use state in a component we should follow 3 steps:

1. Add a new state variable with `useState()` function. Don't forget to import `useState` from `react`. The `useState()` function receives an argument which is the dafault value of the state variable that is being defined. This function returns an array with two elements: first, the default value that we defined, and second, a function that updates the state variable. So we can immediately destructure this returned array into two separate variables: `step`, `setStep`.

```js
export default function App() {
  const [step, setStep] = useState(1);

  function handlePrevious() {
    alert("previous");
  }

  function handleNext() {
    alert("next");
  }

  return (
    <div className="steps">
      <div className="numbers">
        <div className={`${step >= 1 ? "active" : ""}`}>1</div>
        <div className={`${step >= 2 ? "active" : ""}`}>2</div>
        <div className={`${step >= 3 ? "active" : ""}`}>3</div>
      </div>

      <p className="message">
        Step {step}: {messages[step - 1]}
      </p>

      <div className="buttons">
        <button
          style={{ backgroundColor: "#7950f2", color: "#fff" }}
          onClick={handlePrevious}
        >
          Previous
        </button>
        <button
          style={{ backgroundColor: "#7950f2", color: "#fff" }}
          onClick={handleNext}
        >
          Next
        </button>
      </div>
    </div>
  );
}
```

> The `useState()` function is also called a **hook** in React. Hooks are identified with the `use` keyword at the beginning of their name. It is extremely important to remember that we can only call hooks on the top-level of a function, not inside an `if` statement or a function or a loop.

> We should only update state using the setter function that is, by default, defined as the second element of the array returned by the `useState()` function. If you attempt to update the state manually using regular JavaScript code, React cannot understand what you are trying to do. The functionality will simply not work. This is true about primitive values. But what if the state variable holds an object and then we update this state manually? This will actually work and React will re-render! But it is definitely a bad practice, especially in React, which is all about **immutablity** and **function state updates**.

```js
const [test] = useState({ name: "Jonas" });

function handleNext() {
  test.name = "Fred";
}
```

2. Use it in a code, usually in JSX. In this example, we should use the `setStep()` function in `handlePrevious()` and `handleNext()` functions. The `setStep()` function receives an expression that tells it how to update the state variable.
3. Update the piece of state in some event handler

```js
function handlePrevious() {
  if (step > 1) setStep(step - 1);
}

function handleNext() {
  if (step < messages.length) setStep(step + 1);
}
```

> In case we are updating the state based on the current state, it is the best practice to implement a callback function inside the state setter function that will handle the upading task. This way we prepare our application for future changes in its state updating mechanism. Again, this is important when we are updating the state based on the current state. It means that the new value of the state variable is derived somehow from the current value of the state variable.

```js
function handlePrevious() {
  if (step > 1) setStep((s) => s - 1);
}

function handleNext() {
  if (step < messages.length) setStep((s) => s + 1);
}
```

> In case the new value of the state variable does not depend on its current value, we can simply ignore using a callback function inside the state setter function.

### **Forms and handling submissions**

One of the most important things that we do the web is to interact with web applications through forms. We are now going to learn how to use forms in React.

#### **Creating a form**

Take the "Far Away" project as an example. When we build forms in React, we use the normal HTML `<form>` element. So we have a `Form` component, and inside it we write the JSX for a form like this:

```js
function Form() {
  return (
    <form className="add-form">
      <h3>What do you need for your trip?</h3>
      <select>
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          <option value={num} key={num}>
            {num}
          </option>
        ))}
      </select>
      <input type="text" placeholder="Item..." />
      <button>Add</button>
    </form>
  );
}
```

> Notice how we have inserted all the `option` elements of the `select` form element programatically. So basically, we made an `Array` by defining its `length` and a mapping function that receives first the current value, and second the current index, and it will return any value that we produce with any expression in this mapping function.

> Remember to define a `key` prop for any element that is produced through a mapping operation. We will later learn what this key is and why it is important.

#### **Form Events**

When we work with a form, we basically want the form to be submitted once we click on a button element. We can then react to the form submission with an event handler.

To listen for the submission event on a form, we add the `onSubmit` prop to its JSX element, and we pass an event handler function to it, not call it. So we would also have to define an event handler function inside the `Form` component.

```js
function Form() {
  function handleSubmit(e) {
    e.preventDefault();
  }
  return (
    <form className="add-form" onSubmit={handleSubmit}>
      <h3>What do you need for your trip?</h3>
      <select>
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          <option value={num} key={num}>
            {num}
          </option>
        ))}
      </select>
      <input type="text" placeholder="Item..." />
      <button>Add</button>
    </form>
  );
}
```

> Note that we have prevented the default behavior of the HTML form element when a submission happens. The default behavior is to perform a full reload for the whole application, but as we have talked about React and its aim to create single-page applications, that is not what we want.

> The input data that is submitted by a form is accessible in the event (`e`) object that is received by the event handler function. Inside this object there is a `target` object that stores all the elements of the form, and their values if they have any. But this is not the way we acquire form input data in React. Instead, we use **Controlled Elements**.

#### **Controlled elements**

An important thing to keep in mind is that, by default, the input fields of a form maintain their own state inside the DOM. This makes it hard to read their values, and it also leaves the state right in the DOM, which is not ideal for many reasons. In React, we want to keep all states in one central place which is inside the React application, and not inside the DOM. In order to do this, we use a technique called **Controlled Elements**.

With this technique, it is React that will control and own the state of the input fields. So, basically, we need some state in our application.

In order to implement the controlled element technique, we follow 3 steps:

1. Create a piece of state
2. Use this state as a value of the input field

```js
function Form() {
  const [description, setDescription] = useState("");

  function handleSubmit(e) {
    e.preventDefault();
  }
  return (
    <form className="add-form" onSubmit={handleSubmit}>
      <h3>What do you need for your trip?</h3>
      <select>
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          <option value={num} key={num}>
            {num}
          </option>
        ))}
      </select>
      <input type="text" placeholder="Item..." value={description} />
      <button>Add</button>
    </form>
  );
}
```

3. This will make it so that the `value` of the input field is only in sync with the value of the `description` state variable. So we are no longer able to type anything into the field in the UI. In order to fix this, we would have to connect the `description` state variable to the UI. This is done by inserting a `onChange` prop on the input field.

```js
function Form() {
  const [description, setDescription] = useState("");

  function handleSubmit(e) {
    e.preventDefault();
  }
  return (
    <form className="add-form" onSubmit={handleSubmit}>
      <h3>What do you need for your trip?</h3>
      <select>
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          <option value={num} key={num}>
            {num}
          </option>
        ))}
      </select>
      <input
        type="text"
        placeholder="Item..."
        value={description}
        onChange={(e) => setDescription(e.target.value)}
      />
      <button>Add</button>
    </form>
  );
}
```

So we have basically defined an event handler function for the `onChange` prop of the input field. This makes it so that everytime we type something in the field, it will update the state with the value that has just been typed. What then? React detects that the state has been updated, so it triggers a re-render.

> Note that `e.target` is the element to which the event handler function is attached.

> **EXTREMELY IMPORTANT:** Notice how functions are passed differently into `onSubmit` and `onChange` props. The reason behind this difference is that when the `submit` event happens, meaning the form data is being submitted, we call the submit handler function immediately with the `event` object automatically passed into it. On the other hand, when the input `change` event happens, we need to pass the new value into the state setter function. So although the `e` object is automatically passed into the setter function, we need to call the setter function with the new state value which is inside the event object, we don't want to call the setter with the event object itself.

We can implement the same technique for the `select` form field.

```js
function Form() {
  const [description, setDescription] = useState("");
  const [quantity, setQuantity] = useState(1);

  function handleSubmit(e) {
    e.preventDefault();

    if (!description) return;

    const newItem = { description, quantity, packed: false, id: Date.now() };
    console.log(newItem);

    setDescription("");
    setQuantity(1);
  }
  return (
    <form className="add-form" onSubmit={handleSubmit}>
      <h3>What do you need for your trip?</h3>
      <select value={quantity} onChange={(e) => setQuantity(+e.target.value)}>
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          <option value={num} key={num}>
            {num}
          </option>
        ))}
      </select>
      <input
        type="text"
        placeholder="Item..."
        value={description}
        onChange={(e) => setDescription(e.target.value)}
      />
      <button>Add</button>
    </form>
  );
}
```

We should also twick the `handleSubmit` function to prevent the application to accept empty submissions. It is also a normal practice to make the form go back to its empty initial status as the form is submitted.

```js
function handleSubmit(e) {
  e.preventDefault();

  if (!description) return;

  const newItem = { description, quantity, packed: false, id: Date.now() };
  console.log(newItem);

  setDescription("");
  setQuantity(1);
}
```

> Now as the example application is going on in its development phase, we now need to render this new item created through the form submission. Remember that we cannot pass data as props between sibling elements. Data can only flow down the tree, but not sideways. This is where we really need to start thinking about state and state management in React in order to make it possible to pass data between sibling elements.

## **Review: State vs. Props**

| State                                        | Props                                                                                                                            |
| -------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Internal data, owned by component            | External data, owned by parent component. Similar to function parameters, as a communication channel between parent and children |
| Component's memory                           | Read-only, cannot be modified by the component that is receiving them                                                            |
| Can be updated by the component itself       | **Receiving new props causes components to re-render. Usually when the parent's state has been updated.**                        |
| Updating state causes component to re-render |                                                                                                                                  |
| Used to make components interactive          | Used by parent to configure child component (settings)                                                                           |

# **React developer tools**

Since developer tools are so helpful for developers, the React team built dev-tools specific to React, which can be extremely helpful when working with [state](#state-in-react).

Install React's Chrome dev-tools.

# **Thinking in React**

A core skill that every React developer needs to develop, is to think in React. Thinking in React encompasses many aspects:

1. State management
   - When and wehere to create state?
   - When and how to **derive** state?
   - How to communicate between child and parent components by **lifting** state up?
2. some other aspect
3. some other aspect

While you are building an application, thinking in React basically means that you have a very good **mental model** of how and when to use all the React tools, like components, state, props, data flow, effects, and many more. It is also always thinking in terms of **state transitions** rather than element mutations.

Thinking in React can be interpretted as a process that can help us build apps in a more structured way. This process, of course, is not a rigid process. In practice there will be a lot of back and forth between these steps. But here is a good suggestion:

1. Break the desired UI into components and establish how these components are related in the component tree. This also includes thinking about reusablity and composiblity of components.
2. Build a static version in React (without state and interactivity). By doing this, we do most of the coding up front, before having to wory about state and interactivity.
3. Think about **state**:
   - When to use state
   - Types of state: local vs. global
   - Where to place each piece of state
4. Establish **data flow**:
   - One-way data flow
   - Child-to-parent communication
   - Accessing global state

> Steps 3 and 4 are called altogether **state management**.

Once we know how to think in Reeact, we will be able to answer these questions:

- How to break up a UI design into components?
- How to make some of my components truly reusable?
- How to assemble UI from reusable components?
- What piece of state do I need for interactivity?
- Where to place state? (what component should own each piece of state?)
- What types of state can or should I use?
- How to make data flow through the application?

## **State management**

Take a look at a complicated web application. How would we know that we need all pieces of state in the application? How do we know where to place them in the code? This is where state management comes to play.

State management is about deciding **when** to create pieces of state, what **types** of state are necessary, **where** to place each piece of state, and how **data flows** through the app. State management is to give each piece of state a home within our code base.

Up until this point, we never had to worry about state management. We simply placed each state in a component that needed it. However, as an application grows the need to find the right home to each piece of state starts to become really important.

### **Types of state**

There are two types of state: Local vs. Global.

| Local                                                                                             | Global                                                  |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| Needed only by one or few components                                                              | Many components might need                              |
| Defined in a component and only that component and child components have access to it (via props) | Accessible to every component in the entire application |

> Looking at a complicated application, an example of local state might be the input text in the search bar. An example of global state can be the shopping cart since this piece of data is used all over the place.

The distinction between local and global state matters more in large-scale applications. In small apps, we won't have any truly global state. One important guideline in state management is to always start with local state, and only move to global state if you truly need it.

> In practice, we can define global state using React's **Context API** or an external global state management library called **Redux**.

### **When and where?**

It all starts **when** you realize that you need to store some data. When this happens, you have to ask yourself:

**Will this data change at some point in time?**

- No: use a regular `const` variable
- Yes: **Is it possible to compute this new data from an existing piece of state or props?**
  - Yes: _Derive_ state, meaning that you should compute it based on already existing state or prop
  - No: **Should updating the state re-render the component?**
    - No: `useRef`, which persists data over time, like regular state, but does not re-render a component.
    - Yes: Place a new piece of state in component. (mentioned earlier: always start with local state.)

**Is the state variable that we just created only used by the current component?**

- Yes: Leave the state in the component.
- No: **State variable is also used by a child component?**
  - Yes: Pass to child via props
  - No: **Used by one or a few sibling components or a parent component?**
    - Yes: _Lift_ state up to first _common parent_.
    - No: Probably _global state_. later...

### **Lifting state**

Let's go back to the "Far Away" application as an example. In this application, we are going to set a state variable for all the things that should be listed.

Following the set of questions mentioned in the previous part, we should first ask if the data will change at some point? Yes. Can it be computed from an existing state? No. Should it re-render the component? Yes. So we would have to place a new piece of state in the component for now.

What we do now is to create a new piece of state in the `Form` component for `items`. Then we should use the `setItems` setter function to update the `items` state variable whenever the form input data is submitted.

```js
function Form() {
  const [description, setDescription] = useState("");
  const [quantity, setQuantity] = useState(1);
  const [items, setItems] = useState([]);

  function handleAddItems(item) {
    setItems((items) => [...items, item]);
  }

  function handleSubmit(e) {
    e.preventDefault();

    if (!description) return;

    const newItem = { description, quantity, packed: false, id: Date.now() };
    handleAddItems(newItem);

    setDescription("");
    setQuantity(1);
  }
  return (
    <form className="add-form" onSubmit={handleSubmit}>
      <h3>What do you need for your trip?</h3>
      <select value={quantity} onChange={(e) => setQuantity(+e.target.value)}>
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          <option value={num} key={num}>
            {num}
          </option>
        ))}
      </select>
      <input
        type="text"
        placeholder="Item..."
        value={description}
        onChange={(e) => setDescription(e.target.value)}
      />
      <button>Add</button>
    </form>
  );
}
```

> Notice again how we have implemented a callback function inside the `setItems` state setter function because the new state is computed based on the current state.

Up until this point, the state is being updated successfully, but it is not rendered anywhere in the UI. The problem is that the `Form` component in which we have defined the `items` state is actually the sibling of `PackingList` component which is actually responsible for rendering the `items` state to the UI. We cannot pass this data as a prop to the `PackingList`. The solution here is to **lift up state** to the first common parent component, which is the `App` component in this case.

So we move the state definition to the `App` component. Then we would also have to move the `handleAddItems` function to the `App` component because that is where, now, the `setItems` setter function and the `items` state is defined and therefore usable.

Now that we have lifted the state to the `App` component, we can pass the state down to any of the child components.

So the `PackingList` component will simply receive the `items` state variable as a prop, and use it to render the `items` state to the UI.

We also need to pass the `handleAddItems` function, responsible for calling the `setItems` setter function to update the state function, to the `Form` component. Passing down a setter function is also called **child-to-parent communication** or **inverse data flow**, because here it is the child that will update the parent state. It seems as if the data is flowing up, which in fact is not true.

```js
export default function App() {
  const [items, setItems] = useState([]);

  function handleAddItems(item) {
    setItems((items) => [...items, item]);
  }

  return (
    <div className="app">
      <Logo />
      <Form onAddItems={handleAddItems} />
      <PackingList items={items} />
      <Stats />
    </div>
  );
}
```

> There is a convention for naming the prop through which a state setter function is passed. In this example, we insert the `handleAddItems` function into a prop called `onAddItems`.

We would then have to prepare the `Form` and `PackingList` components to receive these props. We would update the `Form` component like this:

```js
function Form({ onAddItems }) {
  const [description, setDescription] = useState("");
  const [quantity, setQuantity] = useState(1);

  function handleSubmit(e) {
    e.preventDefault();

    if (!description) return;

    const newItem = { description, quantity, packed: false, id: Date.now() };
    onAddItems(newItem);

    setDescription("");
    setQuantity(1);
  }
  return (
    <form className="add-form" onSubmit={handleSubmit}>
      <h3>What do you need for your trip?</h3>
      <select value={quantity} onChange={(e) => setQuantity(+e.target.value)}>
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          <option value={num} key={num}>
            {num}
          </option>
        ))}
      </select>
      <input
        type="text"
        placeholder="Item..."
        value={description}
        onChange={(e) => setDescription(e.target.value)}
      />
      <button>Add</button>
    </form>
  );
}
```

And the `PackingList` component like this:

```js
function PackingList({ items }) {
  return (
    <div className="list">
      <ul>
        {items.map((item) => (
          <Item item={item} key={item.id} />
        ))}
      </ul>
    </div>
  );
}
```

As another example, we now want to implement the functionality of deleting items from the list. This means that whenever we hit the X button on any of the elements, that button should be removed from the state, and therefore, should also be removed from the UI.

So we define a `handleDeleteItem` function in the `App` component.

```js
export default function App() {
  const [items, setItems] = useState([]);

  function handleAddItems(item) {
    setItems((items) => [...items, item]);
  }

  function handleDeleteItem(id) {
    setItems((items) => items.filter((item) => item.id !== id));
  }

  return (
    <div className="app">
      <Logo />
      <Form onAddItems={handleAddItems} />
      <PackingList items={items} onDeleteItem={handleDeleteItem} />
      <Stats />
    </div>
  );
}
```

And then we should pass it into the `Item` since it is in that component where the click on delete button will happen in the UI. But on the way to that component, there is the `PackingList` component. So we first pass the `handleDeleteItem` function to the `PackingList` component, and then from there, we pass it into the `Item` component.

```js
function PackingList({ items, onDeleteItem }) {
  return (
    <div className="list">
      <ul>
        {items.map((item) => (
          <Item item={item} onDeleteItem={onDeleteItem} key={item.id} />
        ))}
      </ul>
    </div>
  );
}

function Item({ item, onDeleteItem }) {
  return (
    <li>
      <span style={item.packed ? { textDecoration: "line-through" } : {}}>
        {item.quantity} {item.description}
      </span>
      <button onClick={() => onDeleteItem(item.id)}>❌</button>
    </li>
  );
}
```

> This is, again, the case where we previously mentioned an **EXTREMELY IMPORTANT** note. Keep in mind that we cannot immediately call the `onDeleteItem` function in the `onClick` prop, because in that case, the function will be called with the event (`e`) object passed into it automatically. But here, we don't want to call this object with the event object. Instead, we want the function to be called while the item ID is passed into it. This is why we used a callback function inside the `onClick` prop, in order to be able to pass the necessary data into the `onDeleteItem` handler.

As another example, we now want to implement a checkbox for each item. If the checkbox is checked, we want the item's `packed` property to be updated. It means that we actually want the `items` state variable to be updated.

We start by defining the `handleToggleItem` function in the `App` component since this is where the `items` state variable and its setter function are defined. Remember that this `handleToggleItem` function should receive the item ID in order to be able to find it in the items and update it.

```js
function handleToggleItem(id) {
  setItems((items) =>
    items.map((item) =>
      item.id === id ? { ...item, packed: !item.packed } : item
    )
  );
}
```

We should then pass this function into the `Item` component, but on its way, it should first go through the `PackingList` component.

```js
export default function App() {
  const [items, setItems] = useState([]);

  function handleAddItems(item) {
    setItems((items) => [...items, item]);
  }

  function handleDeleteItem(id) {
    setItems((items) => items.filter((item) => item.id !== id));
  }

  function handleToggleItem(id) {
    setItems((items) =>
      items.map((item) =>
        item.id === id ? { ...item, packed: !item.packed } : item
      )
    );
  }

  return (
    <div className="app">
      <Logo />
      <Form onAddItems={handleAddItems} />
      <PackingList
        items={items}
        onDeleteItem={handleDeleteItem}
        onToggleItem={handleToggleItem}
      />
      <Stats />
    </div>
  );
}
```

Now we should receive the function inside the `PackingList` component and then pass it to the `Item` component.

```js
function PackingList({ items, onDeleteItem, onToggleItem }) {
  return (
    <div className="list">
      <ul>
        {items.map((item) => (
          <Item
            item={item}
            onDeleteItem={onDeleteItem}
            onToggleItem={onToggleItem}
            key={item.id}
          />
        ))}
      </ul>
    </div>
  );
}

function Item({ item, onDeleteItem, onToggleItem }) {
  return (
    <li>
      <input
        type="checkbox"
        value={item.packed}
        onChange={() => onToggleItem(item.id)}
      />
      <span style={item.packed ? { textDecoration: "line-through" } : {}}>
        {item.quantity} {item.description}
      </span>
      <button onClick={() => onDeleteItem(item.id)}>❌</button>
    </li>
  );
}
```

### **Derived state**

This is pretty straight forward. Derived state is state that is computed from an existing piece of state of from props.

Whenever you are in a situation where one state is easily computed from another, always prefer derived state.

As an exmple of this, let's calculate the statistics displayed in the `Stats` component of our imaginary application. What we should do is to pass the `items` state variable to the `Stats` component, where some new states will be derived from the `items` state and then reflected in the `Stats` component.

So in the `App` component, the only thing we do is:

```js
return (
  <div className="app">
    <Logo />
    <Form onAddItems={handleAddItems} />
    <PackingList
      items={items}
      onDeleteItem={handleDeleteItem}
      onToggleItem={handleToggleItem}
    />
    <Stats items={items} />
  </div>
);
```

Then we receive the `items` state variable in the `Stats` component, and based on the value of this state variable, we perform some actions.

```js
function Stats({ items }) {
  if (!items.length)
    return (
      <p className="stats">
        <em>Start adding some items to your packing list.</em>
      </p>
    );

  const numItems = items.length;
  const numPacked = items.filter((item) => item.packed).length;
  const percentage = Math.round((numPacked / numItems) * 100);

  return (
    <footer className="stats">
      <em>
        {percentage === 100
          ? "You got everything! Ready to go ✈"
          : `💼 You have ${numItems} items on your list, and you already packed
        ${numPacked} (${percentage}%)`}
      </em>
    </footer>
  );
}
```

## **Components**

We will now learn:

- how to think about components
- Composition
- Reusability
- How to split a component
- Building layouts

It is important to first understand how to split a UI into components and what type of components we can use.

### **Splitting a UI into components**

When it comes to components these are the important questions that we should ask:

1. How to split a UI into components?
2. When should we create new components?

One important factor that helps us answer these questions is the **component size**. A component, at its extremes, can be huge or small. Many times none of these extremes are ideal.

A huge component is identified when it has a lot of responsibilities. Components are just like JavaScript functions, in the sense that if a function does to many different things, we should break it up into multiple functions. Another sign of a huge component is that it might receive too many props, like 10 or 15! These make the component very **hard to reuse**. It also makes the code complex and hard to understand.

But this does not mean that we should switch to the other extreme and build small components, splitting every single functionality into its own component.

| Small                                               | Huge                      |
| --------------------------------------------------- | ------------------------- |
| end up with 100s of mini-components                 | Too many responsibilities |
| Confusing code base because of too much abstraction | Might need to many props  |

Most of the time the goal is to create components that strike the right balance between being too specific and too broad.

Here are 4 criteria for splitting a UI into comonents:

1. Logical separation of contant/layout
2. Reusability
3. Each component has a single well-defined responsibility to avoid complexity
4. Personal coding style: some people prefer smaller components, while others prefer larger components

#### **When to create a new component?**

When you are creating a new component and you are in doubt about what the component should include, just start with a relatively big component, but not a huge component. Then split the big component into smaller components as it is necessary. But when does it become necessary?

Here is a framework based on the 4 criteria mentioned above to help you decide when to create a new component:

1. Logical separation of content/layout: Does the component contain pieces of content or layout that don't belong together? If yes, Then you might need a new component.
2. Is it possible to reuse part of the component? Do you want or need to reuse it? If yes, then you should probably take that code and extract it into its new component.
3. Is the component doing too many different things? Does the componeent rely on too many props? Does the component havee too many pieces of state and/or effects? Is the code, including JSX, too complex/confusing? If yes, then you might need a new smaller component.
4. Personal coding style: Do you prefer smaller functions/components? If yes, you might need a new component.

#### **General guidelines**

- Creating a new component creates a new abstraction. Abstractions have a cost, because more abstractions require more mental energy to switch back and forth between components. So try not to create new components too early.
- Name a component according to what it does or what it displayes. Don't be afraid of using long names.
- Never declare a new component inside another component. Instead, co-locate related components inside the same file. Don't separate components into different files too early.
- It's completely normal that an application has components of many different sizes, including very small and huge ones: we always need some very small components in any application, because they are highly reusable and have very low complexity. For instance, you can imagine the like button component in an application.
- Most apps will have a few huge components that are not meant to be reused. For instance, a `Page` component of an application that contains the layout of the entire application or the page.

> The reusability range is pretty similar to the size range. Generally, the smaller the components are, the more reusable they will be, but not all components are meeant to be reusable. These are usually the huge components.

### **Component categories**

Most of your components will naturally fall into one of these three categories. We say naturally, because we should not force our components into one of these categories.

1. **Stateless/presentational:** They don't have any state. They are usually components that receive some props and then they simply present the received data or other content. These are usually small and reusable components, like logo, number of results, and one single item component.
2. **Stateful:** They do have state. Just because they have state, it does not mean they cannot be reusable. For instance, a search component does have state and we can reuse it as many times as we need.
3. **Structural:** These include pages, layouts, or screens of the application, which are oftentimes the result of componsing smaller components together. Structural components can be large and non-reusable components, but they don't have to. Structural components can also be small. What matters is that they are responsible for providing some sort of structure to applications, such as pages or layouts. So these componeents might not be used in small applications.
