---
title: "Go Arrays and Slices"

categories:
  - Posts
tags:
  - Go
---

Go에서는 아래와 같이 배열을 코딩합니다.

```go
package main

import "fmt"

func main() {
	array는 크기가 정해져 있는 배열, 배열 크기를 제한하지 않고 싶자면 slice를 사용
	names := [5]string{"nico", "lynn", "dal"}
	names[3] = "lalala"
	fmt.Println(names)
}
```

배열의 크기가 정해져 있다면 위와 같이 코드를 작성하면 됩니다. Go에서 배열은 크기가 정해져 있습니다. 그런데 만약 크기가 알 수 없고 동적으로 변한다면 어떻게 할까요? 그럴때 사용하는 것이 바로 `Slice`입니다.

```go
package main

import "fmt"

func main() {
	names := []string{"nico", "lynn", "dal"}
	names[3] = "lalala"
	fmt.Println(names)
}
```

배열에서 숫자가 들어간 부분을 지우면 slice가 됩니다. 만약 slice에 값을 추가하고 싶다면 어떻게 해야할까요? 위 방법처럼 배열에 값을 집어넣는 것과 동일한 방법을 쓰면 에러가 발생합니다.
slice에 값을 집어넣으려면 `append`라는 함수를 활용합니다.

```go
package main

import "fmt"

func main() {
	names := []string{"nico", "lynn", "dal"}
	names = append(names, "lalala")
	fmt.Println(names)
}
```

append는 names을 수정하지 않고 새로운 변수가 추가된 slice를 반환합니다. 반환된 slice를 names에 다시 할당하는 방식으로 slice에 값을 추가했습니다.
