---
title:  "Annotations With Functions and Objects"

categories:
  - Posts
tags:
  - Typescript
---

# Annotations With Functions & Objects

## More on Annotations Around Functions

![Functions](/assets/images/2020/02/functions.PNG)

이번에는 functions에 대한 annotations를 살펴보겠습니다. 그전에 우리는 변수에다 annotaion을 적용했습니다.

```typescript
const logNumber: (i: number) => void = (i: number) => {
    console.log(i);
}
```

조금 다르게 함수에 직접 annotaion을 달아보겠습니다.

```typescript
const add = (a: number, b: number): number => {
  return a + b;
};
```

## Inference Around Functions

Function Inference는 Annotations와 다르게 return하는 값만 취급합니다. 또한, typescript는 함수안에 logic에 대해서는 전혀 신경쓰지 않습니다. 오로지 type에만 신경씁니다.

```typescript
const add = (a: number, b: number): number => {
  return a + b;
};
```

argument가 각각 어떤 type을 가지는지는 annotation으로 명시해야합니다. (`a: number, b: number`)

![Function-Inference](/assets/images/2020/02/function-inference.PNG)

왜냐하면 function inference는 argument를 고려하지 않기 때문입니다. 오직 return하는 값만 고려합니다. 따라서 아래와 같이 코드를 작성해도 됩니다. (하지만 annotation을 명시하는 것이 좋습니다.)

```typescript
const add = (a: number, b: number) => {
  return a + b;
};
```

## Annotations for Anonymous Functions

```typescript
function divide(a: number, b: number): number {
  return a / b;
}

const mulitiply = function(a: number, b: number): number {
  return a * b;
};
```

## Void and Never

아무런 값도 return하지 않는 함수도 있습니다.

```typescript
const logger = (message: string): void => {
  console.log(message);
};
```

이 경우 type은 void입니다.

```typescript
const throwError = (message: string): never => {
  throw new Error(message);
};
```

에러가 발생하고 아무런 값도 return 하지 않는 경우에는 never라 칭합니다.

## Destructuring with Annotations

```typescript
const todayWeather = {
  date: new Date(),
  weather: "sunny"
};

const logWeather = (forecast: { date: Date; weather: string }): void => {
  console.log(forecast.date);
  console.log(forecast.weather);
};

logWeather(todayWeather);
```

```typescript
const todayWeather = {
  date: new Date(),
  weather: "sunny"
};

const logWeather = ({date, weather}: { date: Date; weather: string }): void => {
  console.log(date);
  console.log(weather);
};

logWeather(todayWeather);
```

## Annotations Around Objects

```typescript
const profile = {
  name: "alex",
  age: 20,
  coords: {
    lat: 0,
    lng: 15
  },
  setAge(age: number): void {
    this.age = age;
  }
};

const { age } = profile;
const { age }: { age: number } = profile;

const { coords: { lat, lng } } = profile;
const { coords: { lat, lng } }: { coords: { lat: number; lng: number } }= profile;
```

