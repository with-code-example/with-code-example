---
title: "React Forms: Controlled Components & Handling"
subtitle: Building Interactive User Interfaces with Controlled Components
description: "Master form creation in React using controlled components and effective form handling. Explore two-way binding and form submission. Dive into examples and collect user input data with confidence."
slug: react-forms-guide
tags: [javascript, reactjs]
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/javascriptwithexample/React_Js_Course_-_Forms_and_Controlled_Components_obcm7x.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/javascriptwithexample/React_Js_Course_-_Forms_and_Controlled_Components_obcm7x.png
comments: true
date: 2023-09-01
toc: true
draft: false
series: [React Js Course]
audio: https://with-code-example.s3.ap-south-1.amazonaws.com/blog/react-forms-guide.e5173e30-4b47-42e2-8967-00e826e297e4.mp3
canonical_url: https://courses.withcodeexample.com/course/react-js/forms/
---

Creating forms in React involves building user interfaces for collecting and processing user input. React provides a convenient way to handle form elements and their values using state and event handling. Here's how you can create forms in React:

## Create form in React
**1. Controlled Components:**
A controlled component in React is a form element whose value is controlled by React's state. You manage the input value and handle changes using state and event handlers.

```jsx
import React, { useState } from 'react';

const FormExample = () => {
  const [inputValue, setInputValue] = useState('');

  const handleInputChange = (event) => {
    setInputValue(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log('Form submitted with value:', inputValue);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Enter something:
        <input type="text" value={inputValue} onChange={handleInputChange} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
};

export default FormExample;
```

**2. Using Multiple Inputs:**
For forms with multiple inputs, you can manage each input's value using separate state variables and event handlers.

```jsx
import React, { useState } from 'react';

const MultiInputForm = () => {
  const [firstName, setFirstName] = useState('');
  const [lastName, setLastName] = useState('');

  const handleFirstNameChange = (event) => {
    setFirstName(event.target.value);
  };

  const handleLastNameChange = (event) => {
    setLastName(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log('Form submitted with values:', firstName, lastName);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        First Name:
        <input type="text" value={firstName} onChange={handleFirstNameChange} />
      </label>
      <label>
        Last Name:
        <input type="text" value={lastName} onChange={handleLastNameChange} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
};

export default MultiInputForm;
```

**3. Select and Textarea:**
For `<select>` and `<textarea>` elements, the approach is similar to `<input>` elements.

```jsx
import React, { useState } from 'react';

const FormWithSelectAndTextarea = () => {
  const [selectedOption, setSelectedOption] = useState('option1');
  const [textareaValue, setTextareaValue] = useState('');

  const handleSelectChange = (event) => {
    setSelectedOption(event.target.value);
  };

  const handleTextareaChange = (event) => {
    setTextareaValue(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log('Form submitted with values:', selectedOption, textareaValue);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Select an option:
        <select value={selectedOption} onChange={handleSelectChange}>
          <option value="option1">Option 1</option>
          <option value="option2">Option 2</option>
          <option value="option3">Option 3</option>
        </select>
      </label>
      <label>
        Textarea:
        <textarea value={textareaValue} onChange={handleTextareaChange} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
};

export default FormWithSelectAndTextarea;
```

By using React state and event handlers, you can create flexible and interactive forms that allow users to input data and submit it to your application for processing.


## Handling form input using state in react

Handling form input using state in React involves creating controlled components where the value of the input element is managed by React's state. This allows you to keep the form input and its corresponding state synchronized and respond to changes in the input value.

Here's a step-by-step guide on how to handle form input using state in React:

**1. Set Up State:**
Start by creating a state variable to hold the value of the input field.

```jsx
import React, { useState } from 'react';

const FormInputExample = () => {
  const [inputValue, setInputValue] = useState('');

  return (
    <div>
      <input
        type="text"
        value={inputValue}
        onChange={(event) => setInputValue(event.target.value)}
      />
      <p>Input value: {inputValue}</p>
    </div>
  );
};

export default FormInputExample;
```

**2. Value and onChange:**
In the `input` element, set the `value` attribute to the state variable (`inputValue` in this case). This makes the input a controlled component where its value is tied to the state.

The `onChange` event handler updates the state (`inputValue`) whenever the input value changes.

**3. Displaying Input Value:**
You can display the current input value in real-time by using the `inputValue` state variable in your JSX.

