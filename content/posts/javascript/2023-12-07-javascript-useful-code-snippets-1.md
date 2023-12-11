---
title: Javascript Useful Code Snippets Part - 1
subtitle: Top useful code snippets with code example.
description: JS code snippets for String Length, String Contains, String to Number, Append to Array and Sleep.
slug: javascript-useful-code-snippets-part-1
tags: [javascript, snippets]
featured_image: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_50_bold:Javascript%20Useful%20Code%20Snippets,co_rgb:fff/javascriptwithexample/bg6.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_50_bold:Javascript%20Useful%20Code%20Snippets,co_rgb:fff/javascriptwithexample/bg6.png
comments: true
date: 2023-12-07
toc: true
draft: false
---


Certainly! Below are code snippets with explanations for the mentioned JavaScript tasks:

## 1. JavaScript String Length

```javascript
// Code snippet for getting the length of a string in JavaScript
const myString = "Hello, World!";
const lengthOfString = myString.length;

console.log(`Length of the string: ${lengthOfString}`);
```

**Explanation:**
In this code, we use the `length` property of a JavaScript string to determine the number of characters in the string. The result is stored in the variable `lengthOfString`, and it is then logged to the console.

## 2. JavaScript String Contains

```javascript
// Code snippet for checking if a string contains another string in JavaScript
const mainString = "Hello, World!";
const subString = "World";

const containsSubstring = mainString.includes(subString);

console.log(`Does the main string contain the substring? ${containsSubstring}`);
```

**Explanation:**
The `includes` method is used to check if a substring is present in the main string. It returns a boolean value (`true` if the substring is found, `false` otherwise). In this example, it checks if the `mainString` contains the `subString`.

## 3. JavaScript Convert String to Number

```javascript
// Code snippet for converting a string to a number in JavaScript
const numericString = "42";
const numericValue = Number(numericString);

console.log(`Converted numeric value: ${numericValue}`);
```

**Explanation:**
The `Number` function in JavaScript is used to convert a string to a number. In this example, the string `"42"` is converted to the numeric value `42`, and the result is logged to the console.

## 4. JavaScript Append to Array

```javascript
// Code snippet for appending an element to an array in JavaScript
const myArray = [1, 2, 3];
const newElement = 4;

myArray.push(newElement);

console.log(`Updated array: ${myArray}`);
```

**Explanation:**
The `push` method is used to add a new element to the end of an array in JavaScript. In this example, the value `4` is appended to the `myArray`, and the updated array is logged to the console.

## 5. JavaScript Sleep

```javascript
// Code snippet for creating a sleep function in JavaScript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

// Example usage
console.log("Start");
await sleep(2000); // Sleep for 2000 milliseconds (2 seconds)
console.log("End");
```

**Explanation:**
The `sleep` function is created using `setTimeout` and a Promise. It allows you to pause the execution of code for a specified duration. In this example, "Start" is logged, then the code sleeps for 2 seconds using `await sleep(2000)`, and finally, "End" is logged after the sleep period. Note that the `sleep` function should be used within an `async` context.