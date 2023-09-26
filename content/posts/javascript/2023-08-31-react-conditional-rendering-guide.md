---
title: "React Conditional Rendering: Techniques and Examples"
subtitle: Create Dynamic User Interfaces with React's Conditional Rendering
description: Learn how to dynamically change what your React app displays based on conditions. Explore techniques like `if` statements, ternary operators, `&&` logical operator, element variables, and rendering components conditionally. Examples and best practices included.
slug: react-conditional-rendering-guide
tags: [javascript]
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/javascriptwithexample/React_Js_Course_-_Conditional_Rendering_jidb3e.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/javascriptwithexample/React_Js_Course_-_Conditional_Rendering_jidb3e.png
comments: true
date: 2023-08-31
toc: true
draft: false
series: [React Js Course]
audio: https://with-code-example.s3.ap-south-1.amazonaws.com/blog/react-conditional-rendering-guide.9e3882fd-ad01-4954-9258-057993778485.mp3
canonical_url: https://courses.withcodeexample.com/course/react-js/conditional-rendering/
---

Conditional rendering is a technique in React that allows you to conditionally render different content or components based on certain conditions or states. It's a powerful way to create dynamic user interfaces that respond to user interactions or changing data. There are multiple ways to achieve conditional rendering in React:

## Conditional Rendering

### 1. Using `if` Statements in React:
You can use regular JavaScript `if` statements to conditionally render content within the `render` method of your component.

```jsx
import React, { Component } from 'react';

class ConditionalRender extends Component {
  render() {
    if (this.props.isLoggedIn) {
      return <p>Welcome, user!</p>;
    } else {
      return <p>Please log in to continue.</p>;
    }
  }
}

export default ConditionalRender;
```

### 2. Using Ternary Operator in React:
The ternary operator is a concise way to perform conditional rendering.

```jsx
import React from 'react';

const ConditionalRender = (props) => {
  return (
    <div>
      {props.isLoggedIn ? <p>Welcome, user!</p> : <p>Please log in to continue.</p>}
    </div>
  );
};

export default ConditionalRender;
```

### 3. Using Logical AND Operator (`&&`) in React:
You can use the logical AND operator (`&&`) to conditionally render content.

```jsx
import React from 'react';

const ConditionalRender = (props) => {
  return (
    <div>
      {props.isLoggedIn && <p>Welcome, user!</p>}
      {!props.isLoggedIn && <p>Please log in to continue.</p>}
    </div>
  );
};

export default ConditionalRender;
```

### 4. Using Element Variables in React:
You can conditionally assign JSX elements to variables and then use those variables within the `render` method.

```jsx
import React, { Component } from 'react';

class ConditionalRender extends Component {
  render() {
    let message;
    if (this.props.isLoggedIn) {
      message = <p>Welcome, user!</p>;
    } else {
      message = <p>Please log in to continue.</p>;
    }

    return <div>{message}</div>;
  }
}

export default ConditionalRender;
```

### 5. Conditional Rendering of Components in React:
You can also conditionally render entire components based on conditions.

```jsx
import React from 'react';
import WelcomeComponent from './WelcomeComponent';
import LoginComponent from './LoginComponent';

const ConditionalRender = (props) => {
  return (
    <div>
      {props.isLoggedIn ? <WelcomeComponent /> : <LoginComponent />}
    </div>
  );
};

export default ConditionalRender;
```

Conditional rendering is extremely versatile and allows you to create dynamic user interfaces that adjust based on various factors. You can use these techniques to display different content, components, or UI elements depending on the state of your application or user interactions.


## The `map()` function for rendering lists

The `map()` function can be used not only for rendering lists of elements but also for conditionally rendering elements based on certain conditions. You can combine the `map()` function with conditional logic to dynamically generate and render components or elements based on the data and conditions. Here's how you can use the `map()` function for conditional rendering of lists in React:

```jsx
import React from 'react';

const ItemList = (props) => {
  const items = props.items;

  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>
          {item.completed ? <s>{item.name}</s> : item.name}
        </li>
      ))}
    </ul>
  );
};

export default ItemList;
```

In this example, the `ItemList` component receives an array of `items` as a prop. Each item has a `name` and a `completed` property. The `map()` function is used to iterate over the `items` array and conditionally render an `<s>` (strikethrough) element around the item's name if the `completed` property is `true`.

Usage of the `ItemList` component might look like this:

```jsx
import React from 'react';
import ItemList from './ItemList';

const ParentComponent = () => {
  const items = [
    { name: 'Task 1', completed: true },
    { name: 'Task 2', completed: false },
    { name: 'Task 3', completed: true },
  ];

  return (
    <div>
      <h2>List of Items:</h2>
      <ItemList items={items} />
    </div>
  );
};

export default ParentComponent;
```

By using the `map()` function with conditional rendering, you can create dynamic lists where the appearance of each item is determined by the values in your data. This allows you to build user interfaces that adjust and display information based on specific conditions.

## Using `key` prop for efficient list rendering


The `key` prop is a special attribute that you provide when rendering lists of elements in React. It helps React identify individual elements efficiently and manage their state and updates effectively during rendering. The `key` prop is essential for performance and correct behavior when rendering dynamic lists.

Here's why the `key` prop is important and how to use it:

**1. Uniqueness:**
Each `key` should be unique among sibling elements in a list. React uses the `key` to keep track of which elements have changed, been added, or been removed.

**2. Reconciliation:**
When a list is updated, React uses the `key` to determine if an element has changed position, if new elements have been added, or if existing elements have been removed. This process is known as reconciliation.

**3. Performance:**
Using proper `key` values helps React optimize updates and avoids unnecessary re-renders, leading to better performance.

**4. No Business Logic:**
The `key` prop is for React's internal use and should not be used to convey business logic or data. It's not passed to the component as a prop.

Here's an example of using the `key` prop for efficient list rendering:

```jsx
import React from 'react';

const ItemList = (props) => {
  const items = props.items;

  return (
    <ul>
      {items.map((item, index) => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
};

export default ItemList;
```

In this example, the `key` prop is set to `item.id`, assuming that each item has a unique `id` property. Using a unique identifier as the `key` ensures that React can accurately track changes in the list and optimize rendering.

Usage of the `ItemList` component might look like this:

```jsx
import React from 'react';
import ItemList from './ItemList';

const ParentComponent = () => {
  const items = [
    { id: 1, name: 'Item 1' },
    { id: 2, name: 'Item 2' },
    { id: 3, name: 'Item 3' },
  ];

  return (
    <div>
      <h2>List of Items:</h2>
      <ItemList items={items} />
    </div>
  );
};

export default ParentComponent;
```

By providing a unique `key` value for each item in your list, you ensure that React can efficiently manage updates and maintain a high level of performance when rendering dynamic lists.