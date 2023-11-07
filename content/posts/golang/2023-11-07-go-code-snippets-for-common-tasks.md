---
title: 10 Common Go (Golang) Code Snippets for Various Tasks
subtitle: Explore Useful Go Code Snippets for Everyday Programming
description: Discover 10 Go code snippets for common programming tasks, including Hello World, input handling, goroutines, slices, error handling, HTTP servers, JSON operations, concurrency, file I/O, and sorting. Use these snippets to simplify your Go development.
slug: go-code-snippets-for-common-tasks
tags: [golang, snippets]
featured_image: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_45_bold:10%20Common%20Go%20(Golang)%20Code%20Snippets,co_rgb:fff/golangwithexample/bg5.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_45_bold:10%20Common%20Go%20(Golang)%20Code%20Snippets,co_rgb:fff/golangwithexample/bg5.png
comments: true
date: 2023-11-07
toc: true
draft: false
---


It's challenging to provide a definitive list of the "top 10" Go (Golang) code snippets, as the usefulness of code snippets depends on the specific problem you're trying to solve. However, I can provide you with ten commonly used Go code snippets that cover a range of tasks and concepts:

## 1. Hello World:
   
   ```go
   package main

   import "fmt"

   func main() {
       fmt.Println("Hello, World!")
   }
   ```

## 2. Reading Input from Console:
   ```go
   package main

   import (
       "fmt"
       "bufio"
       "os"
   )

   func main() {
       scanner := bufio.NewScanner(os.Stdin)
       fmt.Print("Enter text: ")
       scanner.Scan()
       input := scanner.Text()
       fmt.Println("You entered:", input)
   }
   ```

## 3. Creating a Goroutine:
   ```go
   package main

   import (
       "fmt"
       "time"
   )

   func printNumbers() {
       for i := 1; i <= 5; i++ {
           fmt.Println(i)
           time.Sleep(time.Second)
       }
   }

   func main() {
       go printNumbers()
       time.Sleep(3 * time.Second)
   }
   ```

## 4. Working with Slices:
   ```go
   package main

   import "fmt"

   func main() {
       numbers := []int{1, 2, 3, 4, 5}
       fmt.Println("Slice:", numbers)
       fmt.Println("Length:", len(numbers))
       fmt.Println("First Element:", numbers[0])
   }
   ```

## 5. Error Handling:
   ```go
   package main

   import (
       "errors"
       "fmt"
   )

   func divide(a, b float64) (float64, error) {
       if b == 0 {
           return 0, errors.New("division by zero")
       }
       return a / b, nil
   }

   func main() {
       result, err := divide(10, 2)
       if err != nil {
           fmt.Println("Error:", err)
           return
       }
       fmt.Println("Result:", result)
   }
   ```

## 6. HTTP Server:
   ```go
   package main

   import (
       "fmt"
       "net/http"
   )

   func handler(w http.ResponseWriter, r *http.Request) {
       fmt.Fprintln(w, "Hello, HTTP!")
   }

   func main() {
       http.HandleFunc("/", handler)
       http.ListenAndServe(":8080", nil)
   }
   ```

## 7. JSON Marshalling and Unmarshalling:
   ```go
   package main

   import (
       "fmt"
       "encoding/json"
   )

   type Person struct {
       Name  string `json:"name"`
       Age   int    `json:"age"`
   }

   func main() {
       jsonStr := `{"name":"Alice", "age":30}`
       var person Person
       err := json.Unmarshal([]byte(jsonStr), &person)
       if err != nil {
           fmt.Println("Error:", err)
           return
       }
       fmt.Println("Name:", person.Name)
       fmt.Println("Age:", person.Age)
   }
   ```

## 8. Concurrency with Wait Groups:
   ```go
   package main

   import (
       "fmt"
       "sync"
   )

   func worker(id int, wg *sync.WaitGroup) {
       defer wg.Done()
       fmt.Printf("Worker %d started\n", id)
   }

   func main() {
       var wg sync.WaitGroup
       for i := 1; i <= 5; i++ {
           wg.Add(1)
           go worker(i, &wg)
       }
       wg.Wait()
       fmt.Println("All workers have finished.")
   }
   ```

## 9. Reading and Writing Files:
   ```go
   package main

   import (
       "fmt"
       "io/ioutil"
   )

   func main() {
       data := []byte("Hello, File!")
       err := ioutil.WriteFile("example.txt", data, 0644)
       if err != nil {
           fmt.Println("Error:", err)
           return
       }
       content, err := ioutil.ReadFile("example.txt")
       if err != nil {
           fmt.Println("Error:", err)
           return
       }
       fmt.Println("File Content:", string(content))
   }
   ```

## 10. Sorting Slices:
    ```go
    package main

    import (
        "fmt"
        "sort"
    )

    func main() {
        numbers := []int{5, 2, 9, 1, 5}
        sort.Ints(numbers)
        fmt.Println("Sorted Slice:", numbers)
    }
    ```

These code snippets cover a range of common Go programming tasks and concepts, from basic I/O operations to concurrency, error handling, and more. Feel free to adapt and use them as needed in your Go projects.
