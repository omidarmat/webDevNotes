# **Design patterns**

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

## **Factory method**

Factory method is a creational design pattern that provides an interface for creating objects in a **superclass**, but allows subclasses to alter the type of object that will be created.

As a real-world scenario, think of a logistics company that starts its business with road logistics and it can only produce trucks. So it would propbably implement a `Truck` class. But what if later, the comany wants to add sea logistics in order to be able to be able to create ships? They would then have to implement a `Ship` class. And even later, maybe an `Airplane` class. Each of these implementations will make the company do some huge changes to its code.

As a solution, the Factory Method pattern suggests that you replace direct object construction calls (with the `new` operator) with calls to a special _factory_ method (`Transport`). Objects will still be created via the `new` operator, but it is being called from within the factory method. Objects returned by a factory method are often referred to as **products**.

The code that uses the factory method (often called the _client code_) does not see a difference between the actual products returned by various subclasses. The client treats all the products as abstract `Transport`. The client knows that all transport objects are supposed to have, for example the `deliver` method, but exactly how it works is not important to the client.

### **Applicability**

- Use the factory method when you don't know beforehand the exact types and dependencies of the objects your code should work with.
- Use the factory method when you want to provide users of your library or framework with a way to extend its internal components.
- Use the factory method when you want to save system resources by reusing existing objects instead of rebuilding them each time.

### **Implementation**

1. Make all products follow the same interface. This interface should declare methods that make sense in every product.
2. Add an empty factory method inside the creator class. The return type of the method should match the common product interface.
3. In the creator's code find all references to product constructors. One by one, replace them with calls to the factory method, while extracting the product creation code into the factory method. You might need to add a temporary parameter to the factory method to control the type of returned product. At this point, the code of the factory method may look pretty ugly. It may have a large `switch` statement that picks which product class to instantiate. But no need to worry, we will fix it soon.
4. Now, create a set of creator subclasses for each type of product listed in the factory method. Overrise the factory method in the subclasses and extract the appropriate bits of construction code from the base method.
5. If there are too many product types and it does not make sense to create subclasses for all of them, you can reuse the control paramteres from the base class in subclasses.
6. If, after all the extractions, the base factory method ahs become empty, you can make it abstract. If there is something left, you can make it a default behavior of the method.

## **Service locator**

The goal of this pattern is to improve the modularity of your application by removing the dependency between the client and the implementation of an interface.

Interfaces are one of the most flexible and powerful tools to decouple software components and to improve the maintainability of your code. This is closely related to solid design principles:

- Following the **open/closed principle**, you use one or more interfaces to ensure that your component is open for extension but closed for modification.
- The **Liskov substitution principle** requires you to implement your interfaces in a way that you can replace its implementations without changing the code that uses the interface.
- The **interface segregation principle** ensures that you design your interfaces so that clients don't depend on parts of the interface.
- Following the **dependency inversion principle**, you need to introduce an interface as an abstraction between a higher and a lower level component to split the dependency between both components.

Following all of the principles above, is necessary but is not enough. At some point, you would still have to provide an implementation of the interface. If this is done by the same class that uses the interface, you still got a dependency between the client and the implementation of the interface. The **service locator pattern** is one option to avoid this dependency.

Service locator pattern acts as a central registry that provides implementations of different interfaces. Doing so, your component that uses an interface no longer needs to know the specific class that implements the interface. Instead of instantiating that class itself, it gets an implementation from the service locator. In simple terms, the service locator holds all the separate services you need to run tasks in your application and whenever you need a service you ask the service locator and it makes it available.

# **Architectures**

## **Service-Oriented Architecture (SOA)**

It is a style of software design where services are provided to other components by application components, through a communication protocol over a network. In SOA, a number of services communicate with each other, in one of two ways:

1. Through passing data
2. Through two or more services coordinating an activity
