---
layout: ../../components/Layout.astro
title: Day 4 -  Double Equals Corner Cases and Abstract Equality Comparison
description: This is the fourth day of 30 Days of CLG Askmitra. Yesterday, I dug into how Double Equals works and also saw some examples. Today, I will look at more weird examples of Double Equals and see how triple equal works.
---

# Day 4 - Double Equals Corner Cases and Abstract Equality Comparison

This is the fourth day of 30 Days of CLG Askmitra. Yesterday, I dug into how Double Equals works and also saw some examples. Today, I will look at more weird examples of Double Equals and see how triple equal works.

## How Triple Equals works ?

The comparison `x === y` is performed as follows:

1. If the types of **x** and **y** aren't same it will simply return **false.**

    Example:

    ```js
    "21" === 21 //=> false
    ```

2. If **x** is a number:

    a. If either **x** or **y** is `NaN`, return **false**.

    Example:

    ```js
    NaN === NaN //=> false
    ```

    > `NaN` is never equal to anything, not even itself.

    b. If **x** is the same number value as **y**, return **true**.

    c. If one side is `+0` and the other is `-0``, return **true**.

    Example:

    ```js
    0 === -0 //=> true
    ```

    d. If none of the above conditions match, return **false**.

3. If they are not numbers, check if **x** and **y** are exactly the same, and if they are, return **true**.

## Double Equals Corner Cases

![JavaScript meme](/images/coercion-meme-2.png)

I found this meme on my Facebook feed a couple of months ago, and I also thought why JavaScript is so weird ?
But now, after properly understanding **coercion** and **abstract operations**, I don't think JavaScript is that much weird.

Today, I am going to explain to you what's going on here.

-   `0 == "0"` returns **true**

    1. When a **string** is compared with a **number** using **Double Equals**, the `toNumber()` abstract operation will be invoked passing that **string** as the argument.

    2. Here, string "0" is converted to 0, so it becomes `0 == 0` and ultimately the result becomes **true.**

-   `0 == []` also returns **true**

    1. . If an **object** is compared with an **string** using **Double Equals**, the `toPrmitive()` abstract operation is invoked with that **object** input and the result of the comparison is returned.

    2. Since “0” is a string and `[]` is an object (yes you heard is right! Arrays are objects in JavaScript ), as mentioned above, it tries doing `toPrimitve([])` with the hint “string”.

    3. Now the `toPrimitive([])` will do `toString([])` since the hint is “string”. Now, it will return an empty string `""`.

    4. So for `0 == ""`, again `toNumber()` abstract operation will be invoked and it will become `0 == 0` which is **true**.

-   `"0" == []` returns **false**

    1. Since “0” is a string and `[]` is an object, again it tries doing `toPrimitve([])` with the hint “string”.

    2. Now the `toPrimitive([])` will do `toString([])` since the hint is “string”. Now, it will return an empty string `""`.

    3. So it becomes `"0" == ""`. Since the types are now the same, JavaScript will not do further **type conversion**. And the two strings are not the same, so this will become **false**.

I hope it helped. Thank you for reading. Tomorrow, we will look at **Boxing** in JavaScript. Good day!
