---
title: "[Typescript] Typescript Types"
excerpt: Typescript types
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
date: '2021-08-18T21:00:00'
last_modified_at: 2021-08-18T21:00:00
---

## 1. Type Annotation

```ts
// 타입 에러
let a = "Amy";
a = 39;  // Error

// a의 타입을 string로 지정
let a: string;

a = "Amy";
a = 39;  // Error

// a의 타입을 number로 지정
let a: number;

a = "Amy";  // Error
a = 39;

// 함수 내의 type annotation
function hello(b: number) {
  
}
hello(39);
hello('Amy');  // Error
```


<br>

## 2. Typescript Types vs Javascript Types

- Typescript : Static Types(개발 중간에 타입 체크)
- Javascript : Dynamic Types(runtime에 들어가야 체크)

```js
// Javascript

function add(n1, n2) {
  // runtime에서 에러 체크
  if (typeof n1 !== 'number' || typeof n2 !== 'number') {
    throw new Error('Incorrect input!');
  }
  return n1 + n2;
}

const result = add(10, 20);
```

<br>

```ts
// Typescript

// 개발중에 체크
function add(n1: number, n2: number) {
  return n1 + n2;
}

const result = add(10, 20);
```

<br>

- Typescript에서 제공하는 데이터 타입
- Javascript 기본 자료형 포함(superset)
    - ECMAScript 표준에 따른 기본 자료형(6가지)
    - Boolean
    - Number
    - String
    - Null
    - Undefined
    - Symbol(ECMAScript 6에 추가)
    - Array: object형
- 프로그래밍을 도울 몇가지 타입 추가 제공
    - Any, Void, Never, Unknown
    - Enum
    - Tuple: object형


<br>

## 3. Primitive Types

- 오브젝트와 레퍼런스 형태가 아닌 실제 값을 저장하는 자료형
- Primitive 형의 내장 함수를 사용 가능한 것은 Javascript 처리 방식 덕분
- Primitive types은 모두 **_소문자_**
- ES2015 기준 6가지
    - boolean
    - number
    - string
    - symbol
    - null
    - undefined
- literal 값으로 Primitive 타입의 서브 타입을 나타낼 수 있음
- wrapper 객체로 만들 수 있음

```ts
// 내장함수 사용 가능
let name = 'Amy';
name.toString();

// literal 값으로 Primitive 타입의 서브 타입 표시
true;
'hello';
3.14;
null;
undefined;

// wrapper 객체(Typescript에서는 권장하지 않음)
new Boolean(false);  // typeof new Boolean(false) : 'object'
new String('world');  // typeof new String('world') : 'object'
new Number(29);  // typeof new Number(29) : 'object'
```


<br>

## 4. Boolean / boolean

```ts
// boolean.ts

let isDone: boolean = false;
isDone = true;
console.log(typeof isDone)  // boolean
console.log(isDone);  // true

let isOk: Boolean = true;
isOk = false;
console.log(typeof isOk);  // boolean
console.log(isOk);  // false

let isNotOk: boolean = new Boolean(true);  // Error
```

<br>

```bash
$ nxp tsc
$ node boolean.js  # boolean
```


<br>

## 5. Number / number

- Javascript와 같이 Typescript의 모든 숫자는 부동 소수점 값
- 10진수 및 16진수 외에도, ECMAScript 2015에 도입된 2진수 및 8진수 지원
- NaN
- 1_000_000과 같은 표기 가능

```ts
// 10진수 리터럴
let decimal: number = 7;

// 16진수 리터럴
let hex: number = 0xf00e;

// 2진수 리터럴
let binary: number = 0b1100;

// 8진수 리터럴
let octal: number = 0o732;

// NaN
let notANumber: number = NaN;

// 밑줄 표기
let underscoreNum: number = 1_000_000;
```