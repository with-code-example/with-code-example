---
title: useEffect React Hook Explained With Example
subtitle: Manage Side Effects in React Functional Components with the useEffect Hook
description: Discover the useEffect hook in React – the essential tool for handling side effects in functional components. Simplify your code and enhance performance.
tags: [reactjs, react-hooks]
slug: useeffect-react-hook-with-examples
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/awesome-blog/awesome-javascript/React_Hooks_useEffect_icmtv1.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/awesome-blog/awesome-javascript/React_Hooks_useEffect_icmtv1.png
comments: true
date: 2023-08-16
toc: true
draft: false
series: ['React Hooks']
---

The `useEffect` hook is another essential React Hook that allows you to perform side effects in functional components. Side effects include tasks such as data fetching, DOM manipulation, and subscribing to external data sources. The `useEffect` hook ensures that these side effects occur after the component has rendered and the DOM is updated, preventing potential performance issues and inconsistencies. Let's delve into how the `useEffect` hook works and explore some examples.

## Syntax:
```jsx
useEffect(() => {
  // Side effect code here
  return () => {
    // Cleanup code (optional) - runs when the component unmounts or before the next effect
  };
}, [dependencies]);
```

- The function inside `useEffect` is the side effect you want to perform.
- The optional return function can be used for cleanup (e.g., canceling subscriptions, removing event listeners) before the component unmounts or before the next effect runs.
- The `dependencies` array is an array of values that, when changed, will trigger the effect to run again.

## Fetching Data:

```jsx
import React, { useState, useEffect } from 'react';

const DataFetching = () => {
  const [data, setData] = useState([]);

  useEffect(() => {
    // Fetch data from an API
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => setData(data));
  }, []); // Empty dependency array runs effect once (on mount)

  return (
    <div>
      {data.map(item => (
        <p key={item.id}>{item.name}</p>
      ))}
    </div>
  );
};
```

In this example, the `useEffect` hook is used to fetch data from an API and update the component's state (`data`). The empty dependency array ensures that the effect runs only once, similar to `componentDidMount`.

## Document Title Update:

```jsx
import React, { useState, useEffect } from 'react';

const DynamicTitle = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};
```

In this example, the `useEffect` hook updates the document title whenever the `count` state changes.

## Cleanup and Unsubscription:

```jsx
import React, { useState, useEffect } from 'react';

const SubscriptionExample = () => {
  const [message, setMessage] = useState('');

  useEffect(() => {
    const subscription = subscribeToService((data) => {
      setMessage(data);
    });

    return () => {
      // Cleanup: unsubscribe when the component unmounts
      unsubscribeFromService(subscription);
    };
  }, []);

  return <div>{message}</div>;
};
```

In this example, the `useEffect` hook subscribes to a service and updates the component with incoming data. The cleanup function unsubscribes from the service when the component unmounts.

The `useEffect` hook is a powerful tool for managing side effects in your React components. It helps you keep your component logic organized and ensures that side effects are executed in a controlled manner, preventing potential bugs and performance issues.