- [Why scripting?](#why-scripting)
  - [What is scripting?](#what-is-scripting)
    - [Our target scripting language](#our-target-scripting-language)
      - [JavaScript advantages over AppleScript and VBScript](#javascript-advantages-over-applescript-and-vbscript)
      - [Coding environment](#coding-environment)
- [Scripting basics](#scripting-basics)
  - [Understanding objects, properties, and methods](#understanding-objects-properties-and-methods)
  - [Using objects](#using-objects)
    - [DOM](#dom)
    - [How to refer to objects](#how-to-refer-to-objects)
- [Scripting guide](#scripting-guide)
  - [Open a new document in photoshop](#open-a-new-document-in-photoshop)
  - [Add a layer to a newly created document](#add-a-layer-to-a-newly-created-document)

# Why scripting?

Scripting goes beyond the capability of actions and macros by allowing you to manipulate multiple documents and multiple applications in a single script. Additionally, scripts can very cleverly get and respond to information.

## What is scripting?

A script is a series of statements that tells an application to perform a set of tasks. The trick is writing the statements in a language that the application understands.

### Our target scripting language

Adobe has developed an extended version of JavaScript, called ExtendScript, that allows you to take advantage of certain Adobe tools and scripting features. The difference between these two languages will not affect you. However, you should get in the habit of giving your JavaScript scripts a `.jsx` extention, rather than the usual `.js` extention.

#### JavaScript advantages over AppleScript and VBScript

1. Your scripts can be used in either Windows or Mac OS.
2. In photoshop, you can access only `.jsx` files from within the application. You must run AppleScript or VBScripts from outside the application. This is not a major drawback, but it does require a few extra mouse clicks to run your scripts.
3. You can set up `.jsx` scripts to run automatically when you open the application by placing the scripts in the application's startup scripts folder.

#### Coding environment

To write scripts in JavaScript, you can use any text editor, or you can use the ESTK provided with your Adobe applications. The ESTK has many features that make it easier to use than a text editor, including a built-in syntax checker that identifies where the problems are in your script and tries to explain how to fix them, and the ability to run your scripts right from the ESTK without saving the file.

# Scripting basics

## Understanding objects, properties, and methods

In scripting, we need to understand 3 main things:

1. **Objects:** when using an adobe application, you open a file or document, then within the document, you create or manipulate layers, text, frames, channels, graphic lines, colors, and other design elements. These are called objects. To create a script statement, you **create an object or refer to an existing object**, and then you deal with properties or methods.
2. **Properties:** properties **describe** how an object looks like and help you modify it.
3. **Methods:** methods tell the script **what to do** to your objects.

> Note | You can only use the properties or methods that are allowed for objects. Adobe spells out for you in great detail in scripting resources that contain the information you need to create, define, and manipulate scripting objects.

## Using objects

The main concept to understand when using objects in scripts is **how to refer to an object**. In order to be able to refer to an object in scripting, you need to understand the **DOM**.

### DOM

Scripting languages use something called Document Object Model (DOM) to organize objects in a way that makes the object easy to identify. The principle behind a DOM is the **containment hierarchy**. It means that top level objects contain next level objects, which contain the subsequent level of objects and so on.

The top level object in any adobe application is the `application` object. Next is the `document` object, which contains all other objects, such as layers, channels, pages, text frames, and so on.

> Note | objects can belong to more than one collection or element.

### How to refer to objects

1. **Variables:** Most scripters create a variable for each object in their script.
2. **Collections:** scripting languages put each object in a **collection** and then assign the object a number, called the **index**. The objects in a collection are identical types of objects. For instance, the first document in the photoshop application is referred to by `documents[0]`.

> Note | JavaScript collection numbers are static; they don't shift when you add a new object to the collection. Object numbering in JS indicates the order in which objects where added to the collection. The first object you added was assigned the number 0, the next object you add to the collection is number 1, and so on. If you drag layer [2] to the bottom position in the layers palette, it still has index [2].

> Note | Scripts place objects in collections even when there is only one object of that type.

3. **`current` or `active` object properties:** Until the script does somwething else, the last new object is the active object, ready for modifications. Conveniently, many parent obejcts contain properties that allow you to refer easily to the active object. In JS, the property name for active objects is a compound word that combines `active` with the object name, in standard JS case usage:

```js
activeDocument;
activeLayer;
activeChannel;
activeView;
```

# Scripting guide

Here is a guide on how to work with the ExtendScript language. In order to execute the script that you are writing for photoshop, you need to choose photoshop in the ESTK dropdown list. This will then show you a broken link icon, where you can click to open the photoshop software. Then your basic coding environment is ready.

## Open a new document in photoshop

In order to create a document in the photoshop application, you should first refer to the `app` itself, then to the `documents` collection, on which you should then use the `add()` method.

```js
app.documents.add();
```

> Note | It is a good practice to store any object that your create in a separate variable. This will enable you to easily access the object using the variable name.

```js
const mydoc = app.documents.add();
```

> Note | The `add()` method on `documents` collection accepts a number of parameters as listed below.

## Add a layer to a newly created document

In order to create a layer in a document, you must first refer to the document where the layer should be created. Then you can use the `add()` method on `artLayers` collection.

```js
const mydoc = app.documents.add();
const mylayer = mydoc.artLayers.add();
```