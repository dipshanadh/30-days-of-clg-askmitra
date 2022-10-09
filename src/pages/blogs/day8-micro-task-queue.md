---
layout: ../../components/Layout.astro
title: Day 8 - ES6 Micro-Task queue & Memory Management
description: This is the eighth day of 30 Days of CLG Askmitra. Yesterday, I learned about concepts such as call stack, event loop and task queue which together make the JavaScript runtime environment. Today, I am going to learn about **ES6 Micro-Task queue and Memory Management**.
---

# Day 8 - ES6 Micro-Task queue & Memory Management

This is the eighth day of 30 Days of CLG Askmitra. Yesterday, I learned about concepts such as call stack, event loop and task queue which together make the JavaScript runtime environment. Today, I am going to learn about **ES6 Micro-Task queue** and **Memory Management**.

## ES6 Micro-Task queue

The micro-task queue was introduced in **ES6** which is used by **promises**. Micro-Task queue has a **higher priority** than the task queue. This means the event loop doesn't move to the task queue until all tasks inside micro-task queue are not completed.

For example:

```js
console.log("Script start")

setTimeout(() => {
	console.log("setTimeout")
}, 0)

new Promise((resolve, reject) => {
	resolve("Promise resolved")
})
	.then(res => console.log(res))
	.catch(err => console.log(err))

console.log("Script End")
```

Output:

```
Script End
Promise resolved
setTimeout
```

We can see the `Promise` is executed before the `setTimeOut()` even though we provide **zero** milliseconds for the timer. It is because promises are stored in the **microtask queue**, which has **more priority** than the task queue.

## Memory Management

Unlike low-level languages like C or C++, JavaScript automatically allocates memory when objects are created and frees it when not in use anymore. This process is called **Garbage Collection**.

**JavaScript engines have two places to store data:**

-   **Stack**

    It is a data structure used to store the primitive types (String | Number | Boolean | Null | Undefined | Symbol | BigInt). These types of data are static. i.e. their size is known by the engine during the compile time. References to objects and functions are also included.

-   **Heap**

    It is used to store objects, arrays or functions in JavaScript. The engine doesn't allocate a fixed amount of memory for the **heap**. Instead, it allocates more space as required. Data stored in the heap are accessed by reference.

Thank you for reading. This much for today. From tomorrow, we will look at **Object Oriented Programming**. Good day!
