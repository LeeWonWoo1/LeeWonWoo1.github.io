---
title: "[Typescript] 코드 바라보기"
excerpt: 작성자 관점, 사용자 관점
categories:
- Typescript
tags:
- - Typescript
  - Programming
  - Web
  - Node.js
toc: true
toc_sticky: true
popular: true
date: '2021-08-19T18:00:00'
last_modified_at: 2021-08-19T18:00:00
---

## 1. 작성자와 사용자 관점에서 코드 바라보기

- 타입이란 해당 변수가 할 수 있는 일을 결정
- Javascript는 함수 사용법에 대한 오해를 야기

```js
// Javascript

// f1 이라는 함수의 body에서는 a를 사용
// a가 할 수 있는 일은 a의 타입이 결정
function f1(a) {
  return a;
}

// -----------------------------------------------------------
// f2 실행의 결과가 NaN을 의도한 것이 아니라면
// 함수의 작성자는 a가 number 타입이라는 가정으로 함수를 작성
function f2(a) {
  return a * 20;
}

// 사용자는 사용법을 숙지하지 않고, 문자열을 사용해 함수 실행
console.log(f2(10));  // 200
console.log(f2('LWW'));  // NaN
```

<br>

- noImplicitAny 옵션을 켜면 타입을 명시적으로 지정하지 않은 경우, Typescript가 추론 중 'any'라고 판단하게 되면, 컴파일 에러를 발생시켜 명시적으로 지정하도록 유도
- strictNullChecks 옵션을 켜면 모든 타입에 자동으로 포함되어 있는 null과 undefined를 제거
- noImplicitReturns 옵션을 켜면 함수 내 모든 코드가 값을 리턴하지 않으면, 컴파일 에러 발생

```ts
// Typescript
// Typescript의 추론에 의지하는 경우

// a의 타입을 명시적으로 지정하지 않아 a는 any로 추론됨
// 함수의 return 타입은 number로 추론됨
function f3(a) {
  return a * 20;
}

// 사용자는 a가 any이기 때문에, 사용법에 맞게 문자열을 사용해 함수 실행
console.log(f3(10));  // 200
console.log(f3('LWW') + 10)  // NaN


// -----------------------------------------------------------
// noImplicitAny에 의한 방어
function f3(a) {
  return a * 20;  // error TS7006: Parameter 'a' implicitly has an 'any' type
}

// 코드를 실행할 수 없음. 컴파일이 정상적으로 마무리 될 수 있도록 수정 필요
console.log(f3(10));
console.log(f3('LWW') + 10)


// -----------------------------------------------------------
// number 타입으로 추론된 return 타입
// 매개변수의 타입은 명시적으로 지정
// 명시적으로 지정하지 않은 함수의 리턴 타입은 number로 추론됨
// noImplicitAny 옵션 킴
function f4(a: number) {
  if (a > 0) {
    return a * 20;
  }
}

// 사용자는 사용법에 맞게 number형을 사용하여 함수를 실행
// 함수의 리턴 타입은 number이기 때문에, 타입에 따르면 연산을 바로 할 수 있음
// 하지만 실제 undefined + 5가 실행되어 NaN이 출력
console.log(f4(5));  // 100
console.log(f4(-5) + 5)  // NaN


// -----------------------------------------------------------
// number | undefined 타입으로 추론된 return 타입
// 매개변수의 타입은 명시적으로 지정
// 명시적으로 지정하지 않은 함수의 리턴 타입은 number | undefined로 추론됨
// strictNullChecks 옵션 킴
function f4(a: number) {
  if (a > 0) {
    return a * 20;
  }
}

// 사용자는 사용법에 맞게 number형을 사용하여 함수를 실행
// 함수의 리턴 타입은 number | undefined이기 때문에, 타입에 따르면 연산을 바로 할 수 없음
// 컴파일 에러를 고쳐야 하기 때문에 사용자와 작성자가 의논을 해야 함
console.log(f4(5));
console.log(f4(-5) + 5);  // error TS2532: Object is possibly 'undefined'


// -----------------------------------------------------------
// return 타입을 명시적으로 지정
// 매개변수의 타입과 함수의 return 타입을 명시적으로 지정
// 실제 함수 구현부의 return 타입과 명시적으로 지정한 타입이 일치하지 않아 컴파일 에러 발생
function f5(a: number): number {
  if (a > 0) {
    return a * 20;  // error TS2366: Function lacks ending return statement and ...
  }
}


// -----------------------------------------------------------
// 모든 코드에서 리턴을 직접해야함
// if가 아닌 경우 return을 직접 하지 않고 코드가 종료됨
// noImplicitReturns 옵션 킴
function f5(a: number) {
  if (a > 0) {
    return a * 20;  // error TS7030: Not all code paths return a value
  }
}
```

<br>

```js
// Javascript

// 매개변수에 object가 들어오는 경우
function f6(a) {
  return `이름은 ${a.name} 이고, 나이는 ${Math.floor(a.age / 10) * 10}대 입니다.`;
}

console.log(f6({name: 'LWW', age: 29}));  // 이름은 LWW 이고, 나이는 20대 입니다.
console.log(f6('LWW'));  // 이름은 undefined 이고, 나이는 NaN대 입니다.
```

<br>

```ts
// Typescript

// object literal type
function f7(a: {name: string, age: number}) : string {
  return `이름은 ${a.name} 이고, 나이는 ${Math.floor(a.age / 10) * 10}대 입니다.`;
}

console.log(f7({name: 'LWW', age: 29}));  // 이름은 LWW 이고, 나이는 20대 입니다.
console.log(f7('LWW'));  // error TS2345: Argument of type 'string' is not assignable ...
```


<br>

## 2. 나만의 타입을 만드는 방법

```ts
// interface
interface PersonInterface {
  name: string;
  age: number;
}

// typealias
type PersonTypeAlias = {
  name: string;
  age: number;
}

// class
function f8(a: PersonInterface): string {
  return `이름은 ${a.name} 이고, 나이는 ${Math.floor(a.age / 10) * 10}대 입니다.`;
}

console.log(f8({name: 'LWW', age: 29}));  // 이름은 LWW 이고, 나이는 20대 입니다.
console.log(f8('LWW'));  // error TS2345: Argument of type 'string' is not assignable ...
```


<br>

## 3. Structural Type System vs Nominal Type System

- Structural Type System : 구조가 같으면, 같은 타입(Typescript)
- Nominal Type System : 구조가 같아도 이름이 다르면, 다른 타입(Java)
- Duck Typing : 어떤 새가 오리처럼 걷고, 헤엄치고, 꽥꽥거리면 오리라고 부름(Python)

```ts
// Structural Type System
// Typescript

interface IPerson {
  name: string;
  age: number;
  speak(): string;
}

type PersonType = {
  name: string;
  age: number;
  speak(): string;
};

let personInterface: IPerson = {} as any;
let personType: PersonType = {} as any;

personInterface = personType;
personType = personInterface;
```

<br>

```java
// Nominal Type System
// Java

type PersonID = string & { readonly brand: unique symbol };
function PersonID(id: stirng): PersonID {
  return id as PersonID;
}

function getPersonById(id: PersonID) {}

getPersonById(PersonID('id-abcdefg'));
getPersonById('id-abcdefg');  // error TS2345: Argument of type 'string' is not ...
```

<br>

```python
# Duck Typing
# Python

class Duck:
  def sound(self) :
    print u"꽥꽥"

class Dog:
  def sound(self) :
    print u"멍멍"

def get_sound(animal) :
  animal.sound()

def main() :
  bird = Duck()
  dog = Dog()
  get_sound(bird)
  get_sound(dog)
```