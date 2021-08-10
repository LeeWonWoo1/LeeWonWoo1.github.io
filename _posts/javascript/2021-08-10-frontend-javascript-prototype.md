---
title: "[Javascript] Prototype"
excerpt: 생성자 함수 Prototype
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-10T17:00:00'
last_modified_at: 2021-08-10T17:00:00
---

## Prototype

- 객체가 만들어지기 위해 그 객체의 모태가 되는 것

```javascript
// 생성자로 new라는 키워드와 같이 사용되는 함수를 Parcal case로 작성
function User(first, last) {
  this.firstName = first
  this.lastName = last
}

// 객체가 여러개 생기더라도 getFullName 함수는 메모리에 1번만 만들어짐
// constructor와 __proto__ 속성을 가짐
User.prototype.getFullName = function () {
  return `${this.firstName} ${this.lastName}`
}

// user : 생성자 함수
// ww, kim, park : 인스턴스
const ww = new User('WW', 'L')
const kim = new User('ChulSoo', 'Kim')
const park = new User('Younghee', 'Park')

console.log(ww.getFullName())  // WW L
console.log(kim.getFullName())  // ChulSoo Kim
console.log(park.getFullName())  // Younghee Park
```