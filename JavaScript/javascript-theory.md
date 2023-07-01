# **Data structures**

## **Arrays**

An array acts a container into which we can store variables and then reference them.

We have two ways of defining an array:

```js
const friends = ["masoud", "amirhossein", "behzad"];
// or
const friends = new Array("masoud", "amirhossein", "behzad");
```

> **_Note_** | an array can hold as many values as we want, and also of any type that we need. It is even possible to insert an expression, a variable containing a value, or another array as an element.

### **Retrieve elements from array**

In order to retrieve an element from an existing array we can use the bracket notation with the index of the required element in it.

```js
console.log(friends[0]);
```

> **_Note_** | inside the bracket we can insert any **expression**. Remember that expression is anything that can produce a value. We canno put a **statement** here.

> **_Note_** | a new array method (`.at()`) was introduced in ES2022 that enables us to retrieve elementes in another way. This method can also count the elements index from the end using negative indexes. Getting the last element with this method requires `-1` as the index passed into it. This method is particularly useful when we want to do method chaining, or just retrieve elements from the end of an array.

```js
const arr = [1, 2, 3];
console.log(arr.at(0)); // 1
console.log(arr.at(-1)); // 3
console.log(arr.at(-2)); // 2
```

### **Mutate elements of array**

The bracket notation also allows us to mutate array elements.

```js
friends[2] = "maryam";
```

> **_Note_** | this works becasue an array is not a primitive value. Remember that primitive values declared with `const` are not immutable. However, we cannot replace (redefine) the entire array.

### **Length of array**

Length of an array is the number of elements that the array holds in it. We can access this value with the `length` property of the array.

```js
console.log(friends.length); // not zero-based
```

> **_Note_** | This can be useful when we want to retrieve the last element of an array.

```js
console.log(friends[friends.length - 1]);
```

### **Array methods**

There are many array methods that we can attach to arrays in order to perform some operations on them.

#### **Add elements**

**`.push()`**: adds elements to the end of an array.

- Receives one argument: data of any type that should be added to the array.
- Returns the `length` of the updated array. (We rarely use this value).

**`.unshift()`**: adds elements to the beginning of an array.

- Receives one argument: data of any type that should be added to the array.
- Returns the `length` of the updated array. (We rarely use this value).

#### **Remove elements**

**`.pop()`**: removes the last element of an array.

- Receives no argument.
- Returns the removed element.

**`.shift()`**: removes the first element of an array.

- Receives no argument.
- Returns the removed element.

#### **Find elements**

**`.indexOf()`**: finds the index of a certain element in the array.

- Receives the element value.
- Returns the element's index (zero-based). If there is no such element, returns `-1`.

**`.find()`**: used to retrieve one element of an array based on a condition.

- Does NOT mutate the original array.
- Receives a callback function that is called in each iteration in order to check the current element with the condition.
- Returns the first element in the array that satisfies the condition. (unlike `.filter()` the returns a new array of all the elements that satisfy the condition)

```js
const movements = [200, 450, -400, 3000, 650];
const firstWithdrawal = movements.find((mov) => mov < 0);
```

**`.findIndex()`**: works almost the same way as `.find()`.

- Does NOT mutate the original array.
- Receives a callback function that is called in each iteration in order to check the current element with the condition.
- Returns the index of the first element in the array that satisfies the condition.

```js
const movements = [200, 450, -400, 3000, 650];
const firstWithdrawal = movements.findIndex((mov) => mov < 0);
```

#### **Check element existence**

**`.includes()`**: Checks through _strict equality_ if a certain element exists in the array.

```js
const movements = [200, 450, -400, 3000, 650];
console.log(movements.includes(-400)); //true
```

- Receives the element value.
- Returns boolean.

**`.some()`**: Checks whether there is **any element** in an array that satisfy a given condition.

- Receives a callback function where the condition is defined.
- Returns boolean.

```js
const movements = [200, 450, -400, 3000, 650];
console.log(movements.some((mov) => mov > 500)); //true
```

**`.every()`**: Checks whether **all elements** of an array satisfy a given condition.

- Receives a callback function where the condition is defined.
- Returns boolean.

```js
const movements = [200, 450, -400, 3000, 650];
console.log(movements.every((mov) => mov > 500)); //false
```

#### **Looping over array**

