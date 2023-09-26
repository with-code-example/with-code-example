---
title: "A Guide to CRUD Operations with GORM"
subtitle: A Step-by-Step Tutorial on Creating, Reading, Updating, and Deleting Records using GORM in Go
description: Dive into GORM's CRUD operations and learn how to effortlessly manage data in your Go applications. Explore practical examples for creating, reading, updating, and deleting records using GORM.
tags: [golang, database, gorm]
slug: gorm-crud-operations-guide
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/golangwithexample/learn-gorm_yqoeio.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/golangwithexample/learn-gorm_yqoeio.png
comments: true
date: 2023-08-31
toc: true
draft: false
series: [GORM]
---

In the database management, CRUD operations are the backbone of applications, enabling the creation, retrieval, updating, and deletion of data. GORM, the powerful Go Object-Relational Mapping library, makes these operations a breeze by abstracting away the complexities of SQL statements. This article serves as your comprehensive guide to mastering CRUD operations with GORM, offering practical examples and insights into effectively managing data in your Go applications.

## Creating Records in GORM
Creating records is the foundation of any application. With GORM, this process becomes intuitive and efficient.

**Step 1: Define a Model**

Begin by defining a GORM model, which corresponds to a database table. For instance, consider a `Product` model:

```go
type Product struct {
    gorm.Model
    Name  string
    Price float64
}
```

**Step 2: Create a Record**

To create a new record, instantiate a struct of the model and use the `Create` method:

```go
newProduct := Product{Name: "Widget", Price: 29.99}
db.Create(&newProduct)
```

## Reading/Querying Records in GORM

Fetching data from the database is a crucial aspect of application development. GORM simplifies this process with its querying capabilities.

**Step 1: Query Records**

Use GORM's `Find` method to retrieve records from the database:

```go
var products []Product
db.Find(&products)
```

**Step 2: Condition-Based Queries**

Refine queries using conditions. For instance, retrieve products with prices above a certain threshold:

```go
var expensiveProducts []Product
db.Where("price > ?", 50).Find(&expensiveProducts)
```

## Updating Records in GORM

Updating records ensures your data remains accurate and up to date. GORM streamlines this process.

**Step 1: Retrieve a Record**

Fetch the record you want to update using GORM's `First` or `Find` method.

```go
var productToUpdate Product
db.First(&productToUpdate, 1) // Assuming product with ID 1
```

**Step 2: Update and Save**

Modify the fields you want to update and use GORM's `Save` method to persist the changes:

```go
productToUpdate.Name = "Updated Widget"
productToUpdate.Price = 39.99
db.Save(&productToUpdate)
```

Deleting Records in GORM

Deleting records is crucial for maintaining a clean and accurate database. GORM simplifies this process with its intuitive methods.

**Step 1: Retrieve a Record**

Fetch the record you want to delete using GORM's `First` or `Find` method.

```go
var productToDelete Product
db.First(&productToDelete, 1) // Assuming product with ID 1
```

**Step 2: Delete**

Use GORM's `Delete` method to remove the record from the database:

```go
db.Delete(&productToDelete)
```

**Soft Deleting Records**

GORM supports soft deleting, where records are marked as deleted without actually removing them from the database.

```go
db.Delete(&productToDelete) // Soft delete
```

**Restoring Soft Deleted Records**

Soft deleted records can be restored using GORM's `Unscoped` method:

```go
db.Unscoped().Model(&productToDelete).Update("DeletedAt", nil) // Restore soft deleted record
```

**Conclusion**

CRUD operations form the core of any data-driven application, and GORM's capabilities in this realm are truly remarkable. With GORM, creating, reading, updating, and deleting records becomes a seamless process, freeing you from the complexities of raw SQL queries. By following the step-by-step examples and insights provided in this guide, you've acquired the essential skills needed to effectively manage data in your Go applications. Remember that GORM empowers you to focus on building robust and feature-rich applications without getting bogged down in database intricacies. Embrace the power of GORM and unlock a new level of productivity in your Go projects.