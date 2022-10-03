---
layout: ../../components/Layout.astro
title: Day 3 - Equality in JavaScript
description: This is the third day of 30 Days of CLG Askmitra. Yesterday, I learned about type coercion and abstract operations. Today, I wil be learning about Equality in JavaScript and dig into how Double Equals works internally and also see some examples.
---

# Day 3 - Equality in JavaScript

This is the third day of 30 Days of CLG Askmitra. Yesterday, I learned about type coercion and abstract operations. Today, I wil be learning about Equality in JavaScript and dig into how Double Equals works internally and also see some examples.

## Double & triple equals

Commonly we hear and think that the **Double equals** compares the values loosely, and the **Triple equals** checks the value and type strictly.

> The double equals and the triple equals are exactly identical when the types match.

The difference between **Strict Equality Comparison** (===) and **Abstract Equality Comparision** (==) is whether or not they are going to allow any **type conversion.** Importantly, triple equals or strict equality **doesn't do any comparision or checking** at all if the types don't match, whereas double equals or loose equality will first see if the types are same, it will also do **Strict Equality Comparision** else it will do some type conversions.

## How Double Equals works internally ?

The comparision `x == y` is performed as follows:

1. If the either sides are **null** and **undefined**, it will return true.

    **Example**:

    ```js
    null == undefined //=> true
    undefined == null //=> true
    ```

2. If "x" is a number and "y" is a string, the `toNumber()` abstract operation will be performed on "y" and the result of comparision will be returned. Same will happen to "y" if it is a string and "x" is a number.

    **Example**:

    ```js
    0 == "0" //=> true
    ```

    Here, string "0" is converted to 0, and ultimately the result becomes **true.**

3. If "x" is a boolean, again `toNumber()` abstract operation will be performed on it and the result of comparision will be returned. Same will heppen to "y" if it is a boolean.

    **Example**:

    ```js
    3 > 2 > 1 //=> false
    ```

    In this comparision, first `3 > 2` is run which gives us **"true"**, so it becomes, `true > 1`. Now when we are using Relational Comparision, the `toNumber()` abstract operation is invoked which here, converts **true to 1**. Ultimately the result becomes **false** since 1 is not less than 1.

    ```js
    3 > 2 > 1
    true > 1
    1 > 1
    false
    ```

4. If "x" is either string, number, or symbol and "y" is object, the `toPrmitive()` abstract operation is invoked on "y" and the result of the comparison is returned. Same will heppen to "x" if it is an object and "y" is a string, number, or symbol.

    **Example**:

    ```js
    "0" == [] //=> false
    ```

    Since "0" is a string and `[]` is an object (yes you heard is right! Arrays are objects in JavaScript ), as mentioned above, it tries doing `toPrimitve([])` with the hint **"string"**. Now the `toPrimitive([])` will do `toString([])` as the hint is **"string"**. Now, it will return an empty string **""**.

    ```js
    "0" == []
    "0" == ""
    false
    ```

This much for today guys. Thankyou for reading. Tomorrow, we will look about **Strict Equality Comparison**. We will look more about **Abstract Equaltiy Comparision** and deal more with the weirdness of JavaScript. Good day !