**`.forEach()`**: used to loop over an array. It receives a callback function in order to tell it what to do. So it is the `forEach()` method that will call the callback function, not us. The method loops over the array and in each iteration, it will call the callback function.

- Receives a callback function as argument.
- Callback has access to: 1) current element of array, 2) current element's index, 3) the entire array that is being looped. (order matters)

```js
const movements = [200, 450, -400, 3000, -650, -130, 70, 1300];

movements.forEach((mov, i, arr) => {
  if (mov > 0) {
    console.log(`Movement ${i + 1}: You deposited ${mov}`);
  } else {
    console.log(`Movement ${i + 1}: You withdrew ${mov}`);
  }
});
```

> **_Note_** | unlike for-of loop, we cannot break out of a forEach loop. Once it starts, it will go to the end. We cannot use `continue` and `break` in a `forEach` loop.

##### **Data transformation methods**

There are 3 important array methods to perform data transformations, the results of each are always stored in new arrays.

**`.map()`**: yet another method, used to loop over arrays. As it loops over the array, in each iteration, it calls a callback function that pass into it.

- Does NOT mutate the original array.
- Receives a callback function.
- Callback has access to: 1) current element of array, 2) current element's index, 3) the entire array that is being looped.
- Returns a new array based on an operation that it does on the original array. The value that is returned by the callback function in each iteration will be pushed to the new array.

```js
const movements = [200, 450, -400, 3000, 650];
const movementsUSD = movements.map((mov, i, arr) => mov * 1.1);
```

**`.filter()`**: used to filter elements in the original array that satisfies a condition that is checked by a callback function that we pass into the method.

- Receives a callback function.
- Callback has access to: 1) current element of array, 2) current element's index, 3) the entire array.
- Returns a new array including the elements that satisfy the condition that is checked by the callback function that we pass into the callback function.

```js
const movements = [200, 450, -400, 3000, 650];
const deposites = movements.filter((mov, i, arr) => mov > 0);
```

**`.reduce()`**: used to boil down all the elements of an array into one single value. This is usually used to calculate totals, averages, etc. of elements stored in an array.

- Receives two arguments: a callback function and the starting number for the accumulator variable. The callback loops over the array and
- Callback has access to: 1) accumulator variable, 2) current element, 3) current element's index, 4) the entire array.
- Returns a single value.

```js
const movements = [200, 450, -400, 3000, 650];
const balance = movements.reduce((acc, mov, i, arr) => {
  return acc + mov;
}, 0);
```

#### **Other array methods**

**`.slice()`**: extracts a slice of any array, without chainging the original array.

- Does NOT mutate the original array.
- Receives either 1 or 2 arugments: in either case, the first argument will be the starting index for slicing. The element related to the starting index will be included in the slice. If there is a second argument, it would be the ending index of the slice, which will not be included in the slice. Inserting one negative index will start slicing from the end of the array. Negativa and positive indexes can be used together as the starting and ending indexes.
- Returns a new array with the slice part extracted from the original array.

```js
let arr = ["a", "b", "c", "d", "e"];
console.log(arr.slice(2)); // ['c', 'd', 'e']
console.log(arr.slice(2, 4)); // ['c', 'd']
console.log(arr.slice(-1)); // ['e']
consoloe.log(arr.slice(1, -2)); // ['b', 'c']
```

> **_Note_** | it is also possible to create shallow copies with the slice method. Just use it with no index.

```js
const arrCopy = arr.slice();
```

**`.splice()`**: works very similar to `.slice()`, but actually mutates the original array. The extracted elements will be gone from the original array.

Use case: when we want to delete a specific element from the array. (`.splice(<index>, 1)`)

- Mutates the original array
- Receives either 1 or 2 arugments: first the starting index and then the delete count.
- Returns a new array with the slice part extracted from the original array. But we are usually not interested in what it returns, we just need its deletion operation to be performed on the original array.

```js
let arr1 = ["a", "b", "c", "d", "e"];
arr.splice(2); // arr1 = ['a', 'b']

let arr2 = ["a", "b", "c", "d", "e"];
arr.splice(1, 2); // arr2 = ['a', 'd', 'e']
```

**`.reverse()`**: reverses the order of elements in an array. It mutates the original array.

- Mutates the original array
- Receives no argument.
- Returns the same array after its elements being reversed.

```js
let arr = ["a", "b", "c", "d", "e"];
console.log(arr2.reverse());
```

