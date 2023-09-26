---
title: "Components and Props in React"
subtitle: "Exploring Functional vs. Class Components, Destructuring Props, and Customization Techniques"
description: "Delve into React's core concepts! Understand the differences between functional and class components, master destructuring props, and learn how to customize components using props. Build versatile and dynamic UIs with React."
slug: "components-props-react-deep-dive"
tags: [javascript, reactjs]
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/javascriptwithexample/React_Js_Course_-_Components_and_Props_q0svxd.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/javascriptwithexample/React_Js_Course_-_Components_and_Props_q0svxd.png
comments: true
date: 2023-08-28
toc: true
draft: false
series: [React Js Course]
audio: https://res.cloudinary.com/harendra21/video/upload/v1693477885/javascriptwithexample/components-props-react-deep-dive_mlsfvy.wav
canonical_url: https://courses.withcodeexample.com/course/react-js/components-and-props/
---

Functional components and class components are two different ways to define and work with components in React, a popular JavaScript library for building user interfaces. While both approaches achieve the same goal of creating reusable UI elements, there are some differences in how they are structured and used.

## Functional Components vs. Class Components:

**1. Functional Components:**
Functional components, also known as "functional" or "stateless" components, are defined as JavaScript functions. They take in props as their arguments and return JSX (JavaScript XML) to describe what should be rendered. Functional components have become the preferred way of writing components in React due to their simplicity and the introduction of React Hooks.

**Advantages:**
- **Simplicity:** They are simpler and easier to read and write compared to class components.
- **Performance:** They can be more optimized by React's internal mechanisms because they don't involve the overhead of managing instances.
- **Hooks:** Functional components can use React Hooks to manage state and lifecycle behavior without needing to switch to class components.

**Disadvantages:**
- **Limited Lifecycle Methods:** Prior to the introduction of Hooks, functional components had limited access to lifecycle methods.
- **Harder to Manage Shared Logic:** In certain cases, it could be slightly harder to manage shared stateful logic between components.

**Example:**

```jsx
import React from 'react';

const FunctionalComponent = (props) => {
  return <div>{props.message}</div>;
};

export default FunctionalComponent;
```

**2. Class Components:**
Class components are defined as JavaScript classes that extend `React.Component`. They have more features and capabilities compared to functional components, including access to the full set of React lifecycle methods.

**Advantages:**
- **Full Lifecycle Methods:** Class components have access to the complete set of lifecycle methods, which can be useful in some scenarios.
- **Legacy Codebases:** If you're working with an older React codebase, you might encounter class components more frequently.

**Disadvantages:**
- **Complexity:** Class components can be more verbose and harder to read, especially for simpler UI elements.
- **Performance Overhead:** They involve a bit more overhead compared to functional components, although this difference might not be significant in most applications.
- **More Boilerplate:** Class components require more boilerplate code.

**Example:**

```jsx
import React, { Component } from 'react';

class ClassComponent extends Component {
  render() {
    return <div>{this.props.message}</div>;
  }
}

export default ClassComponent;
```
## Passing data through props

Passing data through props (short for properties) is a fundamental concept in React that allows you to pass information from a parent component to a child component. Props are read-only and provide a way to communicate and share data between components in a predictable manner. Here's how you can pass data through props in React:

**1. Parent Component:**
In the parent component, you define the child component and pass the desired data as attributes (props).

```jsx
import React from 'react';
import ChildComponent from './ChildComponent'; // Import the child component

const ParentComponent = () => {
  const message = "Hello from parent!";
  const numberValue = 42;

  return (
    <div>
      <ChildComponent message={message} numberValue={numberValue} />
    </div>
  );
};

export default ParentComponent;
```

**2. Child Component:**
In the child component, you can access the passed data through the `props` object. Props are accessible as properties of the `props` object.

```jsx
import React from 'react';

const ChildComponent = (props) => {
  return (
    <div>
      <p>Message from parent: {props.message}</p>
      <p>Number value from parent: {props.numberValue}</p>
    </div>
  );
};

export default ChildComponent;
```

In this example, the `ParentComponent` passes `message` and `numberValue` as props to the `ChildComponent`. The child component then displays these props in its output.

**3. Destructuring Props:**
Instead of accessing props using `props.message` and `props.numberValue`, you can destructure the props directly within the child component's function parameters:

```jsx
import React from 'react';

const ChildComponent = ({ message, numberValue }) => {
  return (
    <div>
      <p>Message from parent: {message}</p>
      <p>Number value from parent: {numberValue}</p>
    </div>
  );
};

export default ChildComponent;
```

Destructuring props in this way can make your code cleaner and more readable.

**4. Default Props:**
You can also provide default values for props in case they are not passed from the parent component. This is useful to ensure that your component still functions correctly even if certain props are missing.

