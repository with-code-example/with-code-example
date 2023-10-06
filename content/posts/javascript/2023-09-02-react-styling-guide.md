---
title: "React Styling: Inline, Classes, Modules, Frameworks, and CSS-in-JS"
subtitle: Explore Styling Options in React for Beautiful User Interfaces
description: "Learn the ins and outs of styling in React with diverse techniques: inline styles, CSS classes, CSS modules, third-party CSS frameworks, and CSS-in-JS libraries. Discover how to conditionally style based on state and master the art of creating visually appealing React applications."
slug: react-styling-guide
tags: [javascript, reactjs]
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/javascriptwithexample/React_Js_Course_-_Styling_vjca9w.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/javascriptwithexample/React_Js_Course_-_Styling_vjca9w.png
comments: true
date: 2023-09-02
toc: true
draft: false
---

In React, there are several options for styling your components and user interfaces. Here are three common approaches: inline styles, CSS classes, and CSS modules.

## Styling in CSS

**1. Inline Styles:**
With inline styles, you can apply styles directly to individual JSX elements using JavaScript objects. Inline styles are defined as objects, where keys represent style properties in camelCase and values are the corresponding property values.

```jsx
import React from 'react';

const InlineStylesExample = () => {
  const textStyle = {
    color: 'blue',
    fontSize: '16px',
    fontWeight: 'bold',
  };

  return <p style={textStyle}>Styled Text</p>;
};

export default InlineStylesExample;
```

**2. CSS Classes:**
Using CSS classes is a common way to style React components. You define styles in a separate CSS file and apply those styles to your components using className attributes.

```jsx
// styles.css
.text {
  color: blue;
  font-size: 16px;
  font-weight: bold;
}

// React component
import React from 'react';
import './styles.css';

const CSSClassesExample = () => {
  return <p className="text">Styled Text</p>;
};

export default CSSClassesExample;
```

**3. CSS Modules:**
CSS Modules is an approach that allows you to scope CSS styles to specific components. It's particularly useful when you want to avoid style conflicts between different components.

```jsx
// styles.module.css
.text {
  color: blue;
  font-size: 16px;
  font-weight: bold;
}

// React component
import React from 'react';
import styles from './styles.module.css';

const CSSModulesExample = () => {
  return <p className={styles.text}>Styled Text</p>;
};

export default CSSModulesExample;
```

Each approach has its own advantages and use cases:

- **Inline Styles:** Inline styles are useful for applying dynamic styles based on component state or props. They are scoped to individual elements and can't be easily reused.
  
- **CSS Classes:** Using CSS classes is a traditional way to style components. It allows you to separate your styling from your component logic and reuse styles across different components.
  
- **CSS Modules:** CSS Modules combine the benefits of both inline styles and CSS classes. They provide scoped styles specific to each component, ensuring style isolation and preventing unintended side effects.

Choose the styling approach that best fits your project's needs, complexity, and style organization preferences.

## Third party CSS Framework

Using third-party CSS frameworks in your React application can help streamline the styling process and provide pre-designed components that you can easily integrate into your project. These frameworks offer a set of standardized styles and UI components that save you time and effort when building the user interface.

Here's how you can incorporate third-party CSS frameworks into your React application:

**1. Install the Framework:**
Start by installing the desired CSS framework using a package manager like npm or yarn. For example, to install Bootstrap:

```bash
npm install bootstrap
```

**2. Import Styles:**
Import the CSS styles of the framework into your project. This is typically done in your main entry file, such as `index.js` or `App.js`.

```jsx
import 'bootstrap/dist/css/bootstrap.min.css';
```

**3. Use Framework Components:**
You can now use the components and styles provided by the framework within your React components.

```jsx
import React from 'react';
import { Button, Card } from 'react-bootstrap';

const FrameworkExample = () => {
  return (
    <Card>
      <Card.Body>
        <Card.Title>React Bootstrap Card</Card.Title>
        <Card.Text>This is an example card from React Bootstrap.</Card.Text>
        <Button variant="primary">Learn More</Button>
      </Card.Body>
    </Card>
  );
};

export default FrameworkExample;
```

**4. Customize and Extend:**
Many frameworks provide customization options to match your project's design. You can override styles, extend components, and adapt the framework to your needs.

**5. Be Mindful of Styles:**
Using a third-party CSS framework can bring a lot of convenience, but it's essential to consider the impact on your application's overall styles. Sometimes, frameworks might introduce CSS conflicts or unwanted styles. It's a good practice to test and customize styles as needed.

Commonly used third-party CSS frameworks for React include:

- **Bootstrap:** A widely used framework that offers responsive designs and a variety of components.
- **Material-UI:** Implements Google's Material Design principles and provides a rich set of components.
- **Ant Design:** A design system with a collection of high-quality React components.
- **Semantic UI:** Focuses on human-friendly HTML and offers a range of theming options.
- **Bulma:** A modern CSS framework based on Flexbox and used for building responsive layouts.

