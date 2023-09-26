---
title: "Understanding React.js Components: Functional, Class, State, Props, and Hooks"
subtitle: Exploring the Key Types of React Components and Core Concepts
description: Discover the fundamental building blocks of React.js applications – components. Dive into functional and class components, learn how state and props facilitate data flow, and explore the power of lifecycle methods and modern hooks.
slug: understanding-react-js-components-functional-class-state-props-and-hooks
tags: [javascript, reactjs]
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/awesome-blog/awesome-javascript/Understanding_React.js_Components__Functional_Class_State_Props_and_Hooks_x12rck.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/awesome-blog/awesome-javascript/Understanding_React.js_Components__Functional_Class_State_Props_and_Hooks_x12rck.png
comments: true
date: 2023-08-13
toc: true
draft: false
---

React.js is a popular JavaScript library for building user interfaces, and it revolves around the concept of components. Components are the building blocks of a React application, allowing you to create modular, reusable, and encapsulated pieces of user interface. Each component represents a self-contained unit that can have its own state, props (properties), and lifecycle methods. Let's explore some other key types of React components:

## 1. Functional Components:
Functional components are the simplest type of React component. They are defined as JavaScript functions that return JSX (JavaScript XML) to describe the UI. Functional components are stateless by default, meaning they don't manage their own state. They receive data through props and are mainly used for rendering UI elements.

### Example of a functional component:

```jsx
import React from 'react';

const FunctionalComponent = (props) => {
  return <div>{props.text}</div>;
};

export default FunctionalComponent;
```

## 2. Class Components:
Class components are the older way of defining React components. They are JavaScript classes that extend the `React.Component` class. Class components can have their own state and lifecycle methods, making them suitable for more complex interactions and logic.

### Example of a class component:

```jsx
import React, { Component } from 'react';

class ClassComponent extends Component {
  render() {
    return <div>{this.props.text}</div>;
  }
}

export default ClassComponent;
```

## 3. State and Props:
Props (short for properties) are used to pass data from parent to child components. Props are read-only and help components communicate with each other. State, on the other hand, is used to manage a component's internal data and can change over time, triggering re-renders.

### Example using props:

```jsx
import React from 'react';

const Greeting = (props) => {
  return <div>Hello, {props.name}!</div>;
};
```

### Example using state:

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Increment
        </button>
      </div>
    );
  }
}
```

## 4. Lifecycle Methods:
Class components have a lifecycle that consists of various phases such as mounting, updating, and unmounting. These phases are controlled by lifecycle methods, which allow you to perform actions at specific times during a component's lifecycle.

### Example of a lifecycle method (`componentDidMount`) in a class component:

```jsx
import React, { Component } from 'react';

class MyComponent extends Component {
  componentDidMount() {
    // This code runs after the component is mounted (added to the DOM).
    console.log('Component mounted');
  }

  render() {
    return <div>My Component</div>;
  }
}
```

## 5. Hooks (Functional Component Enhancements):
Hooks were introduced in React 16.8 as a way to use state and other React features in functional components without using class components. Hooks like `useState`, `useEffect`, and `useContext` enable you to manage state and side effects directly within functional components.

### Example using the `useState` hook:

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};
```

These are just a few of the core concepts and types of React components. React offers a rich ecosystem of components and libraries that cater to different use cases and scenarios. By mastering these concepts, you'll be well-equipped to build sophisticated and efficient user interfaces using React.js.