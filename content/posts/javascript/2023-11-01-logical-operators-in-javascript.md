---
title: Understanding Logical Operators in JavaScript
subtitle: Making Decisions and Evaluating Conditions description: Learn about the key logical operators in JavaScript, including AND, OR, NOT, XOR, short-circuit evaluation, and the ternary operator.
slug: logical-operators-in-javascript
tags: [javascript]
featured_image: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_50_bold:Logical%20Operators%20in%20JavaScript,co_rgb:fff/javascriptwithexample/bg6.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_50_bold:Logical%20Operators%20in%20JavaScript,co_rgb:fff/javascriptwithexample/bg6.png
comments: true
date: 2023-11-01
toc: true
draft: false
---


JavaScript provides several logical operators that are used to perform logical operations on Boolean values. These operators are frequently used to make decisions, control the flow of code, and evaluate conditions. Here are the most commonly used logical operators in JavaScript:

## 1. **Logical AND (`&&`)**:
   - The `&&` operator returns `true` if both operands are `true`.
   - It returns `false` if at least one of the operands is `false`.
   - Example:

   ```javascript
   const a = true;
   const b = false;
   const result = a && b; // result is false
   ```

## 2. **Logical OR (`||`)**:
   - The `||` operator returns `true` if at least one of the operands is `true`.
   - It returns `false` if both operands are `false`.
   - Example:

   ```javascript
   const a = true;
   const b = false;
   const result = a || b; // result is true
   ```

## 3. **Logical NOT (`!`)**:
   - The `!` operator is used to negate a Boolean value. It returns the opposite value.
   - Example:

   ```javascript
   const a = true;
   const result = !a; // result is false
   ```

## 4. **Short-Circuit Evaluation**:
   - JavaScript performs short-circuit evaluation with `&&` and `||`. This means that it stops evaluating the expression as soon as the outcome is known.
   - For `&&`, if the first operand is `false`, the second operand is not evaluated.
   - For `||`, if the first operand is `true`, the second operand is not evaluated.

   ```javascript
   const a = false;
   const b = true;
   const result = a && someFunction(); // someFunction() is not called
   const result2 = b || someFunction(); // someFunction() is not called
   ```

## 5. **Logical XOR (Exclusive OR)**:
   - JavaScript does not have a built-in `XOR` operator, but it can be simulated using the `!==` (not equal) operator.
   - `a !== b` returns `true` if one of the operands is `true` and the other is `false`.

   ```javascript
   const a = true;
   const b = false;
   const result = a !== b; // result is true
   ```

## 6. **Ternary Operator (Conditional Operator)**:
   - The ternary operator (`condition ? expr1 : expr2`) is a shorthand way of expressing conditional logic.
   - It returns `expr1` if `condition` is `true`, and `expr2` if `condition` is `false`.
   - Example:

   ```javascript
   const age = 25;
   const canVote = age >= 18 ? "Yes" : "No"; // canVote is "Yes"
   ```

These logical operators are fundamental to making decisions and controlling the flow of your JavaScript code based on conditions and Boolean values. They are commonly used in if statements, while loops, and other control structures.