By following these steps, you create a controlled input component that updates its value through state. This approach gives you control over the input value and enables you to manage its changes, validations, and submission.

If you have multiple input fields, you can manage each input's value using separate state variables:

```jsx
import React, { useState } from 'react';

const MultiInputForm = () => {
  const [firstName, setFirstName] = useState('');
  const [lastName, setLastName] = useState('');

  return (
    <div>
      <input
        type="text"
        value={firstName}
        onChange={(event) => setFirstName(event.target.value)}
      />
      <input
        type="text"
        value={lastName}
        onChange={(event) => setLastName(event.target.value)}
      />
      <p>First Name: {firstName}</p>
      <p>Last Name: {lastName}</p>
    </div>
  );
};

export default MultiInputForm;
```

By using state to manage form input values, you create a clear flow of data between the user interface and the component's internal state, enabling you to handle user input effectively and create dynamic and interactive forms.


## Controlled components and two-way binding

Controlled components and two-way binding are concepts used in React to ensure that the values of form elements are synchronized between the component's state and the user interface. They enable you to manage form input and display the current input value while allowing you to handle changes and updates in a controlled manner.

**Controlled Components:**

A controlled component is a form element (input, textarea, select) whose value is controlled by React's state. This means that the value of the input is bound to a state variable, and changes to the input value are managed by updating the state. This approach allows React to have complete control over the value of the input.

```jsx
import React, { useState } from 'react';

const ControlledComponentExample = () => {
  const [inputValue, setInputValue] = useState('');

  const handleInputChange = (event) => {
    setInputValue(event.target.value);
  };

  return (
    <div>
      <input
        type="text"
        value={inputValue}
        onChange={handleInputChange}
      />
      <p>Input value: {inputValue}</p>
    </div>
  );
};

export default ControlledComponentExample;
```

**Two-Way Binding:**

Two-way binding is a pattern where changes to a form element's value in the user interface are reflected back to the component's state, and changes in the state are automatically reflected in the user interface. In the example above, the input value is bound to the `inputValue` state variable. When the user types into the input, the state is updated, and when the state changes, the input value is automatically updated.

```jsx
<input
  type="text"
  value={inputValue}
  onChange={handleInputChange}
/>
```

Here, the `value` attribute of the input is set to the `inputValue` state variable, establishing the binding. The `onChange` event handler updates the state when the user types into the input.

Controlled components and two-way binding ensure that the user interface remains consistent with the component's state. They provide a straightforward and predictable way to manage form input and make it easy to perform validations, handle submission, and create interactive user interfaces.

## Form submission and handling

Form submission and handling in React involve collecting and processing user input data from form elements. React provides various approaches for handling form submissions, including controlled components, event handling, and handling asynchronous operations like API calls.

Here's a step-by-step guide on how to handle form submission in React:

**1. Set Up State:**
Create state variables for the form inputs to hold their values.

```jsx
import React, { useState } from 'react';

const FormSubmissionExample = () => {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');

  const handleNameChange = (event) => {
    setName(event.target.value);
  };

  const handleEmailChange = (event) => {
    setEmail(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log('Form submitted with values:', name, email);
    // Perform additional actions here, such as API calls
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={name} onChange={handleNameChange} />
      </label>
      <label>
        Email:
        <input type="email" value={email} onChange={handleEmailChange} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
};

export default FormSubmissionExample;
```

**2. Handle Form Input Changes:**
For each form input, use state variables to manage their values. Set up event handlers (`handleNameChange` and `handleEmailChange` in this example) to update the state when the user types into the input fields.

**3. Prevent Default Behavior:**
In the `handleSubmit` function, prevent the default form submission behavior using `event.preventDefault()`. This prevents the page from reloading.

**4. Perform Actions:**
Within the `handleSubmit` function, you can perform actions such as validating the data, making API calls, or updating the application's state based on the form data.

**5. Display Feedback:**
You can provide feedback to the user based on the outcome of the form submission. This can be done by rendering success messages, error messages, or loading indicators.

By following these steps, you create a controlled form that captures user input and handles form submission. You can extend this pattern to include more form fields, validations, and additional actions.

Remember that form handling can involve more complex scenarios, such as asynchronous operations, form validation libraries, or using context to manage the form's state globally. Depending on your project's requirements, you might choose to implement additional solutions to enhance the form submission process.