**`.concat()`**: used to concatenate two arrays.

- Does NOT mutate the original array
- Receives the other array that should be attached to the array that the method as called upon.
- Returns a new array.

```js
let arr1 = ["a", "b", "c", "d", "e"];
let arr2 = ["f", "g", "h"];
const letters = arr1.concat(arr2);
console.log(letters); // ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
```

**`.join()`**: used to join the elements of an array.

- Does NOT mutate the original array.
- Receives a character which will be inserted between the elements as they are joined together as a whole string.
- Returns a string.

**`.flat()`**: Introduced in ES2019, will flat a nested array for a specified depth.

- Does NOT mutate the original array.
- Receives one arguments: flatening level. If left empty, default is 1.
- Returns a new array.

```js
const arr = [[[1, 2], 3], [4, 5, 6], 7, 8];
console.log(arr.flat(2)); // [1, 2, 3, 4, 5, 6, 7, 8];
```

**`.flatMap()`**: Introduced in ES2019, executes `.map()` and then `.flat()` method on a given array of elements. Since the execution sequence is a pretty popular one, the method was introduced to perform it in one go.

> **_Note_** | The flatening operation can go only 1 level deep and we cannot increase it.

- Receives the callback function that we would normally pass into the `.map()` method.
- Returns a new flattened array.

**`.sort()`**: used to sort elements of an array based a sorting logic implemented in a callback function that is passed into the method. If no callback is passed into the method, it can only be used to sort string values in an array, not numbers.

- Mutates the original array.
- Receives a callback function where the sorting logic is implemented.
- Returns the original array with its elements sorted.

```js
const owners = ["omid", "ali", "saber", "nasrin"];
console.log(owners.sort());
```

For sorting arrays with numbers, the callback function will have 2 arguments as 2 consecutive elements of the array in each iteration. In each iteration, if the callback returns a positive value, `a` will be positioned before `b`. If the callback returns a negative value, `a` will be positioned after `b`.

```js
const movements = [200, 450, -400, 3000, 650];
movements.sort((a, b) => {
  // for ascending order
  if (a > b) return 1;
  if (a < b) return -1;

  // for descending order
  if (a > b) return -1;
  if (a < b) return 1;
});
```

> **_Note_** | this works with both numbers and strings. However, if we are attempting to sort numbers, the logic above can be simplified as:

```js
const movements = [200, 450, -400, 3000, 650];
movements.sort((a, b) => {
  // for ascending order
  return a - b;

  // for descending order
  return b - a;
});
```

### **Destructuring arrays**

Destructuring is an ES6 feature allowing us to unpack values from an array or an object into separate variables.

Whenever JavaScript detects `[]` on the left side of the equal sign, it knows that it should perform destructuring.

```js
const arr = [2, 3, 4];

const [x, y] = arr;
console.log(x, y); //2 3

const [a, , c] = arr;
console.log(a, c); //2 4
```

> **_Note_** | Attempting to retrieve more variables than the actual length of the array will result in `undefined`. However, we can prevent producing an `undefined` value by definging default values.

```js
const arr = [2, 3, 4];

const [a = 1, b = 1, c = 1] = arr;
console.log(a, b, c); //2 3 1
```

> **_Note_** | the original array is not destroyed with destructuring.

### **Spread operator for arrays**

Spread operator is used to expand an array into its elements. It is usually used when we want to create a new array based on a previous array, but the new array is intended to have some determined elements and then include all the elements of the previous array.
So the spread operator (`...`) will take out the elements of an array and automatically write its elements with a comma between them, just as we would do manually.

**In other words:** we use the spread operator whenever we would otherwise write multiple values separated by commas.

> **_Note_** | spread operators work on all iterables. Iterables in JavaScript include arrays, strings, maps, and sets, but not objects.

> **_Note_** | the `...` syntax is considered by JavaScript as the spread operator if it is used on the right side of the equal sign. If it is on the left side of the equal sign, it will be considered as the **rest pattern**, which would usually be used together with the destructuring syntax. Also this syntax would be considered as the rest pattern if it is used in the arguments of a function.

Use cases:

1. when we want to rewrite the elements of an array in a new array, and

```js
const arr = [7, 8, 9];
const newArr = [5, 6, ...arr];
console.log(newArr); // [5, 6, 7, 8, 9]
```

2. when we want to pass multiple arguments into functions.

