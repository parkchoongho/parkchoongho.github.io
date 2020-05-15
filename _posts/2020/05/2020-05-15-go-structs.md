---
title: "Go Structs"

categories:
  - Posts
tags:
  - Go
---

Go는 maps말고도 Object와 유사한 다른 자료구조를 제공하는데 이를 `Struct`라 부릅니다.

```go
package main

import "fmt"

type person struct {
	name    string
	age     int
	favFood []string
}

func main() {
	// favFood := []string{"kimchi", "ramen"}
	// nico := person{"박충호", 29, favFood}
	// fmt.Println(nico)

	favFood := []string{"kimchi", "ramen"}
	nico := person{name: "박충호", age: 29, favFood: favFood}
	fmt.Println(nico)
}
```

maps와는 다르게 모든 value의 type을 미리 지정할 필요가 없습니다. 미리 선언하고 그에 맞는 값을 입력하면 됩니다.

주석처리된 코드와 아닌 코드를 보면 주석처리된 코드가 더 짧아 좋은 코드로 인식될 수 있으나 결과적으로 주석이 아닌 코드가 더 좋은 코드입니다. 왜냐하면 주석 처리된 코드는 해당 value가 어떤 key값과 매핑되는지 확인해야하지만 주석 처리가 안된 코드는 이를 명시적으로 알려주기 때문입니다. `Struct`를 작성할 때는 주석 처리가 안된 부분처럼 작성하는 연습을 해두면 좋습니다.
