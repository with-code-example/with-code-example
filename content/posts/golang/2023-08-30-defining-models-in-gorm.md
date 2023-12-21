---
title: "Defining Models in GORM"
subtitle: A Comprehensive Guide to Crafting Effective Models in GORM for Seamless Database Interaction
description: Learn how to create, annotate, and associate models using GORM for efficient and organized database management in your applications.
tags: [golang, database, gorm]
slug: defining-models-in-gorm
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/golangwithexample/learn-gorm_yqoeio.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/golangwithexample/learn-gorm_yqoeio.png
comments: true
date: 2023-08-30
toc: true
draft: false
series: [GORM]
---

The core of database administration using GORM is the skill of defining models. Models serve as a link between the object-oriented structure of your programme and the relational world of databases. This article digs into the art of creating successful models in GORM, examining how to design structured Go structs, annotate fields with tags, and develop links across models in order to maximise the potential of your application's database interactions.

## Creating Struct Models in GORM

Well-defined struct models are the brains of your GORM-based application. Every field in a struct model corresponds to a column in a database table, which is represented by a struct model. This is how struct models are made:


```go
package models

import (
    "gorm.io/gorm"
)

type User struct {
    gorm.Model
    Name  string
    Email string `gorm:"uniqueIndex"`
    Age   int
}
```

In this example, the `User` struct models a database table with columns `ID`, `CreatedAt`, `UpdatedAt`, `DeletedAt`, `Name`, `Email`, and `Age`.

## Adding Tags for Field Mapping

GORM relies on struct tags to map struct fields to database columns. Tags provide metadata that guides GORM in database operations. Common tags include:

- `gorm:"primaryKey"`: Marks a field as the primary key.
- `gorm:"uniqueIndex"`: Creates a unique index on the field.
- `gorm:"not null"`: Specifies that the field cannot be null.
- `gorm:"column:custom_name"`: Maps the field to a custom column name.

```go
type Product struct {
    gorm.Model
    Name     string
    Price    float64
    Category string `gorm:"column:item_category"`
}
```

In this example, the `Category` field is mapped to the `item_category` column.

## Model Associations and Relationships

GORM excels in modeling complex relationships between tables. Associations define how different models relate to each other, enabling you to fetch related data easily.

### One-to-One Relationship:

```go
type User struct {
    gorm.Model
    Profile Profile
}

type Profile struct {
    gorm.Model
    UserID  uint
    Address string
}
```

In this example, a `User` has one `Profile`. The `UserID` field in the `Profile` struct is used as the foreign key.

### One-to-Many Relationship:

```go
type User struct {
    gorm.Model
    Orders []Order
}

type Order struct {
    gorm.Model
    UserID  uint
    Product string
}
```

Here, a `User` can have multiple `Orders`, each associated with the user via the `UserID` foreign key.

### Many-to-Many Relationship:

```go
type User struct {
    gorm.Model
    Roles []Role `gorm:"many2many:user_roles;"`
}

type Role struct {
    gorm.Model
    Name string
}
```

This example demonstrates a many-to-many relationship between `User` and `Role` models. GORM handles the creation of the intermediate table `user_roles`.

## Using Associations in Queries:

Associations simplify querying related data. For instance, to fetch a user's orders:

```go
var user User
db.Preload("Orders").Find(&user, 1)
```

The `Preload` method eagerly loads the user's orders in the query result.

**Conclusion**

The key to efficient database administration in your applications is defining models in GORM. You build a solid basis for smooth database interactions by creating relationships between models, annotating fields with relevant tags, and building organised struct models. One-to-one, one-to-many, and many-to-many relationship handling in GORM enables you to model complicated data situations with ease. Remember that a well-structured foundation results in scalable and maintainable applications, making your database management journey easy and fruitful as you set out to learn GORM's model definition capabilities.