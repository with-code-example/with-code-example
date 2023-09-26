---
title: "Hooks and Callbacks in GORM"
subtitle: A Comprehensive Guide to Harnessing the Power of Hooks and Callbacks in GORM for Tailored Database Workflows
description: Elevate your GORM skills with hooks and callbacks. Explore available hooks, their purposes, and learn to implement custom callbacks for flexible and personalized database interactions in Go.
tags: [golang, database, gorm]
slug: gorm-hooks-callbacks-guide
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/golangwithexample/learn-gorm_yqoeio.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/golangwithexample/learn-gorm_yqoeio.png
comments: true
date: 2023-09-04
toc: true
draft: false
series: [GORM]
---

[Download PDF](https://res.cloudinary.com/harendra21/image/upload/v1694109746/golangwithexample/PDF/GORM_Mastery_gmpc1k.pdf)

In the realm of database management, customization is key to crafting efficient and tailored workflows. GORM, the dynamic Go Object-Relational Mapping library, empowers developers with hooks and callbacks, offering a way to inject custom logic into various stages of the database interaction process. This comprehensive guide unveils the potential of hooks and callbacks in GORM, exploring their utilization, the array of available hooks and their purposes, and the art of implementing your own custom callbacks. By the end, you'll be equipped to elevate your database interactions in Go, crafting workflows that align perfectly with your application's unique requirements.

## Using GORM Hooks in GORM

Hooks are your gateway to tapping into GORM's operations and infusing your own logic.

### Available Hooks and Their Purposes in GORM

GORM provides an array of hooks, each catering to a specific point in the data lifecycle:

- `BeforeCreate`: Triggered before a new record is created.
- `AfterCreate`: Triggered after a new record is created.
- `BeforeUpdate`: Triggered before a record is updated.
- `AfterUpdate`: Triggered after a record is updated.
- `BeforeDelete`: Triggered before a record is deleted.
- `AfterDelete`: Triggered after a record is deleted.


**Examples demonstrating how to use GORM's hooks (`BeforeCreate`, `AfterCreate`, `BeforeUpdate`, `AfterUpdate`, `BeforeDelete`, `AfterDelete`) in a Go application:**

```go
package main

import (
	"fmt"
	"log"
	"time"

	"gorm.io/driver/sqlite"
	"gorm.io/gorm"
	"gorm.io/gorm/logger"
)

type User struct {
	ID        uint
	Name      string
	CreatedAt time.Time
	UpdatedAt time.Time
}

func main() {
	dsn := "gorm.db"
	db, err := gorm.Open(sqlite.Open(dsn), &gorm.Config{
		Logger: logger.Default.LogMode(logger.Info),
	})
	if err != nil {
		log.Fatalf("failed to connect to database: %v", err)
	}

	// AutoMigrate will create the "users" table and apply the schema
	db.AutoMigrate(&User{})

	user := User{Name: "Alice"}

	// BeforeCreate hook
	db.Before("gorm:create").Create(&user)
	fmt.Println("User before create:", user)

	// AfterCreate hook
	db.Create(&user)
	fmt.Println("User after create:", user)

	user.Name = "Bob"

	// BeforeUpdate hook
	db.Before("gorm:update").Updates(&user)
	fmt.Println("User before update:", user)

	// AfterUpdate hook
	db.Updates(&user)
	fmt.Println("User after update:", user)

	// BeforeDelete hook
	db.Before("gorm:delete").Delete(&user)
	fmt.Println("User before delete:", user)

	// AfterDelete hook
	db.Delete(&user)
	fmt.Println("User after delete:", user)
}
```

In this example, we define a `User` struct and configure GORM to use an SQLite database. We then demonstrate the usage of various hooks:

- `BeforeCreate`: Triggered before creating a new user record. We print the user information before and after the record is created.
- `AfterCreate`: Triggered after creating a new user record.
- `BeforeUpdate`: Triggered before updating an existing user record. We print the user information before and after the record is updated.
- `AfterUpdate`: Triggered after updating an existing user record.
- `BeforeDelete`: Triggered before deleting a user record. We print the user information before and after the record is deleted.
- `AfterDelete`: Triggered after deleting a user record.

Please note that the behavior of hooks may vary based on the database dialect and version of GORM. Always refer to the official documentation for the most accurate and up-to-date information.


## Implementing Custom Callbacks in GORM

Custom callbacks allow you to inject your own logic into the data interaction process.

**Step 1: Define Your Callback Function**

Create a function that matches the signature `func(*gorm.DB)`.

```go
func MyCustomCallback(db *gorm.DB) {
    // Your custom logic here
}
```

**Step 2: Register the Callback**

Use GORM's `Callback` method to register your custom callback for a specific hook.

```go
db.Callback().Create().After("gorm:create").Register("my_custom_callback", MyCustomCallback)
```

**Conclusion**

GORM's hooks and callbacks provide a versatile mechanism to infuse your database interactions with custom logic. By tapping into the available hooks and understanding their purposes, you can tailor your workflows precisely to your application's needs. Implementing custom callbacks allows you to inject specific behaviors at strategic points in the data lifecycle. As you apply the insights and examples from this guide, remember that GORM's hooks and callbacks empower you to fine-tune your database operations in Go, enabling you to build applications that seamlessly align with your unique requirements.