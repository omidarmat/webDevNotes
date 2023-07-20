# **Architectures**

## **Singleton**

A real-world Singleton can be thought of as a country's government. A country can have only one official government. Regarless of the personal identities of the individuals who form governments, the title 'The Government of X', is a global point of access that identifies the group of people in charge.

The Singlton design pattern is usually implemented to take care of 2 problems:

1. **To ensure that a class can have only one instance:** why would we want this? The most common reason is to control access to some shared resource - for instance, a **database connection** or some files. In this case, creating a separate database object for every other object may be costly. As another example, think of a single configuration manager or error manager in an application. In this case, a single object should handle all problems instead of creating multiple managers. So imagine you created an instance of a class, but after a while you decided to create a new one. This will return to you the object that you have already created, instead of creating a fresh object.

2. **Provise a global access point to that single instance:** lets you access some object from anywhere in the program, just like a global variable. However, it also protects that object from being overwritten by other code.

### **Applicability**

- Use the Singleton pattern when you need stricter control over global variables.
- Use the Singleton pattern when a class in your program should have just a single instance available to all clients; for instance, a single **database object** or connection shared by different parts of the program.

### **Implementation**

All implementations of the Singleton pattern involves 2 steps:

1. Make the default constructor _private_, to prevent other objects from using the `new` operator with the Singlton class.
2. Create a `static` creation method that acts as a constructor. Under the hood, this method will call the private `constructor` to create an object and saves it in a static field. Now all following calls to this static creation method will return the cached object.

> If your code has access to the Singleton class, it would be able to call the Singleton's static creation method. Whenever the method is called, the same object is always returned.

#### **Wanna do this?**

1. Add a private `static` field to the class for storing the singleton instance.
2. Declare a public `static` creation method for getting the singleton instance.
3. Implement **lazy initialization** inside the `static` method. It should create a new object on its first call and put it into the `static` field. The method should always return this stored instance on all subsequent calls.
4. Make the `constructor` of the Singleton class **private**. The `static` creation method will still be able to call the constructor, but not other objects.
5. All client code should replace their direct calls to the singleton's constructor with calls to its `static` creation method.

```js
class FancyLogger {
  constructor() {
    if (FancyLogger.instance == null) {
      this.logs = [];
      FancyLogger.instance = this;
    }
    return FancyLogger.instance;
  }

  log(msg) {
    this.logs.push(msg);
    console.log(`FANCY: ${msg}`);
  }

  printLogCount() {
    console.log(`${this.logs.length} logs`);
  }
}

const logger = new FancyLogger();
Object.freeze(logger); // This will prevent the logger object from being changed in any way by our code. So the object cannot have any new variables or methods added to or removed from it.
module.exports = logger;
```
