---
title: "[Javascript] 연산자"
excerpt: 산술, 할당, 비교, 논리, 삼항 연산자
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-08T21:00:00'
last_modified_at: 2021-08-08T21:00:00
---

## 1. 산술 연산자

```javascript
console.log(1 + 2);  // 3
console.log(5 - 7);  // -2
console.log(3 * 4);  // 12
console.log(10 / 2);  // 5
console.log(7 % 5);  // 2
```


<br>

## 2. 할당 연산자

```javascript
let a = 2;
a += 1;  // a = a + 1
console.log(a);  // 3
```


<br>

## 3. 비교 연산자

```javascript
a === b  // 서로 같음
a !== b // 서로 다름
a < b  // a < b
a <= b  // a <= b
a > b  // a > b
a >= b  // a >= b
```


<br>

## 4. 논리 연산자

```javascript
a && b  // a and b
a || b  // a or b
!a  // not a
```


<br>

## 5. 삼항 연산자

```javascript
console.log(a ? '참' : '거짓');  // true면 앞, false면 뒤
```


<br>

## 6. 동등 연산자

- 대부분의 경우 비교 연산자 '===' 을 사용
- 서로 다른 값이 의도하지 않게 '같다'라고 출력되는 것을 방지

```javascript
const a = 1;
const b = '1';

console.log(a === b);  // false
console.log(a == b);  // true
```