---
layout: ../../components/Layout.astro
title: Day 5 -  Scope in JavaScript
description: This is the fifth day of 30 Days of CLG Askmitra. Today, I am going to learn about scope in JavaScript so that I can understand Closure and Modular pattern.
date: 2022-10-06
---

# Day 5 - Scope in JavaScript

This is the fifth day of 30 Days of CLG Askmitra. Today, I am going to learn about **Scope** in JavaScript so that I can understand Closure and Modular pattern.

Scope in JavaScript refers to the current context of code, which determines the accessibility of variables to JavaScript. The two types of scope are:

-   **Local scope** are those which are declared inside of a function or block.
-   **Global scope** are those which are declared globally.

JavaScript scopes are lexically scoped, meaning that we can determine a variable's scope from where it is declared in the source code. JavaScript organizes scopes with:

-   **Functions**

    Take the following example:

    ```js
    function myFunction() {
    	var myName = "Dipshan"
    }

    console.log(myName) // ReferenceError: myName is not defined
    ```

    The `myFunction () {...}` introduces a **function scope**. We can say that `myName` is a local variable and it can only be accessed inside that function. If we try to access it outside of that function we will get a `ReferenceError`.

-   **Blocks**

    Take the following example:

    ```js
    if (true) {
    	let myName = "Dipshan"
    }

    console.log(myName) // ReferenceError: myName is not defined
    ```

    Here the if statement introduces a **block scope**. We can say that `myName` is a block scope or local variable and it can only be accessed inside that block. If we try to access it outside of that function we will again get a `ReferenceError`.

    > Only the variables decalred with `let` and `const` keyword can be block scoped.

    Take the following example:

    ```js
    if (true) {
    	var myName = "Dipshan"
    }

    console.log(myName) // "Dipshan"
    ```

    This will work because the variables declared with `var` keyword are `function scoped`. Also remember that **function** scoping** is **block scoping** but, **block scoping** is not **function scoping\*\*.

Thank you for reading. This much for today. Tomorrow, we will look at **Closures and hoisting**. Good day!
