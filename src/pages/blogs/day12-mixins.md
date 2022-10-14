---
layout: ../../components/Layout.astro
title: Day 12 - Mixins
description: This is my twelfth day of 30 Days of CLG Askmitra. Yesterday, I learned about prototypical inheritance. Today, I am going to learn how we can use mixins to achieve composition in JavaScript.
date: 2022-10-12
---

# Day 12 - Mixins

This is my twelfth day of 30 Days of CLG Askmitra. Yesterday, I learned about **prototypes** and **prototypical inheritance**. Today, I am going to learn how we can use **mixins** to achieve **composition** in JavaScript.

```js
const canEat = {
		eat() {
			console.log("Eating...")
		},
	},
	canSwim = {
		swim() {
			console.log("Swimming...")
		},
	},
	canWalk = {
		walk() {
			console.log("Walking...")
		},
	}

function Duck() {}

Object.assign(Duck.prototype, canEat, canWalk, canSwim)

const duck = new Duck()
duck.swim() // Swimming...
```

Here, we have separate objects, `canEat`, `canSwim` and `canWalk`. The `Object.assign` method copies the values and properties from one or more source objects to a target object. Here, it will copy all the methods that we have defined in `canEat`, `canWalk` and `canSwim` to the Duck constructor's prototype.

In this way, we can compose many object constructors like Person, Fish, etc. When we have multiple constructor, our code won't be much readable. So we can extract this logic into a function called **mixin**.

```js
function mixin(target, ...sources) {
	Object.assign(target, ...sources)
}

const canEat = {
		eat() {
			console.log("Eating...")
		},
	},
	canSwim = {
		swim() {
			console.log("Swimming...")
		},
	},
	canWalk = {
		walk() {
			console.log("Walking...")
		},
	}

function Person() {}
function Fish() {}
function Duck() {}

mixin(Person.prototype, canEat, canWalk)
mixin(Fish.prototype, canEat, canSwim)
mixin(Duck.prototype, canEat, canWalk, canSwim)

const duck = new Duck()
duck.walk() // Walking...

const dipshan = new Person()
dipshan.eat() // Eating...

const goldFish = new Fish()
goldFish.swim() // Swimming...
```

Here, we have a `mixin()` function which has two parameters, a **target** and **sources**, then we are doing the same thing. But this time, we are using **spread operator** because we don't know how many source objects are going to be passed. Then we can easily use this **mixin function** to compose _Duck_, _Person_ and _Fish_ objects.

Thank you for reading. This much for today. Tomorrow, we will look at **ES6 Classes**. Good day!
