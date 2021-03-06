---
title: "[Javascript] 데이터 불변성"
excerpt: Immutability
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-12T20:00:00'
last_modified_at: 2021-08-12T21:00:00
---

## 데이터 불변성(Immutability)


### - 원시 데이터

- 원시 데이터 : String, Number, Boolean, undefined, null
- 새로운 원시 데이터를 사용했을 때, 그 데이터가 기존의 메모리 주소에 들어있다면 새로운 메모리에 만드는 것이 아니라 기존에 존재하는 메모리 주소를 바라보도록 만들어 줌
- 즉 원시 데이터는 새롭게 만들어지지 않고 불변함

```javascript
let a = 1
let b = 4

// ----------------------------------
// |1: 1     |2: 4    |3: 7    |4: 
// ----------------------------------

console.log(a, b, a === b)  // 1 4 false

// 1번 메모리의 주소를 b에게 할당
b = a
console.log(a, b, a === b)  // 1 1 true

// a가 3번 메모리 주소를 가리킴
a = 7
console.log(a, b, a === b)  // 7 1 false

// c가 4번 메모리 주소에 들어가지 않고, 1번 메모리 주소 가리킴
let c = 1
console.log(b, c, b === c)  // 1 1 true
```

<br>

### - 참조형 데이터

- 참조형 데이터 : Object, Array, Function
- 참조형 데이터는 모양이 같아도 같은 데이터가 아닐수도 있음
- 참조형 데이터는 새로운 값을 만들 때마다 새로운 메모리 주소에 할당
- 즉 참조형 데이터는 불변하는 개념이 아님(가변)
- a라는 변수와 b라는 변수를 구분해서 사용하고 싶다면 **_복사_**를 사용

```javascript
let a = { k: 1 }
let b = { k: 1 }

// ---------------------------
// |1: {K: 1}     |2: {k: 1}  
// ---------------------------

console.log(a, b, a === b)  // {k: 1} {k: 1} false

// ---------------------------
// |1: {K: 7}     |2: {k: 1}   
// ---------------------------

a.k = 7
b = a
console.log(a, b, a === b)  // {K: 7} {k: 7} true

// ---------------------------
// |1: {K: 2}     |2: {k: 1}   
// ---------------------------

// a와 b가 같은 메모리를 바라보고 있기 때문에 a의 값만 수정해도
// b의 값까지 같이 수정됨 (주의!)
a.k = 2
console.log(a, b, a === b)  // {k: 2} {k: 2} true

// ---------------------------
// |1: {K: 2}     |2: {k: 1}   
// ---------------------------

// b가 가리키는 1번 메모리 주소를 c에 할당
let c = b
console.log(a, b, c, a === c)  // {k: 2} {k: 2} {k: 2} true

// ---------------------------
// |1: {K: 9}     |2: {k: 1}   
// ---------------------------

a.k = 9
console.log(a, b, c, a === c)  // {k: 9} {k: 9} {k: 9} true
```

**결론!**  참조형 데이터를 관리할 때, 할당 연산자를 사용하면 의도치 않은 문제를 발생시킬 수 있기 때문에, 의도한 것이 아니라면 **_복사_**라는 개념을 통해서 두 변수를 실제 메모리 상에서 분리해 주어야 함
{: .notice--danger}