---
layout: ../../components/Layout.astro
title: Day 9 - Object Oriented Programming in JavaScript
description: This is the ninth day of 30 Days of CLG Askmitra. From today, I am going to learn about Object Oriented Programming in JavaScript.
date: 2022-10-09
---

# Day 9 - Object Oriented Programming in JavaScript

This is the ninth day of 30 Days of CLG Askmitra. From today, I am going to learn about **Object Oriented Programming**.

OOP is a programming paradigm based on the concept of **objects**, rather than functions. An object can contain variables in the form of **properties** and functions in the form of **methods**. In Object Oriented Programming, we combine a group of different variables and functions into an object.

## Four pillars of OOP

There are four main pillars of OOP.

-   **Encapsulation**

    In OOP, we group related variables and functions that operate on them, into an object. This is what we call encapsulation. In this way, we can reduce complexity.

-   **Abstraction**

    Abstraction is the process of hiding the complexity and internal details from the outside and showing only the essential ones. The main purpose of abstraction is to hide unnecessary details from the users.

-   **Inheritance**

    Inheritance is the mechanism that allows you to eliminate redundant code. It is an approach of sharing common functionality among multiple objects. It increases code reusability.

-   **Polymorphism**

    **"Poly"** means many and **"morphism"** means the ability to take on multiple forms. Thus, polymorphism means the ability of an object to take on multiple forms. It denotes an object’s/reference’ ability to adopt several forms and do different things in various instances.

## Objects

Object in JavaScript is a collection of **property-value pairs**. The simplest way of creating an object in JavaScript is by using the **object literal** syntax.

```js
const mobilePhone = {
	name: "HUAWERI Y-5 PRIME",
	price: 15000,
	company: "HUAWEI",
	model: "DRA-LX2",
	start: function () {
		console.log("Starting...")
	},
}
```

In the curly braces, we can add property-value pairs separated by a **comma (,)**. A property is separated from its value by a **colon (:)**. The function inside of an object is called a **method**.

We can access a property by using the dot **notation**.

```js
mobilePhone.start() // "Starting..."
```

We can also define an object by using **factories** and **constructors**. I will look into that tomorrow. Good day!
