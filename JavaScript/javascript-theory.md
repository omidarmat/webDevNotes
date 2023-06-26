# Object-Oriented Programming

Object-oriented programming is a programming paradigm based on the concept of obejcts. It was developed with the goal of organazing code (paradigm), to make code more flexible and easier to maintain. Here are some tips to be added on this general definition.

- We use objects to **model** or describe real-world or abstract features.
  - Objects are self-contained pieces/blocks of code.
  - Objects usually contain **properties** and **methods**. With objects, we pack data and the corresponding behavior into on block of code.
- In OOP, objects are **building blocks** of applications, and interact with one another through a **public interface (API)**.
  - An API includes methods that the code outside the object can access and use to communicate with the object.

**_Main ideas:_**

1. Creating objects programmatically
2. Being able to reuse some code (methods)

## Traditional OOP (classes and instances)

In OOP, in order to create objects programmatically, we use classes. A **class** contains some rules and it will act as a blueprint from which instances (new objects) can be created.

For example, a class named `User`, will hold some properties and methods that should be available on all user objects created from this class.

> **_Note_** | classes are not objects.

```js
User {
  username;
  password;
  email;

  login(password) {
    // login logic
  }

  sendMessage(str) {
    // message sending logic
  }
}
```

An object created from this class is called an **instance**. Many instances can be created from a class. Instances of the same class may have different data as properties, but they share the same functionalities.

### Four fundamental OOP principles

There are four important principles that can guide us toward a good class implementation:

1. **Abstraction:** ignoring details that don't matter, allowing us to get an overview perspective of the main things that we want to implement.
2. **Encapsulation:** keeping properties and methods private inside the class, so they are not accessible from outside the class. By having critical properties private within the class, we prevent them from being accidentally manipulated by outside code. We may also need some methods to be private to a class. One advantage is that this will prevent the whole code from breaking if the private method's code is updated.
3. **Inheritance:** making all properties and methods of a certain class accessible to a child class. In such cases, a child class `extends` a parent class. This allows common logic to be reused and also to model real-world relationships between features.
4. **Polymorphism:** a child class can overwrite a method it inherited from a parent class.

## OOP in JavaScript

Unlike classical or traditional OOP with its 'class' and 'instance' terminology that is used in other programming languages, in JavaScript we have **Constructor functions**, **Prototypes** and **Objects**. JavaScript does not really have classes. In JavaScript, we create objects from constructor functions. So constructor functions in JavaScript somehow simulate classes in traditional OOP.

### **Prototype & prototypal inheritance**

A prototype is an object that contains some methods and properties. All objects created from this prototype, will have access to these methods and properties. This mechanism is called **prototypal inheritance**.

Here is a table comparing classical OOP and JavaScript OOP:

| Classical OOP                                              | JavaScript OOP                                                                        |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Objects (instances) are _instantiated_ from a class        | Objects are _linked_ to a prototype object                                            |
| Behavior (methods) is _copied_ from class to all instances | Behavior is _delegated_ to the linked prototype object through prototypal inheritance |

For instance, we can use the `map` method on an array, because the map method is defined on the `Array.prototype` object, which is the prototype of all the arrays that we create in JavaScript.

```js
const num = [1, 2, 3];
num.map((v) => v * 2);
```

So the `num` array is linked to `Array.prototype` object, and therefore has access to all methods defined on it. The map method is not defined on the `num` array, but on its prototype.

### **Implementing prototypal inheritance in JavaScripts**

There are 3 ways of implementing prototypal inheritance in JavaScript:

#### **1. Constructor function and the `prototype` property:**

this is a technique to create objects from a function, and it is how built-in objects like Array, Map and Set are actually implemented in JavaScript.

##### **_Creating a construtor function_**

To create a constructor function, the syntax is exactly the same as a regular function declaration or expression.

> **_Note_** | we don't use an arrow function to define a constructor function, because an arrow function does not have its own `this` keyword. In OOP, we always need the `this` keyword.

```js
const Person = function (name, birthYear) {
  // instance properties: available on all instances
  this.name = name;
  this.birthYear = birthYear;
};
```

