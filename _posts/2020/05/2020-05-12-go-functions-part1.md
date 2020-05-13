---
title: "Go Functions Part One"

categories:
  - Posts
tags:
  - Go
---

## Fucntions Part 1

Go에서는 함수를 다음과 같이 작성합니다.

```go
    func multiply(a int, b int) int {
        return a * b
    }
```

이렇게 argument와 return 값을 명시적으로 나타내야합니다. 위 코드를 아래와 같은 코드로 더 간편하게 나타낼 수 있습니다.

```go
    func myltiply(a, b int) int {
        return a * b
    }
```

Go는 특이하게 함수가 동시에 여러개의 값을 반환할 수 있습니다.

```go
  package main

  import(
    "fmt"
    "strings"
  )

  func lenAndUpper(name string)(int, string) {
    return len(name), strings.ToUpper(name)
  }

  func main() {
    totalLength, upperName := lenAndUpper("dd")
    fmt.Println(totalLength, upperName)
  }
```

들어오는 argument의 개수가 정해져 있지 않게 함수를 작성하고 싶은 경우 아래와 같이 `...` 을 활용합니다.

```go
func repeatMe(words ...string){
  fmt.Println(words)
}

func main(){
  repeatMe("DD", "Hi")
}
```
