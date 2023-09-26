---
title: Exploring the useContext Hook in React
subtitle: Share Data and Functions Across React Components using useContext
description: Discover how the useContext hook revolutionizes React component communication. Easily share data and functions without prop drilling, enhancing code clarity and performance.
tags: [reactjs, react-hooks]
slug: unlocking-component-communication-usecontext-react
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/awesome-blog/awesome-javascript/React_Hooks_useContext_izbhvl.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/awesome-blog/awesome-javascript/React_Hooks_useContext_izbhvl.png
comments: true
date: 2023-08-17
toc: true
draft: false
series: ['React Hooks']
---

The `useContext` hook in React allows you to access the context of a parent component within a child component, without the need for prop drilling. This is particularly useful for sharing data or state between components that are not directly related in the component tree. Let's explore a couple of examples of how to use the `useContext` hook.

## Theme Context

Suppose you want to create a themed user interface where components can access the theme colors defined at a higher level. Here's how you can achieve that using `useContext`:

### 1. Create a Context:
```jsx
import React, { createContext } from 'react';

const ThemeContext = createContext();

export default ThemeContext;
```

### 2. Provide the Context in a Parent Component:
```jsx
import React from 'react';
import ThemeContext from './ThemeContext';

const App = () => {
  const theme = {
    background: 'lightblue',
    foreground: 'darkblue'
  };

  return (
    <ThemeContext.Provider value={theme}>
      {/* Your component hierarchy */}
    </ThemeContext.Provider>
  );
};
```

### 3. Use the Context in Child Components:
```jsx
import React, { useContext } from 'react';
import ThemeContext from './ThemeContext';

const ThemedButton = () => {
  const theme = useContext(ThemeContext);

  return (
    <button style={{ backgroundColor: theme.background, color: theme.foreground }}>
      Themed Button
    </button>
  );
};
```

## User Authentication Context

Imagine you're building an authentication system, and you want to share the user's authentication status and related functions across various components. Here's how you can achieve this using `useContext`:

### 1. Create a Context:
```jsx
import React, { createContext, useContext, useState } from 'react';

const AuthContext = createContext();

const AuthProvider = ({ children }) => {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  const login = () => {
    setIsLoggedIn(true);
  };

  const logout = () => {
    setIsLoggedIn(false);
  };

  return (
    <AuthContext.Provider value={{ isLoggedIn, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

export { AuthContext, AuthProvider };
```

### 2. Provide the Context in a Parent Component:
```jsx
import React from 'react';
import { AuthProvider } from './AuthContext';

const App = () => {
  return (
    <AuthProvider>
      {/* Your component hierarchy */}
    </AuthProvider>
  );
};
```

### 3. Use the Context in Child Components:
```jsx
import React, { useContext } from 'react';
import { AuthContext } from './AuthContext';

const Profile = () => {
  const { isLoggedIn, login, logout } = useContext(AuthContext);

  return (
    <div>
      {isLoggedIn ? (
        <div>
          <p>Welcome, User!</p>
          <button onClick={logout}>Logout</button>
        </div>
      ) : (
        <button onClick={login}>Login</button>
      )}
    </div>
  );
};
```

These examples demonstrate how you can use the `useContext` hook to share data and functions across components efficiently, without passing props through every level of the component tree. This helps in keeping your codebase clean and maintainable.