```js
const arr = [1, 2, 3];
const calcAvg = function (val1, val2, val3) {
  const avg = (val1 + val2 + val3) / 3;
};

calcAvg(...arr);
```

3. create shallow copies of arrays.

```js
const menuCopy = [...restaurant.mainMenu];
```

4. Join two or more arrays.

```js
const wholeMenu = [...restaurant.starterMenu, ...restaurant.mainMenu];
```

### **Rest pattern in arrays**

The rest pattern looks exactly like the spread operator, but it does the opposite. Rest pattern is used to condence or pack multiple elements into one array. The rest pattern is usually used together with the destructuring syntax.

**In other words:** we use the rest pattern whenever we would otherwise write multiple variable names separated by commas.

Use cases:

1. to destructure multiple elements from the beginning of an array into new variables and leave all the _rest_ in another variable. In this use case, the rest pattern should be last element of the destructuring syntax.

```js
const [a, b, ...others] = [1, 2, 3, 4, 5];
console.log(others); // [3, 4, 5]
```

2. to pass multiple arrguments into a function, and also make the function ready to receive any arbitrary amount of arguments:

```js
const add = function (...numbers) {
  let sum = 0;
  for (let i = 0; i < numbers.length; i++) sum += numbers[1];
};

add(2, 3);
add(5, 3, 6, 2);
```

This situation can be used together with the same use case of the spread operator.

```js
const numbers = [2, 5, 5, 6, 3, 5, 3];
const add = function (...numbers) {
  let sum = 0;
  for (let i = 0; i < numbers.length; i++) sum += numbers[1];
};

add(...numbers);
```

## **Objects**

Objects are the most fundamental concept in the whole JavaScript language.

In arrays there is no way of giving names to elements. So we are not able to reference them by a name, but only with their index number. Objects, however, provides this option.

In objects we define key-value pairs. So each value will have a key (property) that can be referenced by it.

There are multiple ways of creating objects. This is the object literal syntax:

```js
const omid = {
  name: "omid",
  age: 2037 - 1992,
  job: "developer",
  friends: ["amirhossein", "behzad", "maryam"],
};
```

After defining the object, we can still add key-value pairs to it using the dot notation:

```js
omid.location = "iran";
```

### **Retrieve data from obejct**

Unlike arrays, the order of properties does not matter when we want to retrieve them. To retrieve data from an object we have two ways:

- Bracket notation:

```js
console.log(omid.name); //omid
```

- Dot notation: the bracket notation can receive any expression in it. We don't need to explicitely write the property name. We can generate it programmatically with an expression.

```js
console.log(omid["name"]); //omid
```

> **_Note_** | when we try to retireve a property that does not exist in an object, we receive `undefined`. This implies that we can, in a sense, remove a property from an object by setting it to `undefined`.

### **Object methods**

Since functions are yet another type of values in JavaScript, we can add functions as key-value pairs to objects. Functions defined in objects are also called **methods**.

```js
const omid = {
  name: "omid",
  birthYear: 1992,

  // can only insert function expression, not function declaration
  calcAge: function () {
    this.age = 2037 - this.birthYear;
  },
};

omid.calcAge();
// or
omid["calcAge"]();
```

> **_Note_** | `this` refers to the object that is calling the method.

### **Destructuring objects**

Destructuring is an ES6 feature allowing us to unpack values from an array or an object into separate variables.

Whenever JavaScript detects `{}` on the left side of the equal sign, it knows that it should perform destructuring objects.

```js
const omid = {
  name: "omid",
  age: 2037 - 1992,
  job: "developer",
  friends: ["amirhossein", "behzad", "maryam"],
};

const { name, age, job } = omid; //variable names should match the exact property names of the object
```

> **_Note_** | we can rename variables as we create them in destructuring:

```js
const { name: fullname, age, job: occupation } = omid;
```

> **_Note_** | Attempting to retrieve variables that don't exist in the object will result in `undefined` value. However, we can set default values just like with array destructuring. Notice that we can both rename and provide default value at the same time.

```js
const { name, age, job, location: country = "iran" } = omid;
```

> **_Note_** | to destructure nested objects we nest the destructuing syntax like this:

```js
const restaurant = {
  name: 'italiano';
  openingHours: {
    fri: {
      open: 12,
      close: 23,
    }
  }
}

const {
  fri: { open, close },
} = restaurant.openingHours;
// renaming and default values also work in this case
```

