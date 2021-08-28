---
title: "[Typescript] Interface"
excerpt: Typescript Interface
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
date: '2021-08-21T21:00:00'
last_modified_at: 2021-08-21T21:00:00
---

## 1. 인터페이스란?

- Javascript에는 존재하지 않는 개념
- Typescript 파일에서 작성하고 컴파일해도 Javascript 파일에는 반영되지 않음
- 어떤 객체가 특정 Property, Method를 가진다고 선언하는 것
- 타입 체크를 위해 사용
- 타입을 만들어내는 방식
- 외부적으로 드러나는 객체의 사용 방식이 적혀있음

```bash
# 프로젝트 생성

$ mkdir type-interface
$ cd type-interface
$ npm init -y
$ npm i typescript -D
$ npx tsc --init
```

<br>

```ts
// interface1.ts

interface Person1 {
  name: string;
  age: number;
}

function hello1(person: Person1): void {
  console.log(`안녕하세요! ${person.name} 입니다.`);
}

const p1: Person1 = {
  name: "LWW",
  age: 29,
};

hello1(p1);  // 안녕하세요! LWW 입니다.
```


<br>

## 2. Optional Property

```ts
// interface2.ts

interface Person2 {
  name: string;
  age?: number;  // ? -> 있어도되고 없어도 됨
}

function hello2(person: Person2): void {
  console.log(`안녕하세요 ${person.name} 입니다. ${person.age}살 입니다.`);
}

hello2({name: 'LWW', age: 29});  // 안녕하세요! LWW 입니다. 29살 입니다.
hello2({name: 'Tom'});  // // 안녕하세요! Tom 입니다. undefined살 입니다.
```

<br>

```ts
// interface3.ts

interface Person3 {
  name: string;
  age?: number;
  [index: string]: any;  // 어떤 이름의 property가 와도 괜찮음
}

function hello3(person: Person3): void {
  console.log(`안녕하세요! ${person.name} 입니다.`);
}

const p31: Person3 = {
  name: "LWW",
  age: 29,
};

const p32: Person3 = {
  name: "Tom",
  systers: ["Kim", "Park"],
};

const p33: Person3 = {
  name: "Amy",
  father: p31,
  mother: p32,
};

hello3(p31)  // 안녕하세요! LWW 입니다.
hello3(p32)  // 안녕하세요! Tom 입니다.
hello3(p33)  // 안녕하세요! Amy 입니다.
```


<br>

## 3. Function in Interface

- Interface 안에 Function을 정의하는 방법

```ts
// interface4.ts

interface Person4 {
  name: string;
  age: number;
  hello(): void;
}

// 방법1
const p41: Person4 = {
  name: 'LWW',
  age: 29,
  hello: function (): void {
    console.log(`안녕하세요! ${this.name} 입니다.`);
  },
};

// 방법2
const p42: Person4 = {
  name: 'LWW',
  age: 29,
  hello(): void {
    console.log(`안녕하세요! ${this.name} 입니다.`);
  },
};

// 방법3
const p43: Person4 = {
  name: 'LWW',
  age: 29,
  hello(this: Person4): void {
    console.log(`안녕하세요! ${this.name} 입니다.`);
  },
};

p41.hello();  // 안녕하세요! LWW 입니다.
p42.hello();  // 안녕하세요! LWW 입니다.
p43.hello();  // 안녕하세요! LWW 입니다.
```


<br>

## 4. Class Implements Interface

- Interface를 이용해 Class를 만들어내는 방법

```ts
// interface5.ts

interface IPerson1 {
  name: string;
  age?: number;
  hello(): void;
}

class Person implements IPerson1 {
  name: string;
  age?: number | undefined;

  constructor(name: string) {
    this.name = name;
  }

  hello(): void {
    console.log(`안녕하세요! ${this.name} 입니다.`);
  }
}

const person: IPerson1 = new Person("LWW");
person.hello();  // 안녕하세요! LWW 입니다.
```


<br>

## 5. Interface extends Interface

- Interface를 상속하는 방법

```ts
// interface6.ts

interface IPerson2 {
  name: string;
  age?: number;
}

interface IKorean extends IPerson2 {
  city: string;
}

const k: IKorean = {
  name: "LWW",
  // age: 29,
  city: "서울",
};

HTMLDivElement
```


<br>

## 6. Function Interface

- Function을 Interface로 만드는 방법

```ts
// interface7.ts

interface HelloPerson {
  (name: string, age?: number): void;
}

// Error! 'age' 및 'age' 매개변수의 형식이 호환되지 않습니다.
const helloPerson: HelloPerson = function (name: string, age: number) {
  console.log(`안녕하세요! ${name} 입니다.`);
};

const helloPerson: HelloPerson = function (name: string) {
  console.log(`안녕하세요! ${name} 입니다.`);
};

helloPerson('LWW', 29);
```


<br>

## 7. Readonly Interface Property

- Interface의 Property에 Readonly 키워드를 사용하는 방법

```ts
interface Person8 {
  name: string;
  age?: number;
  readonly gender: string;
}

const p81: Person8 = {
  name: 'LWW',
  gender: 'male',
};

p81.gender = 'female';  // Error! 읽기 전용 속성이므로 'gender'에 할당할 수 없음
```


<br>

## 8. Type alias vs Interface

- Type alias는 어떤 타입을 부르는 이름
- Interface는 새로운 타입을 만들어 내는 것 

```ts
// Function

// type alias
type EatType = (food: string) => void;

// interface
interface IEat {
  (food: string): void;
}


// ------------------------------------
// Array

// type alias
type PersonList = string[];

// interface
interface IPersonList {
  [index: number]: string;
}


// ------------------------------------
// Intersection

interface ErrorHandling {
  success: boolean;
  error?: {message: string};
}

interface ArtistsData {
  artists: {name: string}[];
}

// type alias
type ArtistsResponseType = ArtistsData & ErrorHandling;

let art: ArtistsResponseType;

// interface
interface IArtistsResponse extends ArtistsData, ErrorHandling {}

let iar: IArtistsResponse;


// ------------------------------------
// Union types

interface Bird {
  fly(): void;
  layEggs(): void;
}

interface Fish {
  swim(): void;
  layEggs(): void;
}

type PetType = Bird | Fish;

interface IPet extends PetType {}  // Error! TS2312: An interface can only extend ...
class Pet implements PetType {}  // Error! TS2422: A class can only implement ...


// ------------------------------------
// Declaration Merging - Interface

// interface
interface MergingInterface {
  a: string;
}

interface MergingInterface {
  b: string;
}

let mi: MergingInterface;
mi.  // a
     // b

// type alias
type MergingType = {
  a: string;
};

type MergingType = {  // Error! Duplicate identifier 'MergingType'.
  b: string;
};
```