---
layout: ../../components/Layout.astro
title: Day 11 - Prototypes and Prototypical Inheritance
description: This is my eleventh day of 30 Days of CLG Askmitra. Yesterday, I learned about factory functions, constructor functions, and getters and setters. Today, I am going to learn about prototypes and prototypical inheritance.
date: 2022-10-11
---

# Day 11 - Prototypes and Prototypical Inheritance

This is my eleventh day of 30 Days of CLG Askmitra. Yesterday, I learned about factory functions, constructor functions, and getters and setters. Today, I am going to learn about prototypes and prototypical inheritance.

## Prototypes

Every JavaScript object has a built-in property called **prototype**. The prototype object is a special type of enumerable object to which additional properties can be attached to it which will be shared across all the instances of its constructor function. When we try to access a property from an object and its missing, JavaScript will automatically take it from its prototype.

Example:

```js
function Person(name, birthYear) {
	this.name = name
	this.birthYear = birthYear
}

Person.prototype.getAge = function () {
	const currentYear = new Date().getFullYear()
	return currentYear - this.birthYear
}

const person = new Person("Dipshan", 2008)
console.log(person.getAge()) // 14
```

## Prototypical Inheritance

For instance, we have a `person` object with its properties and methods, and we want to make `student` as slightly different variants of it. We'd like to reuse what we have in `person`, without reimplementing it, just build a new object on top of it. In such cases, **_Prototypical inheritance_** helps.

```js
function extend(Child, Parent) {
	Child.prototype = Object.create(Parent.prototype)
	Child.prototype.constructor = Child
}

function Person(name, birthYear) {
	this.name = name
	this.birthYear = birthYear
}

Person.prototype.getAge = function () {
	const currentYear = new Date().getFullYear()
	return currentYear - this.birthYear
}

function Student(name, birthYear, grade) {
	Person.call(this, name, birthYear)
	this.grade = grade
}

extend(Student, Person)

const dipshan = new Student("Dipshan", 2008, 9)
console.log(dipshan)
console.log(dipshan.getAge())
```

In the above code, inside `Student` constructor:

1. I have `Person.call(this, name, birthYear)`, which will call the `Person` constructor and sets `this` to point to the new instance of `Student` object. This is how you call the super constructor.

2. Similarly, I have also made `extend` function which extends the given child constructor to a parent constructor. The way it works is it first creates an object with the prototype of the parent constructor and then sets the child's prototype to that object. Here, I am using it to extend `Student` to `Person`.

3. I am also reassigning the constructor because step 2 will set the constructor of the instance of `Student` object to `Person` constructor.

Creating many levels of inheritance hierarchies makes the code complex. They are very fragile. With composition, instead of having a complex hierarchy, we can compose a few objects together to create a new object. In JavaScript, we can use **mixins** to achieve composition. and thats what I am going to see tomorrow.
