---
title: 10 Handy React.js Code Snippets for Your Projects
subtitle: Boost Your React.js Development with These Code Snippets
description: Explore these 10 useful React.js code snippets to streamline your project development. Learn how to create functional components, handle state with useState hook, and more!
slug: handy-reactjs-code-snippets
tags: [javascript, reactjs, top]
featured_image: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_60_bold:Top%2010%20Handy%20React.js%20Code%20Snippets,co_rgb:fff/javascriptwithexample/bg4.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_60_bold:Top%2010%20Handy%20React.js%20Code%20Snippets,co_rgb:fff/javascriptwithexample/bg4.png
comments: true
date: 2023-10-03
toc: true
draft: false
series: ["Top In React"]
---

Here are 10 useful React.js code snippets that can come in handy for various scenarios. You can adapt and use these snippets in your React projects:

1. **Creating a Functional Component:**
```jsx
import React from 'react';

function MyComponent() {
  return <div>Hello, React!</div>;
}

export default MyComponent;
```

2. **Using Props in a Component:**
```jsx
function Greeting(props) {
  return <div>Hello, {props.name}!</div>;
}
```

3. **Handling State with useState Hook:**
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

4. **Mapping Over an Array to Render Components:**
```jsx
const items = ['Item 1', 'Item 2', 'Item 3'];

const ItemList = () => (
  <ul>
    {items.map((item, index) => (
      <li key={index}>{item}</li>
    ))}
  </ul>
);
```

5. **Conditional Rendering with Ternary Operator:**
```jsx
function Message({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? <p>Welcome back!</p> : <p>Please log in.</p>}
    </div>
  );
}
```

6. **Handling Form Input with State:**
```jsx
import React, { useState } from 'react';

function TextInput() {
  const [inputValue, setInputValue] = useState('');

  const handleChange = (e) => {
    setInputValue(e.target.value);
  };

  return (
    <input
      type="text"
      value={inputValue}
      onChange={handleChange}
      placeholder="Enter text"
    />
  );
}
```

7. **Fetching Data from an API with useEffect:**
```jsx
import React, { useEffect, useState } from 'react';

function DataFetching() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then((response) => response.json())
      .then((data) => setData(data));
  }, []);

  return <div>{/* Render data here */}</div>;
}
```

8. **Using React Router for Routing:**
```jsx
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';

function App() {
  return (
    <Router>
      <nav>
        <ul>
          <li><Link to="/">Home</Link></li>
          <li><Link to="/about">About</Link></li>
        </ul>
      </nav>
      <Route path="/" exact component={Home} />
      <Route path="/about" component={About} />
    </Router>
  );
}
```

9. **Adding CSS Classes Conditionally:**
```jsx
function Button({ isPrimary }) {
  const className = isPrimary ? 'primary-button' : 'secondary-button';

  return <button className={className}>Click me</button>;
}
```

10. **Handling Click Events:**
```jsx
function handleClick() {
  alert('Button clicked!');
}

function ClickButton() {
  return <button onClick={handleClick}>Click me</button>;
}
```

These snippets cover a range of common React.js use cases. Remember to customize them according to your specific project requirements.