> **_Note_** | we can destructure an object immediately as we receive it in a function. Default values can be set here also.

```js
const restaurant = {
  name: 'italiano';
  openingHours: {
    fri: {
      open: 12,
      close: 23,
    }
  }

  orderDelivery: function({starterIndex, mainIndex, time, address}) {
    console.log(starterIndex, mainIndex, time, address);
  }
}

restaurant.orderDelivery({
  time: '20:45',
  address: 'Ahmad Abad St.',
  mainIndex: 2,
  starterIndex: 3,
})
```

### **Spread operator for objects**

Since ES2018 spread operators can operate on objects although objects are not iterables.

```js
const newRestaurant = { ...restaurant, founder: "Philipo", foundedIn: 1998 };
```

We can also create shallow copies of objects:

```js
const restaurantCopy = { ...restaurant };
```

### **Rest pattern in objects**

The rest pattern looks exactly like the spread operator, but it does the opposite. Rest pattern is used to condence or pack multiple elements into one object.

Use cases:

1. to destructure multiple properties of an object and then pack them into a new object and leave all the _rest_ in another object.

```js
const { sat, ...weekDays } = restaurant.openingHours;
```

# **Object-Oriented Programming**

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

> **_Note_** | we can also define properties that are not based on inputs. They will just be set by the constructor function

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

> **_Note_** | any code can be inserted into the constructor function and it would be executed once the constructor function is called.

```js
class Person {
  constructor(name, birthYear) {
    // instance properties
    this.name = name;
    this.birthYear = birthYear;
    this.movements = [];
    this.locale = navigator.language;

    // any executable code
    console.log(`Thanks for opening an account, ${name}`);
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

> **_Note_** | methods defined in a class can call each other.

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

##### **_Data Encapsulation_**

It means to keep some properties and methods private inside a class so that they are not accessible from outside the class. There are 2 main reasons why we need encapsulation and data privacy:

1. prevent code from outside the class to accidentally manuipulate data inside the class.
2. encapsulation enables us to expose only a small public interface of the class, and this, in turn, allows us to change all other internal methods with confidence, because this way we can be sure that external code does not rely on these internal private methods and our code will not break.

In order to make properties and methods fake-private, we add an underscore at the beginning of their names:

```js
class Student {
  constructor(name, birthYear, pin) {
    this._pin = pin;
  }

  _approveLoan(val) {
    return true;
  }
}
```

> **_Note_** | this does not make the property truly private, it is just a convention and they are still accessible with the underscore. Therefore, we call these _protected properties_.

In traditional OOP, properties are called **class fields**. With the current proposal of implementing private class fields in JavaScript, the language is actually giving its classes some abilities that they didn't have previously.

In this proposal, there are 6 different kinds of fields and methods:

1. Public fields
2. Private fields (fields cannot be defined in constructor functions, they should be defined outside. Then the constructor can access them via `this`)
3. Public methods
4. Private methods
5. Public static methods
6. Private static methods

```js
class Account {
  // public fields (available on all instances)
  locale = navigator.language;

  // private fields (not accessible from outside the class)
  #movements = [];
  #pin;

  constructor(name, birthYear, pin) {
    this.#pin = pin;
  }

  // private methods (currently not supported by any browser)
  #approveLoan(val) {
    return true;
  }
}
```

##### **_Making class methods chainable_**

Each method defined in the class should `return` the object (`this`) after all its process.

```js
class Account {
  #movements = [];
  #pin;

  constructor(name, birthYear, pin) {
    this.#pin = pin;
  }

  deposit(val) {
    this.#movements.push(val);
    return this;
  }

  requestLoan(val) {
    this.deposit(val);
    return this;
  }
}
```

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

# **MVC architecture**

## **Publisher-subscriber pattern**

According to the MVC architecture, we must be able to handle all application logic in Controller, and handle all presentation logic in View. Therefore, we should be able to listen for events in View, and handle events in Controller. The solution is the publisher-subscriber pattern.

The publisher-subscriber pattern involves event listeners attached to DOM elements in View, and events handled by Controller functions living in the controller module.

In this pattern, publisher is the code that knows when to react. It will certainly involve the `addEventListener` method and it is written in View. On the other hand, there is a subscriber which is the code that actually performs the reaction to the event, so it is the code that should be executed when the event happens. It is written in Controller.

The actual implementation of this solution will include a controller `init` function which passes the subscriber into the publisher, so that the publisher would know that the subscriber even exists. The `init` will be called as soon as the program is loaded, and it will, in turn, call the publisher and pass the subscriber into it.

**`controller.js`:**

```js
const init = function () {
  recipeView.addHandlerRender(handler);
};

