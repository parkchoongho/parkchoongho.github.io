---
title: "Go Variables and Constants"

categories:
  - Posts
tags:
  - Go
---

## 변수 선언 방법

Go에서는 크게 2가지 변수 선언 방법이 있습니다.

```go
    var name string = "Park Choong Ho"
```

더 간편하게 선언할 수도 있습니다.

```go
    name := "Park Choong Ho"
```

Go는 변수가 처음 선언됐을 때를 기준으로 타입을 설정합니다. 예를 들어,

```go
    name := "Park Choong Ho"
    name = true
```

이렇게 코드를 작성할 경우 에러가 발생합니다. 왜냐하면 name은 맨 처음 선언되면서 string으로 타입이 지정되었기 때문에 boolean 타입을 할당할 수 없습니다.

## 상수 선언 방법

Go 에서는 다음과 같이 상수를 선언합니다.

```go
    const name = "Park Choong Ho"
```