> **_Note_** | we can define methods inside a constructor function, but this is a bad practice. Methods that are defined inside the constructor function, would be copied into each and every instance object, producing unnecessary copies of the same functionality. The better way to go is to add methods to the `prototype` property of the constructor function.

##### **_Defining methods on prototype_**

Any function in JavaScript automatically has access to a property called `prototype`. Objects created from a constructor function, will have access to all the methods defined on the `prototype` property of that constructor function.

```js
Person.prototype.calcAge = function () {
  return 2037 - this.birthYear;
};
```

##### **_Defining properties on prototype_**

We can also set properties on the prototype, not just methods.

```js
Person.protoype.species = "Homo Sapiens";
```

##### **_Defining static methods_**

Static methods are usually used as helper functions defined on constructor functions. So objects (instances) created from a constructor function will not have access to static methods.

For instance, the `from` method is available on the `Array` constructor, but not on simple arrays.

To define a static method on the `Person` constructor function:

```js
Person.hey = function () {
  console.log("Hey there!");
};
```

We should then call the `hey` method on the `Person` constructor, and not on its instances.

```js
Person.hey();
```

##### **_Creating an object (instance)_**

`Person` is a normal JavaScript function. If we want it to act as a constructor function in order to create an object from it, we should call it using the `new` keyword.

```js
const omid = new Person("Omid", 1992);
```

Calling the the `Person` function with the `new` keyword will perform 4 steps:
| Step No. | Action |
| --------: | ------ |
| 1 | a new empty object is created |
| 2 | `Person` is called, `this` is set to the new empty object |
| 3 | the new empty object is linked to prototype, meaning that the `__proto__` property is created and set to `Person.prototype` |
| 4 | `Person` returns the object |

`omid` has now access to the methods defined on the `prototype` property of the `Person` constructor function:

```js
omid.calcAge(); //45
```

Here are some proof regarding the prototypal inheritance relationships:

- We can say that `omid` is an instance of `Person`. We can prove this using the JavaScript `instanceof` operator:

```js
console.log(omid instanceof Person); //true
```

- The prototype of `omid` is `Person.prototype`. So `prototype` property is not the prototype of `Person`. We can access the prototype of `omid` using the `__proto__` property of it.

```js
console.log(omid.__proto__);
```

We can check if it is exactly the same as the `prototype` property of the `Person` constructor function:

```js
console.log(omid.__proto__ === Person.prototype); //true
```

We can also confirm this using the `isPrototypeOf` method that is available on the `prototype` property of `Person`:

```js
console.log(Person.prototype.isPrototypeOf(omid)); //true
```

- Properties defined on the `prototype` property of the constructor function will not be available on the objects (instances), but they will have access to it through their prototype. We can use the `hasOwnProperty` method to check if a certain property is available on the object itself or not:

```js
console.log(omid.hasOwnProperty("name")); //true
console.log(omid.hasOwnProperty("species")); //false
```

##### **_Prototype chain_**

Every objects in JavaScript has a prototype. Remember that arrays and functions are also objects in JavaScript. An object and its prototype form a prototype chain, but the chain is not always this short.

We saw that the prototype of `omid` is `Person.prototype`. However, `Person.prototype` itself is an object, and should have its own prototype, and it actually does. `Person.prototype` is a simple object, meaning that it was created by the `Object` constructor function. So the prototype of `Person.prototype` is `Object.prototype`. This is usually the final ring of the prototype chain. The prototype of `Object.prototype` is `null`. This is very similar to the _scope chain_.

> **_Note_** | we can add methods to the JavaScript built-in prototypes like `Array.prototype` and `Object.prototype`. However, extending these prototypes is generally not a good idea: next versions of JavaScript might include a method with the same name that you added, and this will break your code. Also, doing this while working in teams may make some troubles during the project development.

```js
console.log(omid.__proto__.__proto__); // Object.prototype
```

For example, the prototype chain for a simple array is like:

```js
const arr = [1, 2, 3];
console.log(arr.__proto__); // Array.prototype
console.log(arr.__proto__.__proto__); // Object.prototype
```

When we call the `hasOwnProperty` method on an object like `omid`, JavaScript will first start looking for the method on the object itself. If it is not there, it will go up the prototype chain and look for the method in `omid`'s prototype, which is `Person.prototype`. If it is not there too, it will go up the prototype chain on level further and look into `Object.prototype`. This is where it will find and call the method.

