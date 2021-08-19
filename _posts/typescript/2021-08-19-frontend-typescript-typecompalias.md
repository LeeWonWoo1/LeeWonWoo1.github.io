---
title: "[Typescript] 타입 호환성, 별칭"
excerpt: Type Compatibility, Type Alias
categories:
- Typescript
tags:
- - Typescript
  - Programming
  - Web
  - NPM
toc: true
toc_sticky: true
popular: true
date: '2021-08-19T19:00:00'
last_modified_at: 2021-08-19T19:00:00
---

## 1. 타입 호환성(Type Compatibility)

- 공변 : 같거나 서브 타입인 경우, 할당이 가능
- 반병 : 함수의 매개변수 타입만 같거나 슈퍼타입인 경우, 할당이 가능

```ts
// 서브 타입

// sub1 타입은 sup1 타입의 서브 타입
let sub1: 1 = 1;
let sup1: number = sub1;
sub1 = sup1;  // error! Type 'number' is not assignable to type '1'


// ----------------------------------------------------------
// sub2 타입은 sup2 타입의 서브 타입
let sub2: number[] = [1];
let sup2: object = sub2;
sub2 = sup2;  // error! Type '{}' is missing the following properties from ... 


// ----------------------------------------------------------
// sub3 타입은 sup3 타입의 서브 타입
let sub3: [number, number] = [1, 2];
let sup3: number[] = sub3;
sub3 = sup3;  // error! Type 'number[]' is not assignable to type '[number, number]'


// ----------------------------------------------------------
// sub4 타입은 sup4 타입의 서브 타입
let sub4: number = 1;
let sup4: any = sub4;
sub4 = sup4;


// ----------------------------------------------------------
// sub5 타입은 sup5 타입의 서브 타입
let sub5: never = 0 as never;
let sup5: number = sub5;
sub5 = sup5;  // error! Type 'number' is not assignable to type 'never'


// ----------------------------------------------------------
// sub6 타입은 sup6 타입의 서브 타입
class Animal {}
class Dog extends Animal {
  eat() {}
}

let sub6: Dog = new Dog();
let sup6: Animal = sub6;
sub6 = sup6;  // error! Property 'eat' is missing in type 'SubAnimal' but ...
```

<br>

```ts
// 공변

// primitive type
let sub7: string = '';
let sup7: string | number = sub7;


// ----------------------------------------------------------
// object -> 각각의 프로퍼티가 대응하는 프로퍼티와 같거나 서브타입이어야 함
let sub8: { a: string; b: number } = { a: '', b: 1 };
let sup8: { a: string | number; b: number } = sub8;


// ----------------------------------------------------------
// array -> object와 마찬가지
let sub9: Array<{ a: string; b: number }> = [{ a: '', b: 1 }];
let sup9: Array<{ a: string | number; b: number }> = sub9;
```

<br>

```ts
// 반병

class Person {}
class Developer extends Person {
  coding() {}
}
class StartupDeveloper extends Developer {
  burning() {}
}

function tellme(f: (d: Developer) => Developer) {}

// Developer => Developer에 Developer => Developer를 할당하는 경우
tellme(function dToD(d: Developer): Developer {
  return new Developer();
});

// Developer => Developer에 Person => Developer를 할당하는 경우
tellme(function pToD(d: Person): Developer {
  return new Developer();
});

// Developer => Developer에 StartupDeveloper => Developer를 할당하는 경우
// strictFunctionTypes 옵션을 켜면 함수 할당 시 매개변수 타입이 같거나
// 슈퍼타입인 경우가 아닌 경우, 에러를 통해 경고
tellme(function sToD(d: StartupDeveloper): Developer {
  return new Developer();
});
```


<br>

## 2. 타입 별칭(Type Alias)

- Interface랑 비슷
- Primitive, Union Type, Tuple, Function
- 기타 직접 작성해야하는 타입을 다른 이름을 지정할 수 있음
- 만들어진 타입의 refer로 사용하는 것
- 타입을 만드는 것은 아님
- 타입이 타입으로서의 목적이 명확하면 Interface, 그렇지 않다면 Type Alias 사용

```ts
// Aliasing Primitive
// 별 의미가 없음
type MyStringType = string;
const str = 'world';
let myStr: MyStringType = 'hello';

myStr = str;


// ------------------------------------------
// Aliasing Union Type
// Union Type은 A도 가능하고 B도 가능한 타입
// 길게 쓰는걸 짧게해주고, 반복을 줄여줌
let person: string | number = 0;
person = 'LWW';

type StringOrNumber = string | number;
let another: StringOrNumber = 0;
another = 'Tom';


// ------------------------------------------
// Aliasing Tuple
// 튜플 타입에 별칭을 줘서 여러군데서 사용할 수 있게 함
let person: [string, number] = ['LWW', 29];
type PersonTuple = [string, number];
let another: PersonTuple = ['Tom', 24];


// ------------------------------------------
// Aliasing Function
type EatType = (food: string) => void;
```