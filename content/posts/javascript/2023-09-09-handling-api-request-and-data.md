---
title: "Handling API Requests and Data in React"
subtitle: "A Guide to Efficient Data Handling"
description: "Learn how to fetch and display data in React apps using `fetch`, `axios`, and `async/await`. Includes tips for loading and error handling."
slug: handling-api-request-and-data
tags: [javascript, reactjs]
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/javascriptwithexample/Handling_API_Requests_w1vzjg.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/javascriptwithexample/Handling_API_Requests_w1vzjg.png
comments: true
date: 2023-09-09
toc: true
draft: false
series: [React Js Course]
canonical_url: https://courses.withcodeexample.com/course/react-js/handling-api/
---

Handling API requests and data in a React application involves making asynchronous calls to APIs, fetching data, and updating the component's state accordingly. Here's a general outline of how you can handle API requests and data in a React application:

## Making API requests in React

You can use the `fetch` API, `axios`, or other HTTP client libraries to make API requests. For the sake of this example, let's use the `fetch` API.

```jsx
import React, { useState, useEffect } from 'react';

const App = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => {
        setData(data);
        setLoading(false);
      })
      .catch(error => {
        setError(error);
        setLoading(false);
      });
  }, []);

  if (loading) {
    return <p>Loading...</p>;
  }

  if (error) {
    return <p>Error: {error.message}</p>;
  }

  return (
    <div>
      {data.map(item => (
        <div key={item.id}>{item.name}</div>
      ))}
    </div>
  );
};

export default App;
```
In this example, the `useEffect` hook is used to make an API request when the component mounts. The `useState` hooks manage the loading state, fetched data, and error state.


## Using `fetch` or third-party libraries


When it comes to making API requests in a React application, you have the choice between using the built-in `fetch` API or third-party libraries like `axios`. Both approaches have their advantages and drawbacks, and the choice depends on your specific use case and project requirements. Let's compare the two:

**Using `fetch` API:**

**Advantages:**

1. **Built-in:** The `fetch` API is built into modern browsers, so you don't need to install any additional dependencies.

2. **Minimal Setup:** Since it's a native browser feature, you don't need to add extra dependencies to your project.

3. **Promises:** The `fetch` API uses Promises, making it compatible with modern JavaScript's asynchronous patterns.

**Drawbacks:**

1. **Low-Level:** The `fetch` API is relatively low-level and lacks some features that might be helpful, such as automatic JSON parsing.

2. **No Request Cancellation:** `fetch` doesn't provide built-in support for canceling requests, which can be important for user experience.

3. **Handling Errors:** While error handling is possible with `fetch`, it can be verbose and less intuitive than some third-party libraries.

**Using Third-Party Libraries (e.g., `axios`):**

**Advantages:**

1. **Feature-Rich:** Third-party libraries like `axios` provide features like automatic JSON parsing, request/response interceptors, and request cancellation.

2. **Request Cancellation:** Libraries like `axios` offer built-in support for canceling requests, which is useful for managing user interactions.

3. **Concise Error Handling:** `axios` makes error handling more concise and standardized.

**Drawbacks:**

1. **Extra Dependency:** Adding a third-party library increases your project's dependencies and bundle size.

2. **Learning Curve:** You'll need to learn the specific syntax and features of the chosen library.

**Which to Choose:**

- If you want a lightweight solution, don't require extensive features, and prefer using native browser APIs, `fetch` is a good choice.

- If you need more advanced features like automatic JSON parsing, request cancellation, and interceptors, and you're comfortable adding an extra dependency, consider using a third-party library like `axios`.

**Example of Using `axios`:**

```jsx
import React, { useState, useEffect } from 'react';
import axios from 'axios';

const App = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    axios.get('https://api.example.com/data')
      .then(response => {
        setData(response.data);
        setLoading(false);
      })
      .catch(error => {
        setError(error);
        setLoading(false);
      });
  }, []);

  if (loading) {
    return <p>Loading...</p>;
  }

  if (error) {
    return <p>Error: {error.message}</p>;
  }

  return (
    <div>
      {data.map(item => (
        <div key={item.id}>{item.name}</div>
      ))}
    </div>
  );
};

export default App;
```

In summary, both `fetch` and third-party libraries like `axios` have their merits. If you're looking for a quick and minimal solution, `fetch` is a solid choice. If you need more features and a streamlined development experience, consider using a third-party library like `axios`.

## Handling asynchronous operations with `async/await`

`async/await` is a powerful feature in modern JavaScript that allows you to work with asynchronous operations in a more synchronous-like manner. It's especially useful when dealing with tasks like making network requests, reading/writing files, or handling any operation that might take time to complete without blocking the main thread. Here's a basic overview of how to use `async/await` in JavaScript:

