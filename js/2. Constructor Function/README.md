<!--
 * @Author: Adam Li adam@bizzone.com
 * @Date: 2024-12-12 22:43:32
 * @LastEditors: Adam Li
 * @LastEditTime: 2024-12-13 12:41:25
 * @FilePath: /interview/js/2. Constructor Function/README.md
-->
# Constructor Functions in JavaScript

In JavaScript, a **constructor function** is a special type of function used to create and initialize objects. They act as blueprints for creating multiple instances with the same properties and methods.


## What is Object
（1）对象是单个实物的抽象。

一本书、一辆汽车、一个人都可以是对象，一个数据库、一张网页、一个与远程服务器的连接也可以是对象。当实物被抽象成对象，实物之间的关系就变成了对象之间的关系，从而就可以模拟现实情况，针对对象进行编程。

（2）对象是一个容器，封装了属性（property）和方法（method）。

属性是对象的状态，方法是对象的行为（完成某种任务）。比如，我们可以把动物抽象为animal对象，使用“属性”记录具体是那一种动物，使用“方法”表示动物的某种行为（奔跑、捕猎、休息等等）。

## Syntax of a Constructor Function

A constructor function typically:

- Starts with an uppercase letter (by convention).
- Is called using the `new` keyword.
- Uses `this` to assign properties and methods.

### Basic Example
```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;

    this.greet = function() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
    };
}

// Creating instances
const person1 = new Person('Alice', 25);
const person2 = new Person('Bob', 30);

person1.greet(); // Output: Hello, my name is Alice and I am 25 years old.
person2.greet(); // Output: Hello, my name is Bob and I am 30 years old.
```
### Important Points to Note

1. **Uppercase Naming**: The function name `Person` starts with an uppercase letter to distinguish it from regular functions.
2. **`new` Keyword**: When calling `new Person()`, a new object is created, and `this` refers to that new object.
3. **Methods**: Methods defined inside the constructor will be duplicated for each instance.

## How the `new` Keyword Works

When you use the `new` keyword, the following steps happen under the hood:

1. A new empty object `{}` is created.
2. The constructor function is called with `this` bound to the new object.
3. The new object is linked to the constructor’s prototype.
4. The new object is returned.


构造函数内部，this指的是一个新生成的空对象，所有针对this的操作，都会发生在这个空对象上。

### Example Illustration
```javascript
const car = new Object(); // Similar to: const car = {};
```
## Adding Methods to the Prototype

To avoid duplicating methods for each instance, you can add methods to the prototype of the constructor.
```javascript
    function Dog(breed) {
      this.breed = breed;
    }

    // Adding a method to the prototype
    Dog.prototype.bark = function() {
      console.log(`Woof! I am a ${this.breed}.`);
    };

    const dog1 = new Dog('Golden Retriever');
    const dog2 = new Dog('Beagle');

    dog1.bark(); // Output: Woof! I am a Golden Retriever.
    dog2.bark(); // Output: Woof! I am a Beagle.
```
### Why Use Prototypes?

- **Efficiency**: Methods defined on the prototype are shared across all instances, saving memory.
- **Inheritance**: Prototypes allow you to implement inheritance in JavaScript.

## Constructor Function vs Class Syntax

ES6 introduced the `class` syntax, which is syntactic sugar over constructor functions.

### Example Using `class`
```javascript
    class Person {
      constructor(name, age) {
        this.name = name;
        this.age = age;
      }

      greet() {
        console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
      }
    }

    const person = new Person('Charlie', 35);
    person.greet(); // Output: Hello, my name is Charlie and I am 35 years old.
```
## Summary

- **Constructor functions** are an older way to create objects in JavaScript.
- Always use the `new` keyword when invoking a constructor function.
- Methods can be added to the **prototype** to improve memory efficiency.
- The **class syntax** offers a modern alternative to constructor functions.
