---
layout: ../../components/Layout.astro
title: Day 6 and Day 7 - Understanding Asynchronous JavaScript
description: This is the fourth day of 30 Days of CLG Askmitra. Today, I am going to learn about Asynchronous JavaScript.
---

# Day 6 and Day 7 - Understanding Asynchronous JavaScript

This is the fourth day of 30 Days of CLG Askmitra. Today, I am going to learn about **Asynchronous JavaScript**.

## Thread & Call Stack

JavaScript is a single-threaded programming language meaning that only one thing can happen at a time. It is a **synchronous** language with **asynchronous capabilities**. Using asynchronous JavaScript (such as callbacks, promises, and async/await), you can perform long network requests without blocking the main thread.

The **call stack** is the stack of functions to be executed. It is used to manage and store all the **execution context** created during the code execution. The bottom of the call stack is always the **Global Execution Context** and then we have our functions stacked on top of it.

JavaScript has a **single call **stack\*\* because it's a single-threaded language.

> The call stack has a LIFO ( Last In, First Out ) structure which means that the last thing in is always the first thing out.

In the call stack, items can be added or removed **from the top** of the stack only.

Let's try to understand how the following code snippet is executed:

```js
const second = () => {
	console.log("Hello there!")
}

const first = () => {
	console.log("Hi there!")
	second()
	console.log("The End")
}

first()
```

![Call stack](/images/call-stack.png)

<p align="center">Src: <a href="https://blog.bitsrc.io/understanding-asynchronous-javascript-the-event-loop-74cd408419ff">Understanding Asynchronous JavaScript</a></p>

1. As the code starts working, a global execution context is created (represented by `main` ) and **pushed to** the stack. Here, we have our `first()` and `second()` functions. But we are only calling `first()` on the global scope and we are calling `second()` inside `first()`.

2. When a call to `first()` is encountered, it is **pushed to** the stack. Next, `console.log('Hi there!')` is **pushed to** the top of the stack, and when it finishes, it’s **popped off** from the stack.

3. When we call `second()` inside `first()`, `second()` is **pushed to** the top of the stack, and still, the `first()` is **not popped off** because it is still running. Next, `console.log('Hello there!')` is **pushed to** the top of the stack, when it finishes, it’s **popped off** from the stack. As `second(`)` is completed executing, it is also **popped off** the stack.

4. Then `console.log(‘The End’)` is **pushed to** the top of the stack and removed when it finishes. As `first(`)` is completed executing, it is also **popped off** the stack.

5. When the program completes its execution, the global execution context(`main()`) is **popped off** from the stack.

## Execution Context

When you run any code in JavaScript, a special environment is created to handle the transformation and execution of that code. This is called execution context. It contains the currently running code and everything that aids in its execution.

There is a **global execution context** as well as a **function execution context** for every function invoked.

There are two phases that happen when an execution context is created:

1. Memory Creation Phase

-   Creates the global object ( browser => `window`, node.js => `global`)
-   Creates the `this` object and binds it to the global object
-   Setup **memory heap** for storing variables and function references
-   Stores functions and variables in the global execution object and sets the variable to `undefined`

2. Execution Phase

-   Execute code line by line
-   Create a new execution context for each function call

## Task Queue & Event Loop

| Blocking Code                                                           | Non-Blocking Code                                            |
| ----------------------------------------------------------------------- | ------------------------------------------------------------ |
| Operations that block further execution until that operation completes. | Operations that doesn't block the call stack or main thread. |
| Have to wait until the operation has finished.                          | Don't have to wait until the operation has finished.         |

To understand how **asynchronous code** or **Non-Blocking Code** is executed we have to understand the **Event Loop** and the **Task Queue**. Remember that, the event loop, the task queue or the web APIs are not part of the JavaScript engine, it’s a part of the JavaScript runtime environment. i.e. the browser.

![Event Loop and the Task queue](/images/task-queue-event-loop.png)

<p align="center">Src: <a href="https://www.youtube.com/watch?v=28AXSTCpsyU&list=PLillGF-Rfqbars4vKNtpcWVDUpVOVTlgB&index=3">JavaScript Under The Hood [3] - Asynchronous JavaScript, Task Queue & Event Loop</a></p>

The job of the **Event loop** is to look into the **call stack** and determine if the call stack is **empty or not**. If the call stack is **empty**, it looks into the **task queue** to see if there’s any pending callback waiting to be executed.

Let's try to understand how the following code snippet is executed in an asynchronous way:

```js
console.log("Hi there !")

setTimeOut(() => {
	console.log("The end")
}, 2000)

console.log("Hello there !")
```

Output:

```
Hi !
Hello there !
The end
```

1. When the above code starts executing, the `console.log("Hi there !")` is **pushed to** the stack and **popped off** when it is finished.

2. Next, the `setTimeOut()` function is called, so it is also **pushed to** the stack and sets a timer of `2s` in the web APIs environment. After that, `the setTimeout()` function has finished and it’s **popped off** from the stack.

3. Similarly, the `console.log("Hello there !")` is **pushed to** the stack and **popped off** when it is finished.

4. Now, when the timer has finished, the web API registers `callback function` to the **task queue**. In this case, the **call stack** is already empty, so the **event loop** pushed the callback function to the stack and `console.log("The end")` is executed.

> The task queue has a FIFO ( First In, First Out ) structure which means that the first thing in is always the first thing out.

This much for today guys. Thank you for reading. Tomorrow, we will look at the **Microtask queue** and **Memory management** in JavaScript. Good day!
