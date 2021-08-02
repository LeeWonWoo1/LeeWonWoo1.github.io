---
title: "[Javascript] 변수, 함수"
excerpt: 데이터를 저장하고 참조하는 변수, 동작을 수행하는 코드인 함수
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-03T00:00:00'
last_modified_at: 2021-08-03T00:00:00
---

## 1. 변수

- 데이터를 저장하고 참조하는 데이터의 이름
- var, let, const


### - let

```javascript
// 재사용 가능
let a = 2;
let b = 5;

console.log(a + b);  // 7
console.log(a - b);  // -3
console.log(a * b);  // 10
console.log(a / b);  // 0.4
```

```javascript
// 값의 재할당 가능
let a = 12;
console.log(a);  // 12

a = 999;
console.log(a);  // 999
```


<br>

### - const

```javascript
// 값의 재할당 불가
const a = 12;
console.log(a);  // 12

a = 999;
console.log(a);  // TypeError: Assignment to constant variable
```


<br>

## 2. 함수

- 특정 동작을 수행하는 일부 코드의 집합

```javascript
// 함수 선언
function helloFunc() {
  // 실행 코드
  console.log('Hello');
}

// 함수 호출
helloFunc();  // Hello
```
<br>

```javascript
function returnFunc() {
  ruturn 777;
}

let a = returnFunc();
console.log(a);  // 777
```

<br>

```javascript
function sum(a, b) { // a, b는 매개변수(Parameters)
  return a + b;
}

// 재사용
let a = sum(1, 2);  // 1, 2는 인수(Arguments)
let b = sum(3, 4);
let c = sum(5, 6);

console.log(a, b, c);  // 3, 7, 11
```

<br>

```javascript
// 기명 함수
function hello() {
  console.log('Hello');
}

// 익명함수
let world = function () {
  console.log('World');
}

hello();  // Hello
world();  // World
```

<br>

```javascript
// 객체 데이터
const lww = {
  name: 'LWW',
  age: '50',
  // 메소드
  getName: function () {
    return this.name;
  }
};

const hisName = lww.getName();
console.log(hisName);  // LWW
// 혹은
console.log(lww.getName());  // LWW
```


<br>

## 3. 예약어

- 특별한 의미를 가지고 있어, 변수나 함수 이름 등으로 사용할 수 없는 단어
- break, case, catch, continue, default, delete, do, else, false, finally, for, function, if, in, instanceof, new, null, return, switch, this, throw, true, try, typeof, var, void, while, with, abstract, boolean, byte, char, class, const, debugger, double, enum, export, extends, final, float, goto, implements, import, int, interface, long, native, package, private, protected, public, short, static, super, synchronized, throws, transient, volatile, as, is, namespace, use, arguments, Array, Boolean, Date, decodeURI, decodeURIComponent, encodeURI, Error, escape, eval, EvalError, Function, Infinity, isFinite, isNaN, Math, NaN, Number, Object, parseFloat, parseInt, RangeError, ReferenceError, RegExp, String, SyntaxError, TypeError, undefined, unescape, URIError ...

```javascript
let this = 'Hello!';  // SyntaxError
let if = 123;  // SyntaxError
let break = true;  // SyntaxEr
```