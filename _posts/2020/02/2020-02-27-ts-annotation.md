---
title:  "Type Annotation & Inference"

categories:
  - Posts
tags:
  - Typescript
---

# Type Annotations

## Annotations and Inference

Type Annotations은 한 변수가 어떤 타입의 값을 가질 것인지 Typescript에게 알려주는 코드입니다.

Type inference는 하나의 변수가 어떤 타입의 값을 가리키는지를 Typescript가 파악하는 것을 의미합니다.

![annotations-inference](/assets/images/2020/02/annotations-inference.PNG)

어떻게 보면 이 두개의 용어는 호환될 수 있는 말입니다. 실제 코드를 작성하면서 예시를 살펴보겠습니다.

![exchange-type](/assets/images/2020/02/exchange-type.PNG)

```typescript
let apples: number = 5;
let speed: string = "fast";
let hasName: boolean = true;

let nothingMuch: null = null;
let nothing: undefined = undefined;

// built in objects
let now: Date = new Date();
```

`: number` 이 코드는 annotation입니다. apples라는 변수가 number라는 타입을 가져야된다고 타입스크립트에 알려주는 코드입니다.

## Object Literal Annotations

```typescript
// Array
let colors: string[] = ["red", "green", "blue"];
let myNumbers: number[] = [1, 2, 3];
let truths: boolean[] = [true, false, true];

// Classes
class Car {}
let car: Car = new Car();

// Object Literal
let point: { x: number; y: number } = {
  x: 10,
  y: 20
};
```

## Annotations Around Functions

함수의 경우에는 어떤 type의 argument를 input으로 받느냐 그리고 어떤 type의 데이터를 output으로 리턴하느냐를 나타냅니다.

```typescript
// Function
const logNumber: (i: number) => void = (i: number) => {
  console.log(i);
};
```

## Inference

```typescript
let apples = 5;
let speed = "fast";
let hasName = true;
```

Typescript는 이렇게 annotation을 입력하지 않아도 정상적으로 작동합니다. `let apples = 5;` 코드를 보면 typescript는 자동으로 type inference를 사용하여 apples라는 변수의 type이 number임을 인식합니다.

![Type Inference](/assets/images/2020/02/type-inference.PNG)

위 그림처럼 한줄에 코드를 작성하면 typescript는 type inference를 사용하지만 변수 선언과 초기화를 따로 해주면 type inference를 사용하지 않고 `any` 로 표시됩니다. any는 다음에 알아보도록 하겠습니다.

![When to use](/assets/images/2020/02/when-to-use-annotation.PNG)

그렇다면 typescript는 type inference를 자동으로 사용하는데 왜 type annotation이 있는 걸까요? 3가지 경우가 있는데 다음시간부터 하나씩 살펴보도록 하겠습니다.

## The 'Any' Type

먼저 any부터 보도록하겠습니다.

```typescript
// Function that returns the 'any' type

const json = '{"x": 10, "y": 20}';
const coordinates = JSON.parse(json);

console.log(coordinates); // {x: 10, y: 20}
```

coordinates 변수를 hover하면 `coordinates: any` 라고 뜨는 것을 확인할 수 있습니다. any는 무엇일까요?

![JSON Parse](/assets/images/2020/02/json-parse.PNG)

json은 위에 보시는 것처럼 `''`로 둘러쌓여 있습니다. 이를 parsing하면 그 안에 있는 실제 값이 나타납니다. 따라서 실질적으로 우리는 string 값을 주는 것이고 그 결과로 어떤 것이 나올지 알 수 없습니다. (string안에 어떤 결과가 있느냐에 따라 달라지기 때문입니다.) 따라서 이를 하나로 그 어떤 값도 올 수 있다 해서 `any` 로 표현합니다. 엄밀히 얘기하자면 any는 어떤 경우에서도 허용해서는 안됩니다. 어떤 변수가 any라는 말은 typescript가 해당변수가 어떤 type을 가지는지 파악하지 못한 것을 의미하기 때문입니다. 따라서 annotaion을 활용해 typescript가 해당 변수가 어떤 type을 취하는지 명시해야 합니다.

```typescript
const json = '{"x": 10, "y": 20}';
const coordinates: { x: number; y: number } = JSON.parse(json);

console.log(coordinates);
```

## Delayed Initialization

변수 선언을 먼저하고 나중에 initialization을 하는 경우도 annotation을 명시합니다. 개발을 하다보면 변수를 먼저 선언하고 값 할당은 나중에 하는 경우가 있습니다.

```typescript
// When we declare a variable on one line
// and initialize it later
let words = ["red", "green", "blue"];
let foundWord;

for (let i = 0; i < words.length; i++) {
  if (words[i] === "red") {
    foundWord = true;
  }
}
```

하지만 이렇게 한다면 typescript가 foundWord가 어떤 type을 가지는지 알 수 없어 any로 표시됩니다. 따라서 이 경우 annotation을 더해서 명시합니다.

```typescript
// When we declare a variable on one line
// and initialize it later
let words = ["red", "green", "blue"];
let foundWord: boolean;

for (let i = 0; i < words.length; i++) {
  if (words[i] === "red") {
    foundWord = true;
  }
}
```

## When Inference Doesn't Work

선언과 초기화를 같이 해도 Inference가 작동하지 않는 경우가 있습니다.

```typescript
// Varaible whose type cannot be inferred correctly
let numbers = [-10, -1, 12];
let numberAboveZero = false;

for (let i = 0; i < numbers.length; i++) {
  if (numbers[i] > 0) {
    numberAboveZero = numbers[i];
  }
}
```

이 경우 numberAboveZero 변수에 boolean을 할당하고 그 다음 numbers array에 0보다 큰 숫자가 있으면 그 숫자를 할당하는 코드를 작성했습니다. 하지만 inference에 의해 numberAboveZero 변수에는 boolean만이 할당될 수 있으므로 경고 메세지가 뜹니다. 우리 코드의 의도를 typescript가 이해하지 못하는 것입니다. 이 경우 `|` (or) 연산자를 활용하여 annotation 합니다.

```typescript
// Varaible whose type cannot be inferred correctly
let numbers = [-10, -1, 12];
let numberAboveZero: boolean | number = false;

for (let i = 0; i < numbers.length; i++) {
  if (numbers[i] > 0) {
    numberAboveZero = numbers[i];
  }
}
```

이렇게 코드를 작성하면 numberAboveZero는 두가지 type을 가질 수 있는 변수가 됩니다. 사실 이런 코드는 그다지 좋지 못한 코드입니다. 하지만 annotation을 사용하는 상황을 이해하고자 이렇게 작성했습니다. 앞으로 다양한 상황에 맞는 코드를 작성하면서 이 부분에 대해 공부해보도록 하겠습니다.