```jsx
import React from 'react';

const ChildComponent = ({ message = 'Default Message', numberValue = 0 }) => {
  return (
    <div>
      <p>Message from parent: {message}</p>
      <p>Number value from parent: {numberValue}</p>
    </div>
  );
};

export default ChildComponent;
```

Passing data through props allows you to create reusable and modular components that can be easily composed to build complex user interfaces.






## Destructuring Props
Destructuring props is a technique in React that allows you to extract specific properties from the `props` object directly in the function parameters of your component. This makes your code cleaner and more concise by avoiding the need to access props with the `props` object. Here's how you can use destructuring to work with props in a React component:

**1. Basic Destructuring:**
Suppose you have a component that receives a `name` and an `age` as props. You can destructure these props in the function parameters like this:

```jsx
import React from 'react';

const PersonInfo = ({ name, age }) => {
  return (
    <div>
      <p>Name: {name}</p>
      <p>Age: {age}</p>
    </div>
  );
};

export default PersonInfo;
```

**2. Default Values:**
You can provide default values for props using destructuring as well. If a prop is not passed, the default value will be used instead:

```jsx
import React from 'react';

const PersonInfo = ({ name = 'Unknown', age = 0 }) => {
  return (
    <div>
      <p>Name: {name}</p>
      <p>Age: {age}</p>
    </div>
  );
};

export default PersonInfo;
```

**3. Nested Destructuring:**
If your props contain nested objects, you can also destructure nested properties:

```jsx
import React from 'react';

const UserProfile = ({ user }) => {
  const { name, age, email } = user;

  return (
    <div>
      <p>Name: {name}</p>
      <p>Age: {age}</p>
      <p>Email: {email}</p>
    </div>
  );
};

export default UserProfile;
```

**4. Renaming Props:**
You can rename props using destructuring. This can be useful when the prop name you want to use in your component conflicts with a reserved keyword or another variable name:

```jsx
import React from 'react';

const Movie = ({ title: movieTitle, releaseYear }) => {
  return (
    <div>
      <p>Title: {movieTitle}</p>
      <p>Release Year: {releaseYear}</p>
    </div>
  );
};

export default Movie;
```

In this example, the prop `title` is renamed to `movieTitle` within the component.

Using destructuring props in your components can lead to more readable and organized code, especially when dealing with multiple props. It's a widely adopted pattern in the React community.


## Using props to customize components


Using props to customize components is a fundamental concept in React that allows you to make your components flexible and reusable. Props provide a way to pass data and configuration to components so that they can be customized and adapted for various use cases. Here's how you can use props to customize your components:

**1. Passing Basic Props:**
You can pass basic data types, such as strings, numbers, and booleans, as props to customize your components.

```jsx
import React from 'react';

const CustomizedComponent = (props) => {
  return <div>{props.text}</div>;
};

export default CustomizedComponent;
```

**2. Using Props in Parent Component:**
In the parent component, you can use the `CustomizedComponent` and provide the necessary props.

```jsx
import React from 'react';
import CustomizedComponent from './CustomizedComponent';

const ParentComponent = () => {
  return <CustomizedComponent text="Hello, World!" />;
};

export default ParentComponent;
```

**3. Customizing Component Behavior:**
Props can be used to customize not only the content but also the behavior of your components.

```jsx
import React from 'react';

const Button = (props) => {
  return (
    <button onClick={props.onClick}>
      {props.label}
    </button>
  );
};

export default Button;
```

**4. Using Props in Parent Component for Behavior Customization:**
In the parent component, you can pass a function as a prop to customize the behavior of the `Button` component.

```jsx
import React from 'react';
import Button from './Button';

const ParentComponent = () => {
  const handleClick = () => {
    alert('Button clicked!');
  };

  return <Button label="Click Me" onClick={handleClick} />;
};

export default ParentComponent;
```

**5. Conditional Rendering with Props:**
You can use props to conditionally render different parts of your component based on the data you receive.

```jsx
import React from 'react';

const ConditionalComponent = (props) => {
  return (
    <div>
      {props.showContent ? <p>{props.content}</p> : <p>No content to display.</p>}
    </div>
  );
};

export default ConditionalComponent;
```

**6. Using Props in Parent Component for Conditional Rendering:**
In the parent component, you can control the conditional rendering by passing a boolean prop.

```jsx
import React from 'react';
import ConditionalComponent from './ConditionalComponent';

const ParentComponent = () => {
  return <ConditionalComponent showContent={true} content="This is some content." />;
};

export default ParentComponent;
```

Props provide a powerful way to make your components adaptable and reusable across different parts of your application. By passing data and behaviors via props, you can create components that can be easily configured to meet a wide range of requirements.