##### **_Inheritance between constructor functions (classes)_**

This is a situation where we define 2 constructor functions, and we want one (child) to extend another (parent). For example, we want a `Person` constructor function, and a `Student` constructor function to extend `Person`.

We define the `Person` constructor function as:

```js
const Person = function (name, birthYear) {
  this.name = name;
  this.birthYear = birthYear;
};

Person.prototype.calaAge = function () {
  return 2037 - this.birthYear;
};
```

Then we define the `Student` constructor function, and call the `Person` constructor function in it. It is important to note here that the `Person` constructor function needs to use `this`. So calling the `Person` in `Student` should not be a regular function call, since in a regular function call, `this` is `undefined`. We can use the `call` method on `Person` to be able to define `this` manually.

```js
const Student = function (name, birthYear, course) {
  Person.call(this, name, birthYear);
  this.course = course;
};

Student.prototype.introduce = function () {
  console.log(`My name is ${this.name} and I study ${this.course}`);
};
```

We can then create an instance of `Student`:

```js
const omid = new Student("Omid", 1992, "Photography");
```

> **_Note_** | up until this point, any instance created from the `Student` constructor function will not have access to instance methods defined on `Person.prototype`. They will only have access to instance methods defined on `Student.prototype`. We need to manually establish the prototype chain, meaning that we want to set the `__proto__` of `Student.prototype` to `Person.prototype`.

```js
const Student = function (name, birthYear, course) {
  Person.call(this, name, birthYear);
  this.course = course;
};

Student.prototype = Object.create(Person.prototype);
// linking prototypes should be implemented right at this point of code, before defining any instance methods, otherwise it would overwrite all instance methods and delete them since it returns an empty object.

Student.prototype.introduce = function () {
  console.log(`My name is ${this.name} and I study ${this.course}`);
};
```

#### **2. ES6 Classes:**

this introduced classes to JavaScript. However, this is not exactly what we mean by 'classes' in traditional OOP. ES6 classes do **NOT** behave like classes in traditional OOP.

##### **_Defining a class and instance properties_**

To declare classes in JavaScript we use a special syntax. Remember that a class is a special type of function. Inside the class, a `constructor` function should be defined. This constructor function behaves exactly the same way as the regular JavaScript constructor function.

```js
class Person {
  constructor(name, birthYear) {
    // instance properties
    this.name = name;
    this.birthYear = birthYear;
  }
}
```

> **_Note_** | we can also define properties that are not based on inputs.

```js
class Person {
  constructor(name, birthYear) {
    // instance properties
    this.name = name;
    this.birthYear = birthYear;
    this.movements = [];
    this.locale = navigator.language;
  }
}
```

##### **_Defining methods_**

We can simply write methods after the constructor function. These methods will not be copied into the instances, they will be accessed by the instances through their prototype.

```js
class Person {
  constructor(fullName, birthYear) {
    // instance properties
    this.fullName = fullName;
    this.birthYear = birthYear;
  }

  // instance methods: will be added to Person.prototype
  calcAge() {
    return 2037 - this.birthYear;
  }
}
```

> **_Note_** | we can still define methods on the `prototype` property of the `Person` class. It is just simpler to write it in the class declaration.

```js
Person.prototype.greet = function () {
  console.log(`Hey ${this.fullName}`); //Hey omid
};
```

##### **_Creating an object (instance)_**

To create an instance of a declared class, we use the exact same syntax as before:

```js
const omid = new Person("Omid Armat", 1992);
```

Here are some tips to remember about ES6 classes:

- Classes are **NOT** hoisted.
- Classes are **first-class citizens**. We can pass them into functions and we can also return them from functions.
- Classes are always executed in **strict mode**.

##### **_Defining getters and setters_**

Every object in JavaScript can have getter and setter properties. These are calls **Assessor properties**, while normal properties are called **Data properties**.

Getters and setters are functions that get and set values, but on the outside, they look like regular properties.

We can also define setters and getters in classes.

```js
class Person {
  constructor(name, birthYear) {
    // instance properties
    this.name = name;
    this.birthYear = birthYear;
  }

  // instance methods: will be added to Person.prototype
  get age() {
    return 2037 - this.birthYear;
  }
}
```

