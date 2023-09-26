---
layout: post
title: Golang Program Example to Sort an Array
subtitle: Learn how to sort an array in golang with examples
description: Learn how to sort an array in golang with examples
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/awesome-blog/awesome-golang/Golang_Example_To_Sort_an_Array_he41of.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/awesome-blog/awesome-golang/Golang_Example_To_Sort_an_Array_he41of.png
tags: [golang, example]
comments: true
date: 2023-08-03
toc: true
draft: false
slug: golang-program-example-to-sort-an-array
---
Go provides a built-in package called `sort` that you can use to sort arrays and slices. Here's a simple example of how to sort an integer array in ascending order:

```go
package main

import (
	"fmt"
	"sort"
)

func main() {
	// Sample unsorted integer array
	numbers := []int{5, 2, 9, 1, 5, 6}

	// Sorting the array in ascending order
	sort.Ints(numbers)

	// Display the sorted array
	fmt.Println("Sorted array:", numbers)
}
```

In this example, we use the `sort.Ints()` function to sort the `numbers` array in place. The function modifies the original array, so be aware that the order of elements in the `numbers` array will change after the `sort.Ints()` call.

If you want to sort an array of a different data type or in descending order, you can use the `sort.Sort()` function with a custom `sort.Interface`. Here's an example of sorting a string array in descending order:

```go
package main

import (
	"fmt"
	"sort"
)

type ByLength []string

func (s ByLength) Len() int           { return len(s) }
func (s ByLength) Less(i, j int) bool { return len(s[i]) > len(s[j]) }
func (s ByLength) Swap(i, j int)      { s[i], s[j] = s[j], s[i] }

func main() {
	// Sample unsorted string array
	names := []string{"Alice", "Bob", "Charlie", "Eve", "David"}

	// Sorting the string array in descending order by length
	sort.Sort(ByLength(names))

	// Display the sorted array
	fmt.Println("Sorted array:", names)
}
```

In this example, we define a custom type `ByLength` that implements the `sort.Interface` interface with the required methods (`Len()`, `Less()`, and `Swap()`). We then use `sort.Sort(ByLength(names))` to sort the `names` array in descending order based on the length of the strings.

Remember that the `sort` package works with slices, not arrays directly. If you have an actual array that you want to sort, you can use a slice to refer to the array elements, as shown in the examples.