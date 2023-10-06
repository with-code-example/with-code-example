---
title: A Guide to JavaScript Promises
subtitle: Understanding Asynchronous Programming
description: Learn the fundamentals of JavaScript Promises, including states, creation, resolution, and rejection.
slug: javascript-promises-beginners-guide
tags: [javascript]
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/javascriptwithexample/promis_in_javascript_ltywru.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/javascriptwithexample/promis_in_javascript_ltywru.png
comments: true
date: 2023-09-23
toc: true
draft: false
---

Have you learned about promises in JavaScript? It’s a subject that a lot of people give up on right away, but I’ll try to make it as simple as possible for you.

## 1. What the HECK is a "Promise"?

A "Promise" is a fundamental concept in asynchronous programming, particularly in JavaScript and many modern programming languages. It represents a value (or the eventual result of an operation) that may not be available yet but will be resolved at some point in the future, either successfully with a value or unsuccessfully with an error.

## 2. States of a Promise:

In JavaScript, a Promise can be in one of three states:

1. **Pending:** This is the initial state when a Promise is created. It indicates that the asynchronous operation represented by the Promise has not yet completed, and the result (fulfilled or rejected) is not available. Promises start in this state and then transition to one of the other states.

2. **Fulfilled (Resolved):** This state represents the successful completion of the asynchronous operation. When a Promise transitions to the fulfilled state, it means that the operation has finished successfully, and the result (a value or data) is available. You can access the resolved value using the `.then()` method.

3. **Rejected:** This state represents the failure of the asynchronous operation. When a Promise transitions to the rejected state, it means that an error or exception occurred during the operation. You can access the reason for rejection (an error object or message) and handle it using the `.catch()` method or the second argument of the `.then()` method.

Here's a visual representation of the states and transitions of a Promise:

```
Initial State:      Pending
                   /       \
Fulfilled State:  Fulfilled  Rejected
(result available) (error occurred)
```

Promises are designed to provide a structured way to work with asynchronous operations, allowing you to handle success and failure cases separately. You can use `.then()` to specify what to do when the Promise is fulfilled and `.catch()` to handle errors when the Promise is rejected. This makes asynchronous code more manageable and easier to read compared to callback-based approaches.

## 3. How to build a promise
To build a Promise in JavaScript, you can use the `Promise` constructor, which takes a single function as an argument. This function is called the executor function, and it has two parameters: `resolve` and `reject`. The `resolve` function is used to fulfill the Promise with a value, and the `reject` function is used to reject the Promise with an error.

Here's the basic structure of creating a Promise:

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous or time-consuming operation goes here
  // Typically, you would perform some async task, like fetching data or reading a file

  // If the operation is successful, call resolve with the result
  // resolve(result);

  // If an error occurs, call reject with an error object or message
  // reject(error);
});
```

Here's a more concrete example that simulates a delayed asynchronous operation using `setTimeout` and resolves the Promise after a certain time:

```javascript
const delay = (milliseconds) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(`Resolved after ${milliseconds} milliseconds`);
    }, milliseconds);
  });
};

// Usage:
delay(2000) // Wait for 2 seconds
  .then((result) => {
    console.log(result); // Resolved after 2000 milliseconds
  })
  .catch((error) => {
    console.error(error);
  });
```

In this example:

1. We define a function `delay` that returns a Promise. Inside the Promise constructor, we use `setTimeout` to simulate an asynchronous delay.

2. If the asynchronous operation is successful (i.e., the `setTimeout` completes), we call `resolve` with the result.

3. If an error occurs during the operation, we can call `reject` with an error object or message.

4. We use `.then()` to specify what to do when the Promise is fulfilled (resolved), and we use `.catch()` to handle any errors that might occur.

This is a simple example, but in practice, you would replace the `setTimeout` with real asynchronous operations like making an API request or reading a file. Promises provide a structured way to handle asynchronous code and make it more readable and maintainable.

### 3.1. Returning values when the promise is resolved

In JavaScript Promises, you can return values when the Promise is resolved by providing the resolved value as an argument to the `resolve` function within the Promise's executor function. Here's how you can do it:

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Simulate a successful asynchronous operation
  setTimeout(() => {
    const result = 'This is the resolved value';
    resolve(result); // Resolve the Promise with the result
  }, 2000);
});

// Use the Promise to access the resolved value
myPromise
  .then((result) => {
    console.log('Resolved:', result); // Resolved: This is the resolved value
  })
  .catch((error) => {
    console.error('Error:', error);
  });
```

In this example:

1. Inside the Promise's executor function, we simulate an asynchronous operation using `setTimeout`.

2. When the asynchronous operation completes successfully, we call `resolve(result)` with the desired resolved value (`'This is the resolved value'` in this case).

3. When you use `.then()` to handle the Promise's resolution, the resolved value is passed as an argument to the callback function. You can access and use the resolved value within that callback.

The `result` variable contains the resolved value, and you can use it as needed in the `.then()` callback.

This pattern allows you to work with the result of an asynchronous operation in a structured and clean way. The resolved value can be of any data type, including strings, numbers, objects, or even other Promises.

### 3.2. Returning an error when the promise is rejected

In JavaScript Promises, you can return an error when the Promise is rejected by providing an error message or an error object as an argument to the `reject` function within the Promise's executor function. Here's how you can do it:

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Simulate a failed asynchronous operation
  setTimeout(() => {
    const errorMessage = 'This is the error message';
    reject(errorMessage); // Reject the Promise with the error message
  }, 2000);
});

// Use the Promise to handle the rejection and error
myPromise
  .then((result) => {
    console.log('Resolved:', result);
  })
  .catch((error) => {
    console.error('Error:', error); // Error: This is the error message
  });
```

In this example:

1. Inside the Promise's executor function, we simulate a failed asynchronous operation using `setTimeout`.

2. When the asynchronous operation encounters an error, we call `reject(errorMessage)` with the desired error message (`'This is the error message'` in this case).

3. When you use `.catch()` to handle the Promise's rejection, the rejected error is passed as an argument to the callback function. You can access and use the error message or error object within that callback.

The `error` variable contains the rejected error, and you can handle and log it or perform any other error-handling tasks as needed.

This pattern allows you to gracefully handle errors that may occur during asynchronous operations using Promises. The rejected value can be an error message string, an error object, or any other value that represents the reason for the rejection.
