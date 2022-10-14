---
layout: ../../components/Layout.astro
title: Day 10
description: This is my tenth day of 30 Days of CLG Askmitra. Yesterday, I learned about concepts like encapsulation, abstraction, inheritance and polymorphism. Today, I am going to learn about factory functions, constructor functions, and getters and setters.
date: 2022-10-10
---

# Day 10

This is my tenth day of 30 Days of CLG Askmitra. Yesterday, I learned about concepts like encapsulation, abstraction, inheritance and polymorphism. Today, I am going to learn about factory functions, constructor functions, and getters and setters.

## Factory function

If we return an object in a function, to create new objects, we refer to that function as a **Factory function**.

**Syntax:**

```js
function createMobile(name, price, model) {
	return {
		name,
		price,
		model,
		start: function () {
			console.log("Starting...")
		},
	}
}

const mobile1 = createMobile("REDMI NOTE 10", 30000, "SOME")

console.log(mobile1) // {...}
mobile1.start() // Starting..
```

## Constructor function

If we use the `this` keyword along with the `new` operator, we refer to that function as a **constructor function**.

**Syntax:**

```js
function Mobile(name, price, model) {
	this.name = name
	this.price = price
	this.model = model
	this.start = function () {
		console.log("Starting...")
	}
}

const mobile2 = new Mobile("REALME NARZO", 26000, "BLAH")
console.log(mobile2) // {...}
mobile2.start() // Starting...
```

The `this` keyword is basically a reference to the object that is executing this piece of code. The `new` operator will create a new empty object. Then it will set `this` to point to that object. By default, `this` points to global object. Any finally it will return that object from the function.

## Constructor property

Every object in JavaScript has a property called a **constructor** and that references the function that was used to construct or create that object. For example, if we try to access the `constructor` property of "mobile2", we will get something like this:

```js
ƒ Mobile(name, price, model) {
	this.name = name
	this.price = price
	this.model = model
	this.start = function () {
		console.log("Starting...")
	}
}
```

This is the function that we used to create `mobile2`. But if we try to see the `constructor` property of "mobile1", we get:

```js
ƒ Object() { [native code] }
```

We had created "mobile1" using a **factory function** and because we used the **object literal** syntax, it was internally created using this **object constructor** function. There are many other built-in constructors in JavaScript.

## Iterating over properties in an object

We can iterate over properties in an object using `for in` loop. We can dynamically access an object's property by using bracket notation.

**Example:**

```js
for (const key in mobile1) {
	console.log(`${key}: ${mobile1[key]}`)
}
```

**Output:**

```
name: REDMI NOTE 10
price: 30000
model: SOME
start: function () {
                        console.log("Starting...")
                }
```

We can also use `Object.keys()` method to get an array of properties (keys) of that object and `Object.values()` method to get the values of that object.

**Example:**

```js
console.log(Object.keys(mobile1))
console.log(Object.values(mobile1))
```

**Output:**

```
[ 'name', 'price', 'model', 'start' ]
[ 'REDMI NOTE 10', 30000, 'SOME', [Function: start] ]
```

## Getters and setters

When we want to define a property in an object which can only be accessed but can not be modified, or a property whose value needs to be computed, in that case, we can use **getters**. Similarly, when we want to do certain validation before changing the value of a property of an object, we can use **setters**.

**Example:**

```js
function Person(name, birthYear) {
	this.name = name
	this.birthYear = birthYear

	Object.defineProperty(this, "age", {
		get: function () {
			const currentYear = new Date().getFullYear()
			return currentYear - birthYear
		},
		set: function (value) {
			if (value !== this.age) throw new Error("Age is not correct !")
		},
	})
}

const dipshan = new Person("Dipshan", 2008)

dipshan.age = 14

console.log(dipshan.age) // 14

dipshan.age = 16 // Error: Age is not correct !
```

Thank you for reading. This much for today. Tomorrow, we will look at **Prototypes** and **Prototypical inheritance**. Good day!
