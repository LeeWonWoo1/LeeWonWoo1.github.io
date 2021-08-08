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

### - 변수 유효범위

let, const : 블록 레벨의 유효범위
var : 함수 레벨의 유효범위

```javascript
// const, let
function scope() {
  if (true) {
    const a = 123;
    console.log(a);  // 블록 내부
  }
}
scope();  // 123;

// const, let
function scope() {
  if (true) {
    console.log(a);  // 블록 내부
    const a = 123;
  }
}
scope();  // undefined

// const, let
function scope() {
  if (true) {
    const a = 123;
  }
  console.log(a);  // 함수 내부
}
scope();  // ReferenceError: a is not defined

// const, let
function scope() {
  console.log(a);  // 함수 내부
  if (true) {
    const a = 123;
  }
}
scope();  // ReferenceError: a is not defined
```


<br>

```javascript
// var
function scope() {
  if (true) {
    const a = 123;
    console.log(a);  // 블록 내부
  }
}
scope();  // 123

// var
function scope() {
  if (true) {
    console.log(a);  // 블록 내부
    const a = 123;
  }
}
scope();  // undefined

// var
function scope() {
  if (true) {
    const a = 123;
  }
  console.log(a);  // 함수 내부
}
scope();  // 123

// var
function scope() {
  console.log(a);  // 함수 내부
  if (true) {
    const a = 123;
  }
}
scope();  // undefined
```

- var은 의도하지 않은 범위에서 변수가 사용될 수 있음
- 그만큼 메모리를 차지하고, 결국 개발자가 확인하지 못하는 메모리 누수로 발전할 수 있음
- 즉 let과 const를 사용해 블록레벨의 유효범위를 만들어 주는 것이 관리하기 효과적


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

### - 화살표 함수

```javascript
// () => {}  vs  function () {}

//기존 함수
const double = function (x) {
  return x * 2;
}
console.log('double: ', double(7));  // double: 14

// 화살표 함수
const doubleArrow = x => x * 2;  // 축약 가능
console.log('doubleArrow', doubleArrow(7));  // doubleArrow 14

// 화살표 함수가 객체 데이터를 return 할 때
const doubleArrow = x => ({ name: 'LWW' })
console.log('doubleArrow', doubleArrow(7))  // {name: "LWW"}
```


<br>

### - 즉시 실행 함수(IIFE)

```javascript
// 한번 사용하고 쓸일이 없는 함수의 경우 이름을 지정해 줄 필요가 없음
// 함수를 만들자마자 바로 동작 실행

const a = 5;
function double() {
  console.log(a * 2);
}
double();  // 10

// IIFE
(function () {
  console.log(a * 2)
})();  // 10

// IIFE(더 권장되는 방법)
(function () {
  console.log(a * 2)
}());  // 10
```


<br>

### - 호이스팅(Hoisting)

```javascript
// 함수 선언부가 유효범위 최상단으로 끌어올려지는 현상

const a = 5;

double();  // TypeError: double is not a function

const double = function () {
  console.log(a * 2);
}
```


<br>

```javascript
// 호이스팅 발생

const a = 5;

double();  // 10

function double() {
  console.log(a * 2);
}
```


<br>

### - 타이머 함수

- setTimeout(함수, 시간) : 일정 시간 후 함수 실행
- setInterval(함수, 시간) : 시간 간격마다 함수 실행
- clearTimeout() : 설정된 Timeout 함수를 종료
- clearInterval() : 설정된 Interval 함수를 종료

```javascript
// setTimeout

setTimeout(function () {
  console.log('LWW!');  // 2초 뒤 LWW!
}, 2000);

// 화살표 함수
setTimeout(() => {
  console.log('LWW!'); // 2초 뒤 LWW!
}, 2000);
```


<br>

```javascript
// clearTimeout

// h1 태그를 클릭하면 timer함수를 종료
const h1El = document.querySelector('h1')
h1El.addEventListener('click', () => {
  clearTimeout(timer);
});
```


<br>

```javascript
// setInterval

const timer = setInterval(() => {
  console.log('LWW!');  // 2초에 한번 LWW!
}, 2000);
```


<br>

```javascript
// clearInterval

// h1 태그를 클릭하면 interval함수를 종료
const h1El = document.querySelector('h1')
h1El.addEventListener('click', () => {
  clearTimeout(timer);
});
```

## 3. 예약어

- 특별한 의미를 가지고 있어, 변수나 함수 이름 등으로 사용할 수 없는 단어
- break, case, catch, continue, default, delete, do, else, false, finally, for, function, if, in, instanceof, new, null, return, switch, this, throw, true, try, typeof, var, void, while, with, abstract, boolean, byte, char, class, const, debugger, double, enum, export, extends, final, float, goto, implements, import, int, interface, long, native, package, private, protected, public, short, static, super, synchronized, throws, transient, volatile, as, is, namespace, use, arguments, Array, Boolean, Date, decodeURI, decodeURIComponent, encodeURI, Error, escape, eval, EvalError, Function, Infinity, isFinite, isNaN, Math, NaN, Number, Object, parseFloat, parseInt, RangeError, ReferenceError, RegExp, String, SyntaxError, TypeError, undefined, unescape, URIError ...

```javascript
let this = 'Hello!';  // SyntaxError
let if = 123;  // SyntaxError
let break = true;  // SyntaxEr
```