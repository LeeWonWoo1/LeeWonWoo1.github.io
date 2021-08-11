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

### - String 메서드

자세한 내용은 string mdn 검색
{: .notice--info}

- 기호를 통해서 데이터를 손쉽게 선언하는 방식을 **_리터럴 방식_**이라고 함
- 리터럴 방식이 아니면 new라는 키워드를 사용해야 함

```javascript
// String.prototype.indexOf() -> 찾으려는 문자의 첫 번째 등장 index, 없으면 -1
const result1 = 'Hello world!!'.indexOf('world')
const result2 = 'Hello world!!'.indexOf('king')
console.log(result1)  // 6
console.log(result2)  // -1

const str = 'Hello world!!'
console.log(str.indexOf('king') !== -1)  // false

// length -> 문자열의 길이 반환
const str = '0123'
console.log(str.length)  // 4
console.log('0123'length)  // 4

// slice(x, y) -> 문자열을 인덱스 x부터 y-1까지 추출
const str = 'Hello world!'
console.log(str.slice(0, 3))  // Hel
console.log(str.slice(6, 11))  // world

// replace() -> 문자열 치환
const str = 'Hello world!'
console.log(str.replace('world', 'LWW'))  // Hell LWW!

const str = 'Hello world!'
console.log(str.replace(' world!', ''))  // Hello

// match() -> 정규표현식을 통해 특정한 문자를 match. 배열데이터로 반환
const str = 'emailaddress@gmail.com'
// 정규표현식
console.log(str.match(/.+(?=@)/)[0])  // emailaddress

// trim() -> 문자데이터의 앞뒤의 모든 공백문자 제거
const str = '      Hello world     '
console.log(str.trim())  // Hello world
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