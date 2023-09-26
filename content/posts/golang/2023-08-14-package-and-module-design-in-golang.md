---
title: Package and Module Design in Golang
description: Package and Module Design in Golang, Designing Cohesive and Reusable Packages, Creating APIs with Careful Consideration, Versioning and Dependency Management
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/awesome-blog/awesome-golang/Package_and_Module_Design_in_Golang_oxy812.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/awesome-blog/awesome-golang/Package_and_Module_Design_in_Golang_oxy812.png
tags: [golang, golang-best-practices]
comments: true
date: 2023-08-14
toc: true
draft: false
slug: package-and-module-design-in-golang
series: ['Golang Best Practices']
---

Go, also known as Golang, is a statically typed, compiled language that is popular among developers for its simplicity and robust support for concurrent programming. One of the key aspects of Go programming is its package and module systems, which allow for the creation of reusable, maintainable, and efficient code. This blog post will delve into the best practices for designing packages and modules in Go, focusing on creating cohesive and reusable packages, designing APIs with careful consideration, and managing versions and dependencies.

## Designing Cohesive and Reusable Packages

In Go, the most fundamental building blocks that enable code reuse are functions, with packages being the subsequent development in code reuse. Packages in Go are collections of Go source files that are grouped into a single unit, making the code modular, reusable, and maintainable. Each Go package resides in a single directory and is designed to handle a set of problems related to what that package aims to do.

When designing packages, it's important to follow the DRY (Don't Repeat Yourself) principle, which states that you should never write the same code again. Instead, you should strive to reuse and expand upon existing code as much as possible.

Go packages offer several design features that aid in creating "firewalls" within programs, allowing various pieces to be completely isolated, exposing only what is needed for a minimum and clean API. These features include:

### 1. Namespacing:  
This allows you to choose short and clear names for types and functions in a package without worrying if common names have already been used in other packages, as packages are self-contained.
**Example:**
```go
package user

import "fmt"

type User struct {
    ID   int
    Name string
}

func CreateUser(id int, name string) User {
    return User{ID: id, Name: name}
}

func PrintUser(u User) {
    fmt.Printf("User ID: %d, Name: %s\n", u.ID, u.Name)
}
```
### 2. Encapsulation:
Through the use of exported variables and functions, you control what is accessible outside of a package. This restricted visibility allows for the possibility of having a very intentional API at the package level.
**Example:**
```go
package main

import (
	"fmt"
)

type Employee struct {
	ID        int
	Name      string
	Salary    float64
	isManager bool
}

func NewEmployee(id int, name string, salary float64, isManager bool) Employee {
	return Employee{
		ID:        id,
		Name:      name,
		Salary:    salary,
		isManager: isManager,
	}
}

func (e *Employee) SetManagerStatus(isManager bool) {
	e.isManager = isManager
}

func (e Employee) PrintDetails() {
	fmt.Printf("ID: %d\nName: %s\nSalary: %.2f\nManager: %v\n", e.ID, e.Name, e.Salary, e.isManager)
}

func main() {
	emp := NewEmployee(1, "Alice", 50000.0, false)
	emp.PrintDetails()

	// Try to change manager status directly (encapsulation prevents this)
	// emp.isManager = true // Uncommenting this will result in a compilation error

	emp.SetManagerStatus(true)
	emp.PrintDetails()
}
```
In this example:

1.  We define a `struct` named `Employee`, containing fields like `ID`, `Name`, `Salary`, and an unexported `isManager` field.
2.  The `NewEmployee` function is a constructor that creates a new `Employee` instance.
3.  The `SetManagerStatus` method allows controlled modification of the `isManager` field.
4.  The `PrintDetails` method encapsulates the logic to print employee details, including the unexported `isManager` field.
5.  In the `main` function, we create an `Employee` instance, print its details, and then use the `SetManagerStatus` method to change the manager status.

Note that by making the `isManager` field unexported and providing a method to modify it, we encapsulate the internal state of the `Employee` object and control access to it. This prevents direct modification of the `isManager` field from outside the `Employee` type.

Remember that Go doesn't have traditional access modifiers like some other languages, so encapsulation relies on naming conventions and exporting or unexporting identifiers.
### 3. Internal packages:
These disallow the importing of code containing the element "internal" from outside the tree rooted at the parent directory of the internal directory.

## Creating APIs with Careful Consideration

When creating APIs, it's crucial to carefully consider what to expose to the outside world. In Go, this is achieved through the use of exported variables and functions. By controlling what is accessible outside of a package, you can provide a very intentional API at the package level, and have the flexibility to change unexported code without worrying about breaking that API.

Moreover, designing APIs with careful consideration can also help in ensuring the maintainability and durability of the software. As Dave Cheney stated in his Golang UK 2016 keynote talk, "the maintenance of Go programs, the ease of which they can change, will be a key factor in their decision".

## Versioning and Dependency Management

Go modules are collections of Go packages, and each project is a module. The packages used in the module are managed by Go with the  `go.mod`  file.

Go modules use the Semantic Versioning (Semver) system for versioning, which has three parts: major, minor, and patch. For example, a package in version 1.2.3 has 1 as its major version, 2 as its minor version, and 3 as its patch version.

Developers make their modules available for other developers to use from their own repository and publish with a version number. Go tools make it easier for you to manage dependencies, including getting a module’s source, upgrading, and so on.

When you're ready to release a new version of your module, you can use the  `go mod tidy`  command to ensure that your  `go.mod`  file includes all the necessary dependencies. Then, you can tag the new version in your version control system.

In conclusion, the design of packages and modules in Go is a crucial aspect of Go programming. By designing cohesive and reusable packages, creating APIs with careful consideration, and managing versions and dependencies effectively, you can write clean, maintainable, and efficient Go code.