# **Architectures**

## **Singleton**

The singlton design pattern is usually implemented to take care of 2 problems:

1. **To ensure that a class can have only one instance:** why would we want this? The most common reason is to control access to some shared resource - for instance, a database or some files. Imagine you created an instance of a class, but after a while you decided to create a new one. This will return to you the object that you have already created, instead of creating a fresh object.

2. **Provise a global access point to that single instance:** lets you access some object from anywhere in the program, just like a global variable. However, it also protects that object from being overwritten by other code.

### **Implementation**

All implementations of the Singleton pattern involves 2 steps:

1. Make the default constructor _private_, to prevent other objects from using the `new` operator with the Singlton class.
2. Create a `static` creation method that acts as a constructor. Under the hood, this method will call the private `constructor` to create an object and saves it in a static field. Now all following calls to this static creation method will return the cached object.

> If your code has access to the Singleton class, it would be able to call the Singleton's static creation method. Whenever the method is called, the same object is always returned.
