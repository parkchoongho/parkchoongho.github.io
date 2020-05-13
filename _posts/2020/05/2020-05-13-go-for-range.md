---
title: "Go for, range, ..args"

categories:
  - Posts
tags:
  - Go
---

## Loop

GO에서는 오직 loop로 for문 만을 사용합니다.

```go
package main

import "fmt"

func superAdd(numbers ...int) int {
	for index, number := range numbers {
		fmt.Println(index, number)
	}
	for i := 0; i < len(numbers); i++ {
		fmt.Println(numbers[i])
	}
	total := 0

	for _, number := range numbers {
		total += number
	}

	return total
}

func main() {
	result := superAdd(1, 2, 3, 4, 5, 6)
	fmt.Println(result)
}
```
