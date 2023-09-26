---
title: "Golang MySQL Database Libraries With Examples"
subtitle: A Comprehensive Guide to Golang MySQL Database Libraries for Efficient Data Management
description: Discover the power of Golang MySQL database libraries through real-world examples and use cases. Explore GORM, Go-MySQL-Driver, SQLX, Beego, GORP, Go-firestorm, and SQLBoiler to streamline your data management process.
tags: [golang, go-libreary]
slug: golang-mysql-database-libraries
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/golangwithexample/Golang_MySQL_Database_Libraries_With_Examples.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/golangwithexample/Golang_MySQL_Database_Libraries_With_Examples.png
comments: true
date: 2023-08-27
toc: true
draft: false
---

Golang, also known as Go, has emerged as a preferred language for building robust and high-performance applications. When it comes to working with MySQL databases, Golang offers a range of powerful libraries that simplify database interactions and improve efficiency. In this article, we'll delve into some of the most popular Golang MySQL database libraries, exploring their features with practical examples.

## 1. [GORM](/series/gorm) (github.com/go-gorm/gorm)

GORM is a feature-rich Object-Relational Mapping (ORM) library for Golang that simplifies database operations by providing an intuitive API for working with database models. Let's take a look at a simple example of how to use GORM:
### GORM Example
```go
package main

import (
	"fmt"
	"gorm.io/driver/mysql"
	"gorm.io/gorm"
)

type User struct {
	ID   uint
	Name string
	Age  int
}

func main() {
	dsn := "user:password@tcp(localhost:3306)/dbname?charset=utf8mb4&parseTime=True&loc=Local"
	db, err := gorm.Open(mysql.Open(dsn), &gorm.Config{})
	if err != nil {
		panic("Failed to connect to database")
	}

	user := User{Name: "John", Age: 30}
	result := db.Create(&user)
	fmt.Println("Created user:", result.RowsAffected)
}
```

## 2. Go-MySQL-Driver (github.com/go-sql-driver/mysql)

Go-MySQL-Driver is the official MySQL driver for Go's database/sql package. It provides a low-level but efficient way to interact with MySQL databases. Here's a basic example of how to use the Go-MySQL-Driver:

### Go-MySQL-Driver Example

```go
package main

import (
	"database/sql"
	"fmt"
	_ "github.com/go-sql-driver/mysql"
)

func main() {
	dsn := "user:password@tcp(localhost:3306)/dbname"
	db, err := sql.Open("mysql", dsn)
	if err != nil {
		panic("Failed to connect to database")
	}
	defer db.Close()

	var name string
	err = db.QueryRow("SELECT name FROM users WHERE id = ?", 1).Scan(&name)
	if err != nil {
		panic(err)
	}

	fmt.Println("User's name:", name)
}
```

## 3. SQLX (github.com/jmoiron/sqlx)

SQLX is a library built on top of Go's database/sql package that enhances database interactions by providing a simpler API and support for mapping query results directly to structs. Here's a simple SQLX example:

### SQLX Example
```go
package main

import (
	"fmt"
	"github.com/jmoiron/sqlx"
	_ "github.com/go-sql-driver/mysql"
)

type User struct {
	ID   int
	Name string
	Age  int
}

func main() {
	dsn := "user:password@tcp(localhost:3306)/dbname"
	db, err := sqlx.Connect("mysql", dsn)
	if err != nil {
		panic("Failed to connect to database")
	}
	defer db.Close()

	user := User{}
	err = db.Get(&user, "SELECT * FROM users WHERE id = ?", 1)
	if err != nil {
		panic(err)
	}

	fmt.Printf("User ID: %d, Name: %s, Age: %d\n", user.ID, user.Name, user.Age)
}
```

## 4. Beego (github.com/astaxie/beego/orm)

Beego is a popular web framework for Go, and it includes an ORM package that supports various databases, including MySQL. Here's an example of using Beego's ORM:

