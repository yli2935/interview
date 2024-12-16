<!--
 * @Author: Adam Li adam@bizzone.com
 * @Date: 2024-12-12 22:22:55
 * @LastEditors: Adam Li
 * @LastEditTime: 2024-12-12 22:36:34
 * @FilePath: /interview/js/protptype and prototype chain/README.md
-->
# JavaScript: Prototype and Prototype Chain

## Introduction

JavaScript is a prototype-based language. Understanding prototypes and the prototype chain is essential for mastering object-oriented programming in JavaScript.

---

## What is a Prototype?

Every JavaScript **object** has a hidden property called `[[Prototype]]`, which references another object known as its **prototype**. This prototype allows JavaScript objects to inherit properties and methods from other objects.

### Accessing the Prototype

In modern JavaScript, you can access an object's prototype using:

- `Object.getPrototypeOf(obj)`
- The `__proto__` property (non-standard, but widely supported)

### Example:

```javascript
const person = {
  greet: function () {
    console.log('Hello!');
  }
};

const user = Object.create(person); // user inherits from person

user.greet(); // Output: Hello!
console.log(Object.getPrototypeOf(user) === person); // true
```
## Constructor Functions and Prototypes

When you create objects using a **constructor function**, the prototype of those objects is set to the `prototype` property of the constructor function.

### Example:
```javascript
function User(name) {  
  this.name = name;  
}  
// constructor have prototype
User.prototype.sayHello = function () {  
  console.log(`Hello, my name is ${this.name}`);  
};  

const user1 = new User('Alice');  
user1.sayHello(); // Output: Hello, my name is Alice  

// object have __proto__, and it is the same as prototype in it constructor function
console.log(user1.__proto__ === User.prototype); // true  
```
In this example:

- `User` is a constructor function.  
- `User.prototype` contains the `sayHello` method.  
- `user1` inherits `sayHello` from `User.prototype`.  

---

## The Prototype Chain

The **prototype chain** is a series of links between objects. If a property or method is not found on an object, JavaScript looks up the prototype chain to find it.

### Prototype Chain Lookup Example:
```javascript
function Animal(name) {  
  this.name = name;  
}  

Animal.prototype.speak = function () {  
  console.log(`${this.name} makes a sound.`);  
};  

const dog = new Animal('Dog');  

dog.speak(); // Output: Dog makes a sound.  

// Check the prototype chain  
console.log(dog.__proto__ === Animal.prototype); // true  
console.log(Animal.prototype.__proto__ === Object.prototype); // true  
console.log(Object.prototype.__proto__ === null); // true  
```

### Prototype Chain Diagram:
```javascript
dog --> Animal.prototype --> Object.prototype --> null
```
If `dog.speak()` is called:

1. JavaScript looks for `speak` on `dog`.  
2. If not found, it checks `Animal.prototype`.  
3. If still not found, it checks `Object.prototype`.  
4. The search ends when it reaches `null`.  

---

### Object.prototype
The base prototype that all objects ultimately inherit from.
It provides a set of fundamental methods that are inherited by all objects, such as:
- **hasOwnProperty():** Checks if an object has a specific property as its own property.
  ```javascript
    const person = {
      firstName: "Alice",
      lastName: "Bob"
    };

    // 检查person对象是否有"firstName"属性
    console.log(person.hasOwnProperty("firstName")); // 输出：true

    // 检查person对象是否有"toString"属性（从Object.prototype继承而来）
    console.log(person.hasOwnProperty("toString")); // 输出：false
  ```
- **toString():** Returns a string representation of an object.
- **valueOf():** Returns the primitive value of an object

## Important Points

1. **Prototype Inheritance**: Objects inherit properties and methods via their prototypes.  
2. **`__proto__`**: Links an object to its prototype (though `__proto__` is not recommended for production use).  
3. **`Object.prototype`**: The base prototype that all objects ultimately inherit from.  
4. **Constructor's `prototype`**: Used to define methods/properties that will be inherited by instances created with that constructor.  

---

## Summary

- **Prototype** is a mechanism for inheritance in JavaScript.  
- The **prototype chain** allows JavaScript to search up the chain for methods or properties.  
- Use **constructor functions** and their `prototype` to define shared behavior.  
- The prototype chain ends with `Object.prototype`, which has its own methods like `toString`.  

Understanding prototypes and the prototype chain is crucial for writing efficient and organized JavaScript code.  

---

## Further Reading

- [MDN Web Docs: Prototype](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)  
- [MDN Web Docs: Inheritance and the Prototype Chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)  