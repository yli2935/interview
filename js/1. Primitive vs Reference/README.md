<!--
 * @Author: Adam Li adam@bizzone.com
 * @Date: 2024-12-09 22:55:29
 * @LastEditors: Adam Li
 * @LastEditTime: 2024-12-10 21:14:44
 * @FilePath: /interview/js/Primitive vs Reference/README.md
-->
# Understanding Data Types in JavaScript

As programmers, we use data types every day, and understanding how the computer handles these data types is essential. In JavaScript, data types are divided into two categories: **primitive data types** and **reference data types**. The computer treats each of these categories differently, and knowing the difference helps you avoid errors and write efficient code.

---

## 📌 **Primitive Data Types**

Primitive data types are the simplest types in JavaScript. They are **not objects** and **do not have methods**. Examples of primitive data types are:

- **Numbers**
- **Strings**
- **Booleans**
- **Null**
- **Undefined**

### Strings and Methods

Even though strings have methods, they are still primitive data types. JavaScript temporarily converts primitive strings to string objects to allow the use of string methods.

### How Primitive Data Types are Stored

When you declare a primitive data type, it is stored in the **stack**. The stack is a data structure that stores and retrieves data quickly.

Example:

```javascript
let numOne = 50;
let numTwo = numOne; // numTwo = 50
numOne = 100;

console.log(numOne); // Outputs 100
console.log(numTwo); // Outputs 50
```

### Explanation:

1. `numOne` and `numTwo` are stored separately on the stack.
2. Changing `numOne` does not affect `numTwo` since they occupy different memory locations.

---

## 📌 **Reference Data Types**

Reference data types are dynamic and do not have a fixed size. They are considered **objects** and can have methods. Examples include:

- **Arrays**
- **Functions**
- **Objects**

### How Reference Data Types are Stored

When you create a reference data type, the value itself is stored on the **heap**, while a **pointer** to that value is stored on the **stack**.

**Example:**
```javascript
let object1 = { name: 'Bingeh', age: 18 };
let object2 = object1;

object1.age = 20;

console.log(object2);
→ Outputs { name: 'Bingeh', age: 20 }
```
### Explanation:

1. `object1` stores a pointer on the stack, pointing to the actual object on the heap.
2. `object2` gets the same pointer, so it references the same object.
3. Updating `object1` affects `object2` since both point to the same memory location.

---

## 🔍 **Key Differences**

| **Feature**                    | **Primitive Data Types**                    | **Reference Data Types**                       |
| -------------------------------| -------------------------------------------- | ---------------------------------------------- |
| **Storage Location**           | Stack                                       | Heap (object) + Stack (pointer)               |
| **Size**                       | Fixed                                        | Dynamic                                        |
| **Example Types**              | `number`, `string`, `boolean`, `null`      | `array`, `function`, `object`                 |
| **Copy Behavior**              | Creates a separate copy                     | Copies the pointer to the same object         |
| **Mutability**                 | Immutable                                    | Mutable                                        |

---

## 📝 **Why It Matters**

- Understanding these differences helps you avoid unexpected behavior, like modifying one variable and unintentionally changing another.
- Debugging issues like **'null pointer reference'** becomes easier when you know how data is stored and accessed.

---
## 📝 **Interview Questions**

### 1. **How to determine if a variable is an array or an object (without using `typeof`)?**

In JavaScript, you can determine whether a value is an array using the built-in method `Array.isArray()`.

## Syntax

`Array.isArray(value);`

- **Returns:** `true` if the value is an array, otherwise `false`.

## Example Usage
```javascript
const arr = [1, 2, 3];
console.log(Array.isArray(arr)); // true

const notArr = { key: 'value' };
console.log(Array.isArray(notArr)); // false
```
## Why Use `Array.isArray()`?

1. **Reliable**: Works consistently across different JavaScript environments.  
2. **Safe**: Correctly identifies arrays even if they originate from different contexts (e.g., `iframe`).

## Alternative Method (Not Recommended)

You can also use the `instanceof` operator:

`console.log(arr instanceof Array); // true`

### Drawbacks of `instanceof`

- Fails when arrays are created in different execution contexts (e.g., different `iframe` contexts).

Therefore, **`Array.isArray()`** is the preferred method.

## Summary

- **Preferred Method**: `Array.isArray(value)`  
- **Avoid**: `value instanceof Array` due to potential context issues.
---

### 2. **Is `null` an object?**

- **Explanation:**  
  In JavaScript, `null` is **not** an object. However, the `typeof` operator returns `"object"` for `null` due to a historical bug in the language. This behavior remains for backward compatibility.  

  Example: `typeof null;` returns `"object"`  

---

### 3. **Why is `0.3 + 0.1` not equal to `0.4`?**

- **Explanation:**  
  Computers store numbers in binary. Some decimal fractions (like `0.1` or `0.3`) cannot be represented precisely in binary. Because of this, `0.1` and `0.3` are stored as approximations, and when added together, the result is not exactly `0.4`.  

  Example: `0.3 + 0.1` outputs `0.4000000000000001`
