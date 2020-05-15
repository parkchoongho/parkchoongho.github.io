---
title: "Go Pointers"

categories:
  - Posts
tags:
  - Go
---

Go는 주소값을 저장하는 pointer 기능을 제공합니다.

```go
    a := 2
	b := &a
	a = 5
	fmt.Println(*b)
```

결과값으로 _5_ 가 나타납니다. `*` 표시는 해당 주소를 참조한다는 의미입니다. b에 a의 주소값을 저장하고 그 주소가 있는 메모리를 `*`를 활용하여 참조하였습니다.
`*`를 사용하여 해당 주소의 값을 변경할 수도 있습니다.

```go
    a := 2
	b := &a
	*b = 5
	fmt.Println(a)
```

위 결과도 *5*가 나타납니다. 이처럼 go는 pointer라는 저수준 단계의 프로그래밍을 지원합니다.
