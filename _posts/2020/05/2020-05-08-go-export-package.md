---
title: "Go Packages and Imports"

categories:
  - Posts
tags:
  - Go
---

# Go에서 export 하는 방법

Go에서 특정 함수나 변수를 export하는 방법은 해당 함수나 변수의 초성을 대분자로 적으면 됩니다.

```go

package something

import "fmt"

func sayBye() {
	fmt.Println("Bye")
}

func SayHello() {
	fmt.Println("Hello")
}

```

이렇게하면 다른 go 파일에서 해당 something 파일로 부터 `SayHello()` 함수를 불러올 수 있습니다.

```go

package main

import (
	"fmt"

	"github.com/parkchoongho/learngo/something"
)

func main() {
	fmt.Println("Hello World!")
	something.SayHello()
}

```

이런식으로 go에서는 외부 파일의 함수를 불러와서 실행할 수 있습니다.
