---
title: "[Typescript] Generics"
excerpt: Typescript Generics
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
date: '2021-08-24T01:00:00'
last_modified_at: 2021-08-24T01:00:00
---

## 1. Generics와 Any의 차이점

- Any는 들어오는 input에 대해 다른 타이핑을 할 수 없음
- Generics은 타입으로 된 연산이 함수 내에서 가능하게 함

```bash
# 프로젝트 생성

$ mkdir ts-generic
$ cd ts-generic
$ npm init -y
$ npm i typescript -D
$ npx tsc --init
```

<br>

```ts
// generic1.ts

// 많은 반복된 함수들
function helloString(message: string): string {
  return message;
}

function helloNumber(message: number): number {
  return message;
}


//---------------------------------------------------------
// any
function hello(message: any): any {
  return message;
}

console.log(hello('LWW').length);  // 3
console.log(hello(29).length);  // undefined


//---------------------------------------------------------
// generic
function helloGeneric<T>(message: T): T {
  return message;
}

console.log(helloGeneric('LWW').length);  // 3
console.log(helloGeneric(29).length);  // Error!
console.log(helloGeneric(true));  // true
```


<br>

## 2. Generics Basic

```ts
// generic2.ts

function helloBasic1<T>(message: T): T {
  return message;
}

// 방법1 -> 지정
helloBasic1<string>('LWW');
helloBasic1<string>(10);  // Error!

// 방법2 -> 추론
helloBasic1(36);


//---------------------------------------------------------
function helloBasic2<T, U>(message: T, comment: U): T {
  return message;
}

helloBasic2<string, number>('LWW', 29);
helloBasic2(10, 20);
```


<br>

## 3. Generics Array & Tuple

```ts
// generic3.ts

// Array
function helloArray<T>(message: T[]): T {
  return message[0];
}

helloArray(['Hello', 'World']);  // string
helloArray(['Hello', 5]);  // string | number


//---------------------------------------------------------
// Tuple
function helloTuple<T, K>(message: [T, K]): T {
  return message[0];
}

helloTuple(['Hello', 'World']);  // string
helloTuple(['Hello', 5]);  // string
```


<br>

## 4. Generics Function

```ts
// generic4.ts

// type alias
type HelloFunctionGeneric1 = <T>(message: T) => T;

const helloFunction1: HelloFunctionGeneric1 = <T>(message: T): T => {
  return message;
};


//---------------------------------------------------------
// interface
interface HelloFunctionGeneric2 {
  <T>(message: T): T
}

const helloFunction2: HelloFunctionGeneric2 = <T>(message: T): T => {
  return message;
};
```


<br>

## 5. Generics Class

```ts
// generic5.ts

class Person<T, K> {
  private _name: T;
  private _age: K;

  constructor(name: T, age: K) {
    this._name = name;
    this._age = age;
  }
}

new Person('LWW', 29);
new Person<string, number>('Tom', 'haha');  // Error!
```


<br>

## 6. Generics with extends

- Type을 제한하는 용도로 사용

```ts
// generic6.ts

class PersonExtends<T extends string | number> {
  private _name: T;

  constructor(name: T) {
    this._name = name;
  }
}

new PersonExtends('LWW');
new PersonExtends(29);
new PersonExtends(true);  // Error!
```


<br>

## 7. keyof & type lookup system

```ts
// generics.ts

interface IPerson {
  name: string;
  age: number;
}

const person: IPerson = {
  name: 'LWW',
  age: 29,
};

// get
function getProp1(obj: IPerson, key: "name" | "age"): string | number {
  return obj[key];  // 에러는 없지만 문제가 발생할 가능성 있음
}
// IPerson[keyof IPerson] 
// => IPerson["name" | "age"] 
// => IPerson["name"] | IPerson["age"]
// => string | number
function getProp2(obj: IPerson, key: keyof IPerson): IPerson[keyof IPerson] {
  return obj[key];
}
function getProp3<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

getProp3(person, 'name');
getProp3(person, 'age');


//---------------------------------------------------------
// set
function setProp1(obj: IPerson, key: "name" | "age", value: string | number): void {
  obj[key] = value;  // Error!
}

function setProp2<T, K extends keyof T>(obj: T, key: K, value: T[K]): void {
  obj[key] = value;
}

setProp2(person, "name", "Tom");
```