---
title: "[Javascript] 구조 분해 할당"
excerpt: Destructuring assignment 비구조화 할당
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-12T02:00:00'
last_modified_at: 2021-08-12T02:00:00
---

## 구조 분해 할당

- 객체 데이터에서 내용을 구조 분해 해서 원하는 속성들만 꺼내서 사용

```javascript
// 객체 데이터
const user = {
  name: 'LWW',
  age: 45,
  email: 'abcdefg@gmail.com'
}
const { name = 'abc', age, address = 'Korea' } = user

console.log(`사용자의 이름은 ${name}입니다.`)  // 사용자의 이름은 LWW입니다.
console.log(`${name}의 나이는 ${age}세 입니다.`)  // LWW의 나이는 45세 입니다.
// LWW의 이메일 주소는 abcdefg@gmail.com입니다.
console.log(`${name}의 이메일 주소는 ${user.email}입니다.`)  
console.log(address)  // Korea
```

<br>

```javascript
// 배열 데이터
const animals = ['Cat', 'Dog', 'Tiger']
const [a, b, c, d] = animals
console.log(a, b, c, d)  // Cat Dog Tiger undefined

const[, b] = animals
console.log(b)  // Dog
```