Remember that while third-party CSS frameworks can save time, they might also introduce some overhead and additional styles that you don't need. Evaluate the framework's fit for your project's requirements and consider the trade-offs before adopting it.


## CSS-in-JS libraries for dynamic styling

CSS-in-JS libraries allow you to write and manage your styles using JavaScript in your React components. This approach offers benefits like scoped styles, dynamic styling based on props or state, and easy integration with component logic. Here are some popular CSS-in-JS libraries that you can use for dynamic styling in your React applications:

1. **Styled Components:**
   Styled Components is one of the most widely used CSS-in-JS libraries. It allows you to define styles using tagged template literals. Styles are automatically scoped to the component they're defined in and can be dynamic based on props.

   Example usage:
   ```jsx
   import styled from 'styled-components';

   const Button = styled.button`
     background-color: ${(props) => props.primary ? 'blue' : 'gray'};
     color: white;
     padding: 10px 20px;
     border: none;
   `;

   const App = () => {
     return (
       <div>
         <Button>Normal Button</Button>
         <Button primary>Primary Button</Button>
       </div>
     );
   };
   ```

2. **Emotion:**
   Emotion is another popular CSS-in-JS library that offers powerful styling capabilities. It provides a similar syntax to Styled Components and supports theming, server-side rendering, and global styles.

   Example usage:
   ```jsx
   import { css } from '@emotion/react';

   const buttonStyles = css`
     background-color: blue;
     color: white;
     padding: 10px 20px;
     border: none;
   `;

   const App = () => {
     return (
       <div>
         <button css={buttonStyles}>Normal Button</button>
       </div>
     );
   };
   ```

3. **@mui/styles (formerly makeStyles in Material-UI):**
   If you're using Material-UI, you can use the `@mui/styles` package to create styles that are tightly integrated with Material-UI's components and theming system.

   Example usage:
   ```jsx
   import { makeStyles } from '@mui/styles';

   const useStyles = makeStyles({
     button: {
       backgroundColor: 'blue',
       color: 'white',
       padding: '10px 20px',
       border: 'none',
     },
   });

   const App = () => {
     const classes = useStyles();
     return (
       <div>
         <button className={classes.button}>Material-UI Button</button>
       </div>
     );
   };
   ```

4. **Glamorous:**
   Glamorous is another CSS-in-JS library that focuses on simplicity and performance. It offers a simple API for creating styled components.

   Example usage:
   ```jsx
   import glamorous from 'glamorous';

   const Button = glamorous.button({
     backgroundColor: 'blue',
     color: 'white',
     padding: '10px 20px',
     border: 'none',
   });

   const App = () => {
     return (
       <div>
         <Button>Styled Button</Button>
       </div>
     );
   };
   ```

These libraries offer various features and syntaxes for dynamic styling in React. Choose the one that aligns with your project's requirements, preferences, and existing tools.

## Conditional styling based on state

Conditional styling based on state in React allows you to dynamically change the styles of a component based on its current state. This can be particularly useful for providing visual feedback to users or creating interactive user interfaces. You can achieve this using CSS classes or inline styles, depending on your preferred approach.

Here's how you can conditionally apply styles based on the component's state:

**Using CSS Classes:**

1. Define your styles in a CSS file:

```css
.highlight {
  background-color: yellow;
  font-weight: bold;
}
```

2. In your React component, use conditional rendering to apply the CSS class based on the state:

```jsx
import React, { useState } from 'react';
import './styles.css';

const ConditionalStyling = () => {
  const [isHighlighted, setIsHighlighted] = useState(false);

  const toggleHighlight = () => {
    setIsHighlighted(!isHighlighted);
  };

  return (
    <div>
      <p className={isHighlighted ? 'highlight' : ''}>
        This text can be highlighted.
      </p>
      <button onClick={toggleHighlight}>Toggle Highlight</button>
    </div>
  );
};

export default ConditionalStyling;
```

**Using Inline Styles:**

1. In your React component, use inline styles and conditional rendering to apply styles based on the state:

```jsx
import React, { useState } from 'react';

const ConditionalStyling = () => {
  const [isHighlighted, setIsHighlighted] = useState(false);

  const toggleHighlight = () => {
    setIsHighlighted(!isHighlighted);
  };

  const highlightStyles = {
    backgroundColor: 'yellow',
    fontWeight: 'bold',
  };

  return (
    <div>
      <p style={isHighlighted ? highlightStyles : {}}>
        This text can be highlighted.
      </p>
      <button onClick={toggleHighlight}>Toggle Highlight</button>
    </div>
  );
};

export default ConditionalStyling;
```

In both examples, the component's state (`isHighlighted` in this case) determines whether the conditional styles should be applied. The styles are either defined in a CSS class (first example) or as an inline style object (second example). When the state changes, the component re-renders, and the styles are applied or removed based on the updated state.

Choose the approach that aligns with your styling preferences and the structure of your project. CSS classes provide better separation of concerns, while inline styles offer more dynamic styling control.