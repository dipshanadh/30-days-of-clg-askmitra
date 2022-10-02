---
layout: ../../components/Layout.astro
title: Day 2 - Coercion and Abstract operations
description: This is the second day of 30 Days of CLG Askmitra. Yesterday, I had talked about types and a little bit about coercion. Today, I am going to dive into type coercion and abstract operations.
---

# Day 2 - Coercion and Abstract Operations

This is the second day of 30 Days of CLG Askmitra. Yesterday, I had talked about **types** and a little bit about **coercion**. Today, I am going to dive into **type coercion** and **abstract operations**.

## Type coercion

JavaScript implicitly performs **automatic type conversions** when needed. This automatic or implicit conversion of values of one data type to another (such as numbers to strings or strings to numbers) is called **type coercion.**

> Type coercion and type conversoin are not same. Type coercion is implicit or automatic whereas type conversion maybe implicit or explicit.

**Example:**

```js
const v1 = "11"
const v2 = 1
const sum = v1 + v2
console.log(sum) // "111"
```

Here, JavaScript has **_coerced_** `1` to a string and performed **_concatenation_**, resuting in a string of `111`.

## Abstract operations

Have you ever wondered how coercion works internally ? **Abstract operations** are the fundamental building blocks that makes up how we deal with **type coercion**. These operations are not a part of JavaScript, but are defined to aid the specification of the semantics of the language. The abstract operations perform the tasks of **_type conversion_.** They are conceptual operations.

## Some abstract operations

Here we will look into four abstract operations, **toPrimitive**, **toString**, **toNumber** and **toBoolean**.

-   **ToPrimitive**

    The abstract operation `toPrimitive()` converts a non-primitive (like function, object and array) to a primitve. It takes to arguement **_input_** and an optional arguement **_preferred type_** (string or number). Another thing to keep in mind is that `toPrimitve()` is a **recursive** operations, which means that if the result from `toPrimitive` is not a primitive, it is going to be evoked again until it can get a primitve, or in some cases gets an error.

    The way it works is that there are two methods that are available on any non-primitive, the `valueOf()` and `toString()`. If the hint given is **"number"**, it will first try to invoke `valueOf()`. And if we get a **primitive type** from the result then we are done. If it doesn't get a primitive, then it will again try doing `toString()`. Now if we don't get a primitive even after trying both of those, generally thats gonna end up resulting an **error.** If the hint was string, the order is just reversed.

    > When `toPrimitive` is called without a hint, then it generally behaves as if the hint was number.

-   **ToString**

    The abstract operation `toString()` takes any value and gives us the representation of that value in **string form**. It converts argument to a value of type String according to [Table 15](https://tc39.es/ecma262/#table-tostring-conversions).

    | Value                               | Result            |
    | ----------------------------------- | ----------------- |
    | undefined                           | "undefined"       |
    | null                                | "null"            |
    | true                                | "true"            |
    | false                               | "false"           |
    | 10                                  | "10"              |
    | `{name: "Dipshan"}`                 | "[object Object]" |
    | `{toString() { return "Dipshan" }}` | "Dipshan"         |
    | `[]`                                | ""                |
    | `[1, 2, 3]`                         | "1,2,3"           |

    \*\*You can also specify your own `toString` method to override the default return value.\*\*

-   **ToNumber**

    The abstract operation `toNumber()` takes a **non-numeric** and converts it to a value of type Number according to [Table 13](https://tc39.es/ecma262/#table-tonumber-conversions).

    | Value     | Result |
    | --------- | ------ |
    | undefined | NaN    |
    | null      | 0      |
    | true      | 1      |
    | false     | 0      |
    | "5"       | 5      |

    When we use `toNumber()` on **_object_** or an **_array_**, it invokes the `toPrimitive()` with the number hint and the resulting value

-   **ToBoolean**

    Anytime you have a value that is not a **Boolean**, but is used in a place that needs a **Boolean**, this operation occures. It converts a value to **false** if it is `""` (empty string), 0, -0 (negative zero), null, `NaN`, false and undefined. In other cases, it will just return **true.**

This much for today guys. Thankyou for reading. We will look more about coercions (cases of coercions) and also see about boxing tomorrow. Good day !
