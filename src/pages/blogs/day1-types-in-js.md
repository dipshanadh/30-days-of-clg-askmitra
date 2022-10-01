---
layout: ../../components/Layout.astro
title: Day 1 - Types in JavaScript
description: This is the first day of 30 Days of CLG Askmitra. Today, I am going to dive into JavaScript types.
---

# Types in JavaScript

This is the first day of 30 Days of CLG Askmitra. Today, I am going to dive into **JavaScript types**, the **typeof** operator and **BigInt**.

## Dynamic and weak typing

JavaScript is a **dynamically typed** language, which means that variables in JavaScript are not directly associated with any particular value type, and any variable can be assigned value of other type.

> In JavaScript, variables don't have types, values do.

JavaScript is also a **weakly typed** language meaning that a value of one type can be `coerced` into another type when an operatoin involves mismatched types.

Take a look at this meme !

![JavaScript type coercion meme](/images/coercion-meme.png)

So whats happening here is, while doing `"11" + 1`, 1 is **coerced** to a string, so that it can be concatenated with "11". Similarly while doing `"11" - 1`, "11" is **coerced** to a number, so that 1 can be subtracted from it.

---

## Primary types

In JavaScript, a **primitive** is a data that is not an **object**. There are seven primitive data types:

-   Undefined
-   String
-   Number
-   Boolean
-   Symbol
-   BigInt
-   Null

> In JavaScript everything is an object

This is a **wrong** misconception. The primitives are not objects ! And they don't have any methods too, but still behaves as if they do. When properties are accessed on primitives, JavaScript **_auto-boxes_** the value into a **wrapper object** and accesses the property on that object instead. Autoboxing is the idea of implicitly turning primitive into object when we are to access certain methods that primitives **“appear”** to have.

For example: When we do `let num = 1` and we try to access `num.valueOf()`, the `num` gets autoboxed into a `Number` object and then it calls `Number.prototype.valueOf()` on that object. Likewise, when we call a method on a **"string"** primitive, the same thing happens. It gets autoboxed into a `String` object, which is attached with a lot of useful prototypical methods such as substring and concat.

### Sub types

-   Object
-   Function
-   Array

**Object**: Object is a collection of properties. All JavaScript values, except primitives, are objects. Objects are written as `key: value` pairs. A **method** is an object property containing a function definiton.

**Function**: Function in JavaScript is an object with additional capability of being _callable_. Functions are reusable bits of code, which can be used again and again.

**Array**: An array is a special variable, which can hold more than one similar values:

```js
const cars = ["Saab", "Volvo", "BMW"]
```

Arrays are also objects, with `index`, which is used to access the particular array element, and `length` property which represents the size of an array. The `index` starts from zero and ends to a number one less than the `length`

---

### The typeof operator

The `typeof` operator tells us what is the type of value stored in that variable.

```js
typeof v // 'undefined'

let v
typeof v // "undefined"
// this is a historical bug

v = "1"
typeof v // 'string'

v = 2
typeof v // 'number'

v = {}
typeof v // "object

v = Symbol()
typeof v // "symbol
```

Guess what ? The output given by the `typeof` operator is always `string`

Now, let's look at some weirdness of JavaScript

```js
let v = null
typeof v // "object" OOPS ?

v = () => {}
typeof v // "function" hmm ?

v = [1, 2, 3]
typeof v // "object" relly ?
```

The [specification](https://262.ecma-international.org/5.1/#sec-11.4.3) defines different behaviour for `typeof` when it interacts with different types of variables.

---

### BigInt

The **BigInt** value is a `bigInt` primitive created by appending `n` to an end of an integer literal, or by calling the `BigInt` function without the `new` operator. It is used to represent and manipulate the numerical values which are too large to be represented by the `number` primitive.

```js
typeof 1n === "bigint" // true
typeof BigInt(1) === "bigint" // true
```

**Thing to remember:**

> A BigInt value cannot be used with methods in the built-in `Math` object and cannot be mixed with a Number value in operations; they must be `coerced` to the same type. The precision of a BigInt value may be lost when it is `coerced` to a Number value.

This much for today guys. We will look into equalities, abstract operations and more about coercions & boxing tomorrow.