### Beego MySql Example
```go
package main

import (
	"fmt"
	"github.com/astaxie/beego/orm"
	_ "github.com/go-sql-driver/mysql"
)

type User struct {
	ID   int
	Name string
	Age  int
}

func init() {
	orm.RegisterDriver("mysql", orm.DRMySQL)
	orm.RegisterDataBase("default", "mysql", "user:password@tcp(localhost:3306)/dbname")
	orm.RegisterModel(new(User))
}

func main() {
	o := orm.NewOrm()

	user := User{ID: 1}
	err := o.Read(&user)
	if err == orm.ErrNoRows {
		fmt.Println("User not found")
	} else if err == nil {
		fmt.Printf("User ID: %d, Name: %s, Age: %d\n", user.ID, user.Name, user.Age)
	}
}
```

## 5. GORP (github.com/go-gorp/gorp)

GORP is another ORM library for Golang that offers support for database interactions and mapping. It simplifies CRUD operations and database migrations. Here's an example of using GORP with MySQL:

### GORP MySql Example
```go
package main

import (
	"fmt"
	"database/sql"
	_ "github.com/go-sql-driver/mysql"
	"gopkg.in/gorp.v2"
)

type User struct {
	ID   int
	Name string
	Age  int
}

func main() {
	dsn := "user:password@tcp(localhost:3306)/dbname"
	db, err := sql.Open("mysql", dsn)
	if err != nil {
		panic("Failed to connect to database")
	}
	defer db.Close()

	dbMap := &gorp.DbMap{Db: db, Dialect: gorp.MySQLDialect{}}
	
	user := User{}
	err = dbMap.SelectOne(&user, "SELECT * FROM users WHERE id = ?", 1)
	if err != nil {
		panic(err)
	}

	fmt.Printf("User ID: %d, Name: %s, Age: %d\n", user.ID, user.Name, user.Age)
}
```

## 6. Go-firestorm (github.com/firestorm-go/firestorm)

Go-firestorm is a library that focuses on simplicity and flexibility when working with SQL databases. It provides an easy-to-use API for database interactions. Here's a basic example of how to use Go-firestorm:

### Go-firestorm MySql Example

```go
package main

import (
	"fmt"
	"github.com/firestorm-go/firestorm"
)

type User struct {
	ID   int    `db:"id"`
	Name string `db:"name"`
	Age  int    `db:"age"`
}

func main() {
	db, err := firestorm.New("mysql", "user:password@tcp(localhost:3306)/dbname")
	if err != nil {
		panic("Failed to connect to database")
	}
	defer db.Close()

	var user User
	err = db.SelectOne(&user, "SELECT * FROM users WHERE id = ?", 1)
	if err != nil {
		panic(err)
	}

	fmt.Printf("User ID: %d, Name: %s, Age: %d\n", user.ID, user.Name, user.Age)
}
```

7. SQLBoiler (github.com/volatiletech/sqlboiler)

SQLBoiler is an ORM that generates Go code from your database schema. It aims to reduce the amount of boilerplate code required for database interactions. Here's how you can use SQLBoiler:

### SQLBoiler Example

```sh
# Install SQLBoiler
go install github.com/volatiletech/sqlboiler/v4@latest

# Generate code based on the database schema
sqlboiler mysql
```

Generated code for the `User` table:

```go
package models

import "time"

type User struct {
	ID        int       `boil:"id" json:"id" toml:"id" yaml:"id"`
	Name      string    `boil:"name" json:"name" toml:"name" yaml:"name"`
	Age       int       `boil:"age" json:"age" toml:"age" yaml:"age"`
	CreatedAt time.Time `boil:"created_at" json:"created_at" toml:"created_at" yaml:"created_at"`
	UpdatedAt time.Time `boil:"updated_at" json:"updated_at" toml:"updated_at" yaml:"updated_at"`
	DeletedAt time.Time `boil:"deleted_at" json:"deleted_at" toml:"deleted_at" yaml:"deleted_at"`
}
```

**Conclusion**

Golang MySQL database libraries offer a range of features and capabilities to simplify database interactions and enhance the efficiency of your applications. Whether you're looking for an ORM like GORM or SQLBoiler, a driver like Go-MySQL-Driver, a simpler API like SQLX or Go-firestorm, or integration with a web framework like Beego or GORP, there's a library that fits your needs. By leveraging these libraries, you can focus on building your application's logic without getting bogged down in the intricacies of database management.