init();
```

**`view.js`:**

```js
// publisher is usually implmented as a public API of a view class
addHandlerRender(handler) {
  window.addEventListener('load', handler);
}
```

# **Working with the DOM**

DOM stands for Document Object Model. It is a structured representation of HTML documents which allows JavaScript to access and manipulate HTML elements. So the DOM is the connection between HTML documents and JavaScript code.

The DOM is automatically created by the browser as soon as the HTML page loads. It is stored in a tree structure of nodes, where each HTML element is an object. In the DOM tree, for each HTML element there is one element node that we can manipulate and interact with. The DOM also allows us to respond to certain DOM events using the JavaScript code.

The DOM always starts with the document object. Document is a special object that we can access in JavaScript. It serves as an entry point into the DOM as we can easily examine this by using the `querySelector` method on it to select any HTML element:

```js
document.querySelector(".class");
```

The first child element of the document is usually the `<html>` element. This is usually the root element in all HTML documents.

Next, the `<html>` element usually has two child elements: `<head>` and `<body>`. These are adjacent elements, so they are siblings in the DOM.

The DOM has more than just element nodes. It also has nodes for each group of text characters (e.g text inside a `<p>` element), comments and other stuff.

> **_Note_** | the rule is that whatever is in the HTML document, also has to be in the DOM.

> **_Note_** | DOM is not part of the JavaScript language. DOM allows us to make JavaScript code impact the appearance of webpages. **Web APIs** make it possible to work with DOM and DOM methods. Web APIs are libraries written in JavaScript and implemented by browsers, which we can access from our JavaScript code. Besides the DOM, there are many other web APIs like timers, fetch API, and so on.

## **A detailed look into the DOM**

The DOM API allows JavaScript to programmatically interact with the DOM. So the DOM actually contains a ton of methods and properties that we use to interact with the DOM tree. (e.g `querySelector`, `addEventListener`, and `createElement` methods, or `innerHTML`, `textContent`, and `children` properties among many others)

There are different types of nodes in the DOM. Some nodes are HTML elements, but others are just text. This is important because DOM methods and properties are organized into these different types of objects.

### **DOM organization**

Every single node in the DOM tree is of the type **Node**. Each node is represented in JavaScript by an object. This object has access to different node methods and properties, such as `textContent`, `childNodes`, `parentNodes`, `cloneNodes` among many others.

This Node type has a couple of child types: **Element**, **Text**, **Comment**, **Document**.

- `Window` node

- `Node` node: every single node in the DOM is of this type. Each `Node` is represented in JavaScript by an object that has access to special methods and properties, such as `.textContent`, `.childNodes`, `.parentNode`, `cloneNode` among many others.

  - `Element` node: each HTML element is of this type. Gives each HTML elemtn access to a ton of useful methods and properties, such as `innerHTML`, `classList`, `children`, `parentElement`, `append()`, `remove()`, `querySelector()`, `closest()` and so on. Each element is represented internally as an object.

    - `HTMLElement` node: this node type would have exactly one child type for each HTML element that exists in the HTML file. Each of these HTML elements can have unique properties. (e.g `src` attribute of the `<img>` element, or `href` attribute of the `<a>` element)

      - HTMLDivElement
      - HTMLButtonElement

  - `Text` node: text inside any element gets its own Text node.
  - `Comment` node: comment in the HTML file gets its Comment node.
  - `Document` node: has access to methods and properties, such as `querySelector()`, `createElement()`, `getElementById()`.

> **_Note_** | Inheritance makes the relation between these node types work. So all the child types will have access to methods and properties of their parent node types. Note how the Document node type and Element node type both have access to `querySelector()`.

The DOM needs to provide all node types with the ability to listen to events. Remember that we usually listen to events by calling the `addEventListener` method on an Element or Document node type. The DOM has another node type called `EventTarget` which is a parent of both the `Node` and the `Window` node types. So actually, we can call the `addEventListener` method on every single type of node.

## **Selecting elements**

### **Select document, head and body**

To select the document element in order to apply CSS styles we don't need to use any selector:

```js
const doc = document.documentElement;
```

We can also select the `head` and `body` elements:

```js
const head = document.head;
const body = document.body;
```

### **Select elements with `querySelector()`**

> Frequently used

We can use any CSS selector with the`querySelector()` method in order to select one element.

- Returns the first element that matches the query.

```js
const header = document.querySelector(".header");
```

### **Select elements with `querySelectorAll()`**

> Frequently used

We can use any CSS selector with the`querySelectorAll()` method in order to select a series of elements.

- Returns a `NodeList` containing all the elements that match the query. Remember that a `NodeList` is not a live list.

```js
const allSections = document.querySelectorAll(".section");
```

> **_Note_** | `querySelector()` and `querySelectorAll()` are available not only the document, but also on all the elements. Using them on elements is usually with the goal of selecting child elements.

### **Select elements with `getElementById()`**

We can select elements only with their ID in this method. We don't need to insert the CSS ID selector actually.

- Returns the only element with the inserted ID.

```js
const map = document.getElementById("map");
```

### **Select elements with `getElementsByTagName()`**

Used to selec all elements with the same tag name.

- Returns a `HTMLCollection`, which is a live collection, meaning that if the DOM changes, this collection is immediately updated.

```js
const allButtons = document.getElementById("button");
```

### **Select elements with `getElementsByClassName()`**

Used to selec all elements with the same class name.

- Returns a `HTMLCollection`.

```js
const allButtons = document.getElementsByClassName("button");
```

## **Creating and inserting elements**

### **Create elements with `insertAdjacentHTML()`**

Used to insert HTML markup into a certain HTML element.

- Accepts two arguments:

  1. Determine where the HTML markup should be inserted in the HTML element: `beforeend`, `beforebegin`, `afterend`, `afterbegin`.
  2. HTML markup code

```js
const section1 = document.querySelector('.section-1');
section1.insertAdjacentHTML('beforebegin', <markup-code>);
```

### **Create elements with `createElement()`**

used to create an HTML element.

- Accepts one argument: string containing the tag name.
- Returns an HTML element with the specified tag name.

```js
const message = document.createElement("div");
```

> **_Note_** | All this does is to create a DOM element. It is not yet in the DOM itself, and it cannot yet be found on the webpage. We have to manually insert it into the page.

We can also add classes to this newly created element.

```js
message.classList.add("cookie-message");
```

We can add text to this element.

```js
message.textContent =
  "We use cookies for improved functionality and analytics.";
