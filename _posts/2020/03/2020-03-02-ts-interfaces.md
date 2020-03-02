---
title:  "Typed Interfaces"

categories:
  - Posts
tags:
  - Typescript
---

# Interfaces

이번에는 Interface에 대해 알아보도록 하겠습니다.

![Interfaces](/assets/images/2020/03/Interfaces.PNG)

![Interfaces and Classes](/assets/images/2020/03/inter-class.PNG)

## Long Type Annotations

지금까지 우리가 배워온 것으로 코드를 작성하겠습니다.

```typescript
const oldCivic = {
  name: "civic",
  year: 2000,
  broken: true
};

const printVehicle = (vehicle: {
  name: string;
  year: number;
  broken: boolean;
}): void => {
  console.log(`Name: ${vehicle.name}`);
  console.log(`Year: ${vehicle.year}`);
  console.log(`Broken: ${vehicle.broken}`);
};
```

vehicle을 설명하는 annotation을 보면 vehicle parameter에 대한 설명이 적혀있는데 길고 읽기 힘들게 되어있습니다. 이 읽기 힘든 annotation 코드를 interface로 대체해보도록 하겠습니다.

## Fixing Long Annotations with Interfaces

![Definition of Interfaces](/assets/images/2020/03/def-inter.PNG)

인터페이스란 특정 객체의 property가 가지는 type을 묘사하는 custom type입니다. 우리가 스스로 만드는 type이라 보시면 됩니다.

```typescript
interface Vehicle {
  name: string;
  year: number;
  broken: boolean;
}

const oldCivic = {
  name: "civic",
  year: 2000,
  broken: true
};

const printVehicle = (vehicle: Vehicle): void => {
  console.log(`Name: ${vehicle.name}`);
  console.log(`Year: ${vehicle.year}`);
  console.log(`Broken: ${vehicle.broken}`);
};
```

이렇게 하면 printVehicle 함수의 argument로 Vehicle interface처럼 name은 string, year은 number, broken은 boolean type을 가지는 객체가 와야합니다.

## Syntax Around Interfaces

interface의 property로는 primitive type외에 함수도 올 수 있습니다.

```typescript
interface Vehicle {
  name: string;
  year: Date;
  broken: boolean;
  summary(): string;
}

const oldCivic = {
  name: "civic",
  year: new Date(),
  broken: true,
  summary(): string {
    return `Name: ${this.name}`;
  }
};

const printVehicle = (vehicle: Vehicle): void => {
  console.log(vehicle.summary());
};

printVehicle(oldCivic);
```

```powershell
$ ts-node .\interfaces.ts
Name: civic
```

## Functions in Interfaces

방금 작성한 코드를 보도록 하겠습니다.

```typescript
interface Vehicle {
  name: string;
  year: Date;
  broken: boolean;
  summary(): string;
}

const oldCivic = {
  name: "civic",
  year: new Date(),
  broken: true,
  summary(): string {
    return `Name: ${this.name}`;
  }
};

const printVehicle = (vehicle: Vehicle): void => {
  console.log(vehicle.summary());
};

printVehicle(oldCivic);
```

printVehicle 함수를 보면 vehicle의 summary property만을 사용하는 것을 확인할 수 있습니다. Vehicle interface에서 property는 중요해보이지 않는군요. 다른 property들을 지우고 코드를 돌려보겠습니다.

```typescript
interface Vehicle {
  summary(): string;
}

const oldCivic = {
  name: "civic",
  year: new Date(),
  broken: true,
  summary(): string {
    return `Name: ${this.name}`;
  }
};

const printVehicle = (vehicle: Vehicle): void => {
  console.log(vehicle.summary());
};

printVehicle(oldCivic);
```

```powershell
$ ts-node .\interfaces.ts
Name: civic
```

에러없이 잘 작동하는 것을 보실 수 있습니다. 이말은 Vehicle annotation은 해당 property가 있고 type을 만족하는 지만 확인한다는 것입니다. oldCivic 객체가 다른 property를 가지고 있는냐 없느냐를 따지지 않는다는 의미입니다.

## Code Reuse with Interfaces

```typescript
interface Reportable {
  summary(): string;
}

const oldCivic = {
  name: "civic",
  year: new Date(),
  broken: true,
  summary(): string {
    return `Name: ${this.name}`;
  }
};

const drink = {
  color: "brown",
  carbonated: true,
  sugar: 40,
  summary(): string {
    return `My drink has ${this.sugar} grams of sugar`;
  }
};

const printSummary = (item: Reportable): void => {
  console.log(item.summary());
};

printSummary(oldCivic);
printSummary(drink)
```

위 코드를 보면 drink 객체를 추가한 것을 확인할 수 있습니다. drink 객체는 oldCivic 객체처럼 string을 반환하는 summary property를 가지고 있습니다. 따라서 둘다 Reportable type을 만족시킵니다. 따라서 위 코드를 돌리면 올바르게 작동합니다.

여기서 의미하는 것은 하나의 interface로 다른 object의 다른 property가 올바르게 동작하는지 제어할 수 있다는 점입니다.

![General Plan Interfaces](/assets/images/2020/03/general-plan-inter.PNG)

![Reusable Interfaces](/assets/images/2020/03/reusable-inter.PNG)