To call this getter function, we should not write a function call syntax. We should use the method as a property.

```js
console.log(omid.age);
```

Setters are usually used for data validation before being persisted into an object. Also remember that setter methods should always receive at least one argument.

```js
class Person {
  constructor(fullName, birthYear) {
    // instance properties
    this.fullName = fullName;
    this.birthYear = birthYear;
  }

  // instance methods: will be added to Person.prototype
  get age() {
    return 2037 - this.birthYear;
  }

  set fullName(name) {
    if (name.includes(" ")) this._fullName = name;
    // creates _fullName instead of fullName property
    else alert(`${name} is not a full name.`);
  }
}
```

In order to be able to retrieve the `fullName` variable while we don't actually have it stored on the object, we should implement a getter function with the `fullName` name.

```js
class Person {
  constructor(fullName, birthYear) {
    // instance properties
    this.fullName = fullName;
    this.birthYear = birthYear;
  }

  // instance methods: will be added to Person.prototype
  get age() {
    return 2037 - this.birthYear;
  }

  set fullName(name) {
    if (name.includes(" ")) this._fullName = name;
    // creates _fullName instead of fullName property
    else alert(`${name} is not a full name.`);
  }

  get fullName() {
    return this._fullName;
  }
}
```

##### **_Defining static methods_**

To define a static method on the `Person` class:

```js
class Person {
  constructor(fullName, birthYear) {
    // instance properties
    this.fullName = fullName;
    this.birthYear = birthYear;
  }

  // static methods
  static hey() {
    console.log("Hey there!");
  }
}
```

We should then call the `hey` method on the `Person` class, and not on its instances.

```js
Person.hey();
```

##### **_Inheritance between ES6 classes_**

We first define a `Person` class:

```js
class Person {
  constructor(fullName, birthYear) {
    // instance properties
    this.fullName = fullName;
    this.birthYear = birthYear;
  }

  // instance methods: will be added to Person.prototype
  calcAge() {
    return 2037 - this.birthYear;
  }
}
```

Then we define a `Student` class knowing that it `extends` the `Person` class. The `extends` keyword will make the `Student` class to inherit from the `Person` class, it will link the prototypes for us. We also need to call the `super` function inside the `Student`'s constructor function. `super` is the constructor function of the parent class `Person`, and it is responsible for defining `this` in the child class.

```js
class Student extends Person {
  constructor(fullName, birthYear, course) {
    super(fullName, birthYear); // defines this, so should be called before other code

    // instance properties
    this.course = course;
  }

  // instance methods
  introduce() {
    console.log(`My name is ${this.fullName} and I strudy ${this.course}`);
  }
}
```

> **_Note_** | It is not necessary for the child class to accept additional instance properties compared to the parent class. In such case, we would not have to define the constructor function in the child class, and still all instances of `Student` will get their `fullName` and `birthYear` instance properties, because `Student` would still _extend_ `Person`. Just keep in mind that no constructor function, means no `super` function call, and therefore `this` would be `undefined`.

#### **3. `Object.create()`:**

this is the easiest way of linking an object to a prototype object. However, this syntax is not used much.

In this last way of implementing OOP programming, the idea is still based on prototypal inheritance, but there are no `prototype` properties involved. Also, there is no constructor function, and no `new` operator.

We use `Object.create()` to manually set the prototype of an object, to any other object that we want. For example, we can now create a new object and make it the prototype of all the person objects.

##### **_Defining a prototype object and instance methods_**

The prototype objects would be defined as a simple JavaScript object. However, to make the instances be created programmatically, we need to implement a method like `init` in this object that will place instance properties as they are passed into it. This would be very similar to a constructor function, but it actually has nothing to do with it. It is just a regular method available on an object.

```js
const Person = {
  // instance methods
  init(name, birthYear) {
    this.name = name;
    this.birthYear = birthYear;
  }

  calcAge() {
    return 2037 - this.birthYear;
  },
};
```

##### **_Creating an object (instance)_**

```js
const omid = Object.create(Person);
// creates an empty object
```

to input data into this object is it is defined in the `Person` object, we should call the `init` method on it.

```js
omid.init("Omid", 1992);
```