```

We can also insert HTML code into this element.

```js
message.innerHTML = '<button class="btn btn--close-cookie">Got it!</button>';
```

> **_Note_** | we can use the `innerHTML` property to both read and set the HTML markup.

Finally, to insert this element really into the DOM, we can use `prepend()`, `append()`, `before()`, or `after()`.

### **Insert element with `prepend()`**

Used to insert an element at the beginning of another element.

- Accepts one argument: the element that should be inserted.

```js
header.prepend(message);
```

### **Insert element with `append()`**

Used to insert an element at the end of another element.

- Accepts one argument: the element that should be inserted.

```js
header.append(message);
```

> **_Note_** | one DOM element is unique and cannot exist at two places at the same time. Therefore, in a code example where both prepend and append are used, only the last method used will affect the DOM. However, if we need the same element appear in two places, we have to make a copy of it using the `cloneNode()` method.

```js
header.prepend(message);
header.append(message.cloneNode(true)); // true determines that all the child elements of the message will also be copied
```

### **Insert element with `before()`**

Uset to insert an element as a sibling, before another element.

- Accepts one argument: the element that should be inserted.

```js
header.before(message);
```

### **Insert element with `after()`**

Uset to insert an element as a sibling, after another element.

- Accepts one argument: the element that should be inserted.

```js
header.after(message);
```

### **Delete element with `remove()`**

Used to delete elements, usually based on a click or timer event.

```js
document
  .querySelector(".btn--close-cookie")
  .addEventListener("click", function () {
    message.remove();
  });
```

> **_Note_** | previously, before the `remove()` method became available in JavaScript, we had to move up the DOM to select the parent element, and then remove the child element using the `removeChild()` method, into which we had to pass in the element that should be removed again.

```js
document
  .querySelector(".btn--close-cookie")
  .addEventListener("click", function () {
    message.parentElement.removeChild(message);
  });
