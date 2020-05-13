---
title: "Go Functions Part Two"

categories:
  - Posts
tags:
  - Go
---

## Functions Part 2

naked return이라는 재밌는 기능을 Go에서는 제공합니다.
naked return이란, return할 변수를 명시하지 않아도 되는 것을 의미합니다. 아래와 같이 사용합니다.

```go
func lenAndUpper(name string) (length int, uppercase string) {
	length = len(name)
	uppercase = strings.ToUpper(name)
	return
}

func main() {
	totalLength, upperName := lenAndUpper("dd")
	fmt.Println(totalLength, upperName)
}
```

이미 `(length int, uppercase string)` 에 어떤 값을 반환할지 명시했기에 `return` 뒤에 변수를 작성하지 않아도 됩니다.
참고로 `(length int, uppercase string)` 이렇게 작성하는 동시에 변수가 선언되기에 `length = len(name)` 처럼 할당할 수 있습니다.

다음은 defer라는 기능입니다. defer는 함수가 종료 된 후 (실행 후) 추가적으로 무엇인가를 동작할 수 있게 하는 기능입니다.

```go

package main

import (
	"fmt"
	"strings"
)

func lenAndUpper(name string) (length int, uppercase string) {
	defer fmt.Println("I'm done")
	length = len(name)
	uppercase = strings.ToUpper(name)
	return
}

func main() {
	totalLength, upperName := lenAndUpper("dd")
	fmt.Println(totalLength, upperName)
}
```

이렇게 코드를 작성하고 실행하면 아래와 같은 결과가 나타납니다.

```powershell
$ go run main.go
I'm done
2 DD
```

함수가 종료된 후에 `I'm done` 을 출력하게 끔 defer를 설정했기에 위와 같은 결과가 나타났습니다.
이런 defer는 이미지나 비디오 업로드 후 프로그램이 실행해야 될 다음 일을 명시하는데 굉장히 유용합니다.