1. **Async Function Declaration:**

   To use `async/await`, you need to define an `async` function. An `async` function always returns a promise implicitly, and you can use the `await` keyword inside it to pause the execution of the function until a promise is resolved.

   ```javascript
   async function fetchData() {
     // Asynchronous code goes here
   }
   ```

2. **`await` Keyword:**

   Inside an `async` function, you can use the `await` keyword before a promise to pause the execution of the function until the promise is resolved. This allows you to write asynchronous code that looks similar to synchronous code.

   ```javascript
   async function fetchData() {
     const response = await fetch('https://api.example.com/data');
     const data = await response.json();
     return data;
   }
   ```

   In this example, `fetchData` fetches data from an API, but the use of `await` makes it seem like a linear, synchronous operation.

3. **Error Handling:**

   You can use try-catch blocks to handle errors when working with `async/await`. If a promise rejects, the `await` expression will throw an exception that you can catch.

   ```javascript
   async function fetchData() {
     try {
       const response = await fetch('https://api.example.com/data');
       if (!response.ok) {
         throw new Error('Failed to fetch data');
       }
       const data = await response.json();
       return data;
     } catch (error) {
       console.error('Error:', error);
     }
   }
   ```

4. **Consuming the Async Function:**

   When you call an `async` function, it returns a promise. You can use `.then()` and `.catch()` to handle the result of the promise, or you can use `await` if you're calling it from another `async` function.

   ```javascript
   async function main() {
     try {
       const result = await fetchData();
       console.log('Data:', result);
     } catch (error) {
       console.error('Main Error:', error);
     }
   }

   main(); // Call the async function
   ```

5. **Parallel Execution:**

   `async/await` also allows you to execute asynchronous operations in parallel using `Promise.all()` or similar constructs.

   ```javascript
   async function fetchMultipleData() {
     const promise1 = fetch('https://api.example.com/data1');
     const promise2 = fetch('https://api.example.com/data2');
     const [data1, data2] = await Promise.all([promise1, promise2].map(async (p) => await p.json()));
     return { data1, data2 };
   }
   ```

6. **Async Iteration:**

   You can use `for...of` loops with asynchronous iterators to process items in an asynchronous sequence.

   ```javascript
   async function processItemsAsync(items) {
     for (const item of items) {
       await processItem(item);
     }
   }
   ```

`async/await` greatly simplifies working with asynchronous code in JavaScript and makes it more readable and maintainable compared to traditional callback-based or promise-chaining approaches. It's a fundamental feature for modern web development and is also available in Node.js for server-side applications.

## Displaying data from API responses

To display data from API responses in a React application, you can follow these steps:

** Fetch Data**

   ```javascript
   import React, { useState, useEffect } from 'react';
   import axios from 'axios';

   function App() {
     const [data, setData] = useState([]);

     useEffect(() => {
       // Fetch data from the API
       axios.get('https://api.example.com/data')
         .then((response) => {
           setData(response.data);
         })
         .catch((error) => {
           console.error('Error fetching data:', error);
         });
     }, []);

     return (
       <div>
         <h1>Data from API:</h1>
         <ul>
           {data.map((item) => (
             <li key={item.id}>{item.name}</li>
           ))}
         </ul>
       </div>
     );
   }

   export default App;
   ```

   This code uses React's `useState` and `useEffect` hooks to fetch data when the component mounts and update the component's state with the fetched data.

**Render Data:**

   In the example above, we use the `data` state variable to map over the API response and render it in the component. You can customize the rendering based on your API response structure and design needs.
 **Handling Loading and Errors:**

   It's a good practice to handle loading and error states while fetching data from an API. You can use additional state variables to manage these states and conditionally render content based on them.

   ```javascript
   import React, { useState, useEffect } from 'react';
   import axios from 'axios';

   function App() {
     const [data, setData] = useState([]);
     const [loading, setLoading] = useState(true);
     const [error, setError] = useState(null);

     useEffect(() => {
       // Fetch data from the API
       axios.get('https://api.example.com/data')
         .then((response) => {
           setData(response.data);
           setLoading(false);
         })
         .catch((error) => {
           setError(error);
           setLoading(false);
         });
     }, []);

     if (loading) {
       return <p>Loading...</p>;
     }

     if (error) {
       return <p>Error: {error.message}</p>;
     }

     return (
       <div>
         <h1>Data from API:</h1>
         <ul>
           {data.map((item) => (
             <li key={item.id}>{item.name}</li>
           ))}
         </ul>
       </div>
     );
   }

   export default App;
   ```

   This code adds loading and error states to the component, which provides a better user experience when dealing with asynchronous data.

That's it! You now have a React component that fetches data from an API and displays it in your application. You can customize this structure based on your specific API and UI requirements.