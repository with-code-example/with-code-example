---
title: "Error Handling in Golang: A Comprehensive Guide with Examples"
subtitle: Handle errors in golang
description: Golang provides a robust error handling mechanism that allows developers to manage errors effectively. By understanding how to use error types and custom errors, defer and panic, and error wrapping, you can build reliable and resilient applications that gracefully handle unexpected situations.
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/awesome-blog/awesome-golang/Error_Handling_aqphgs.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/awesome-blog/awesome-golang/Error_Handling_aqphgs.png
tags: [golang, golang-best-practices, error-handling]
comments: true
date: 2023-08-09
draft: false
toc: true
slug: error-handling-in-golang-a-comprehensive-guide-with-examples
series: ['Golang Best Practices']
---

As a developer, you know that error handling is a critical aspect of building reliable and robust applications. Golang provides powerful error handling mechanisms that help you identify and manage errors effectively. In this article, we'll explore three essential topics related to error handling in Golang: Using Error Types and Custom Errors, Defer and Panic - When to Use Them Wisely, and Error Wrapping and Error Chains. Let's dive in!

## 1. Using Error Types and Custom Errors

In Golang, errors are represented by the built-in `error` interface, which is defined as:

```go
type error interface {
    Error() string
}
```

To create custom errors, implement this interface for your error type. Custom errors enable you to provide additional context and information about the error.

Example:

```go
package main

import (
    "fmt"
)

type MyError struct {
    message string
}

func (e MyError) Error() string {
    return e.message
}

func divide(a, b int) (int, error) {
    if b == 0 {
        return 0, MyError{"division by zero"}
    }
    return a / b, nil
}

func main() {
    result, err := divide(10, 0)
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("Result:", result)
    }
}
```

Output:
```
Error: division by zero
```

## 2. Defer and Panic - When to Use Them Wisely

Golang provides the `defer` keyword, which allows you to schedule a function call to be executed after the surrounding function returns. It's commonly used for cleanup tasks like closing files or releasing resources.

Example:

```go
package main

import (
    "fmt"
)

func processFile() {
    fmt.Println("Opening file...")
    defer fmt.Println("Closing file...")
    // Code to process the file goes here
}

func main() {
    processFile()
}
```

Output:
```
Opening file...
Closing file...
```

On the other hand, `panic` is used to indicate unexpected and unrecoverable errors. When a `panic` occurs, it immediately stops the execution of the current function and starts unwinding the stack, executing deferred functions along the way.

Example:

```go
package main

import (
    "fmt"
)

func performTask() {
    fmt.Println("Starting task...")
    panic("Unexpected error occurred!")
    fmt.Println("Task completed.") // This line will not be executed
}

func main() {
    performTask()
}
```

Output:
```
Starting task...
panic: Unexpected error occurred!
```

## 3. Error Wrapping and Error Chains

When handling errors, it's often useful to wrap the original error with additional context to provide a more comprehensive understanding of the error's origin. Golang provides the `fmt.Errorf()` function to create a new error that wraps the original error.

Example:

```go
package main

import (
    "fmt"
    "errors"
)

func process() error {
    err := doSomething()
    if err != nil {
        return fmt.Errorf("process failed: %w", err)
    }
    return nil
}

func doSomething() error {
    return errors.New("something went wrong")
}

func main() {
    err := process()
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("Success!")
    }
}
```

Output:
```
Error: process failed: something went wrong
```

By using `%w` verb in `fmt.Errorf()`, we create an error chain that retains information about the original error.

In conclusion, Golang provides a robust error handling mechanism that allows developers to manage errors effectively. By understanding how to use error types and custom errors, defer and panic, and error wrapping, you can build reliable and resilient applications that gracefully handle unexpected situations.