---
title: "[Javascript] 자료형"
excerpt: String, Number, Boolean, Undefined, Null, Object, Array
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-01T15:00:00'
last_modified_at: 2021-08-01T15:00:00
---

## 1. String

```javascript
// 따옴표 사용
let myName = "LWW";
let email = "plmplmdnjsdn@naver.com";
let hello = `Hello ${myName}!`;

console.log(myName);  // LWW
console.log(email);  // plmplmdnjsdn@naver.com
console.log(hello);  // Hello LWW!
```


<br>

## 2. Number

```javascript
// 정수 및 부동소수점 숫자를 나타냄
let number = 123;
let opacity = 1.57;

console.log(number);  // 123
console.log(opacity);  // 1.57
```


<br>

## 3. Boolean

```javascript
// true, false 두 가지 값밖에 없는 논리 데이터
let checked = true;
let isShow = false;

console.log(checked);  // true
console.log(isShow);  // false
```


<br>

## 4. Undefined

```javascript
// 값이 할당되지 않은 상태를 나타냄
let undef;
let obj = {abc: 123};

console.log(undef);  // undefined
console.log(obj.abc);  // 123
console.log(obj.xyz);  // undefined
```


<br>

## 5. Null

```javascript
// 어떤 값이 의도적으로 비어있음을 의미
let empty = null;

console.log(empty);  // null
```


<br>

## 6. Object

```javascript
// 여러 데이터를 Key:Value 형태로 저장 { }
let user = {
  name: 'LWW',
  age: 50,
  isValid: true
};

console.log(user.name);  // LWW
console.log(user.age);  // 50
console.log(user.isValid);  // true
```


<br>

## 7. Array

```javascript
// 여러 데이터를 순차적으로 저장 [ ]
let animals = ['Cat', 'Dog', 'Tiger'];

console.log(animals[0]);  // 'Cat'
console.log(animals[1]);  // 'Dog'
console.log(animals[2]);  // 'Tiger'
```