```

## **Manipulating styles, attributes and classas**

### **Manipulate styles**

In order to manipulate the style of an element, we should select the `style` property of that element, and then select a specific css property on it.

```js
message.style.backgroundColor = "#374956";
message.style.width = "120%";
```

> **_Note_** | Styles set through JavaScript code are inserted into the HTML file as inline styles. Therefore, we cannot use the `style` property to read styles defined outside the HTML file, for example, in a CSS file. However, we can use it to read inline styles.

> **_Note_** | in order to get non-inline styles of an element, we can use the `getComputedStyle()` function. It receives the target element as an argument. It returns a `CSSStyleDeclaration` object containing all the styles with which the element is appearing on the page. So these styles are not necessarily written in the CSS file.

```js
console.log(getComputedStyle(message));
```

### **Manipulate CSS custom properties**

We can change the values stored in CSS custom properties using JavaScript. As we know, CSS custom properties are stored in the document root, and in JavaScript that is equivalent to the document element.

In order to achieve this we can use the `setProperty()` method on the style property of the document element.

```js
document.documentElement.style.setProperty("--color-primary", "orangered");
```

### **Manipulate HTML attributes**

We can read and set attributes in JavaScript.

```js
const logo = document.querySelector(".nav__logo");
console.log(logo.src); // returns absolute URL while in HTML file we write the relative URL. To get the relative URL we use getAttribute(). Same is true about 'href' for links.
console.log(logo.className); // NOT 'class'

logo.alt = "Beautiful minimalist logo";
```

> **_Note_** | this works only if the target attribute is a standard HTML attribute that the element is supposed to have it. So if we set these standard attributes in the HTML file, they will be accessible in JavaScript simply as properties of the element. However, if we set some non-standard properties on an element, we would only be able to access them using the `getAttribute()` method, into which we can pass the attribute name.

```js
const logo = document.querySelector(".nav__logo");
console.log(logo.designer);
```

> **_Note_** | we can also set non-standard attributes using the `setAttribute()` method. This method accepts as the first argument the attribute name, then as the second argument the attribute value.

```js
const logo = document.querySelector(".nav__logo");
logo.setAttibute("company", "bankist");
```

#### **HTML data attribute**

We can add a special data attribute for a HTML element. We frequently use this attribute when we need to store some data in the UI in order to basically create a bridge between the frontend and the backend code.

The name of this attribute should start with 'data-' and then we continue the name however we want. These attributes will then be accessible in JavaScript through the 'dataset' property of the element. Just notice how the dictation of the attributes name changes in JavaScript to cammelcase.

```html
<img class="nav__logo" data-verion-number="3.0" />
```

```js
const logo = document.querySelector(".nav__logo");
console.log(logo.dataset.versionNumber); //3.0
```

### **Manipulate classes**

In order to interact with classes of an HTML element we can use 4 methods on the `classList` property of the element:

1. `.add()`: adds a class name string to the classlist of the element.
2. `.remove()`: removes a class name string from the classlist of the element.
3. `.toggle()`: adds/removes a class name string to/from the classlist of the element if it doesn't/does alreadey exist.
4. `.contains()`: returns boolean whether the specified class name string exists on the classlist of the element. (Don't mistake it with `includes()` in arrays)

> **_Note_** | multiple class name strings can be passed into the `add()` and `remove()` methods separated by commas.

## **Events**

## **Event delegation**

In event delegation we use the fact that events _bubble up_. Utilizing this fact usually means to attach the event listener to a common parent of a series of elements. Now if the user clicks on any of the elements in that parent element, an event is emited and we can catch it at the parent level as it bubbles up. We can also identify where the event is originating from using the `e.target` property.

Actual steps in utilizing event delegation:

1. Add the event listener to a common parent element of all the elements that we are interested in.
2. Determine what element originated the event.
3. Execute a custom command.

```js
document.querySelector(".nav__links").addEventListener("click", function (e) {
  if (e.target.classList.contains("nav__link")) {
    const id = e.target.getAttribute("href");
    // other executable commands
  }
});
```

> **_Note_** | Event delegation is a nice solution for situations where we want to work with elements that are not yet on the page in the runtime. This is a common use case of event delegation, especially with buttons that are added dynamically to the webpage while using the application.

Renamed master to branch on GitHub.