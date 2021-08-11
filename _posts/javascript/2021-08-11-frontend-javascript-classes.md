---
title: "[Javascript] ES6 Classes"
excerpt: ES6 Classes
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-11T20:00:00'
last_modified_at: 2021-08-10T20:00:00
---

## 1. function 축약

- 객체 데이터 내부에서 일반함수를 사용할 때 function 축약 가능

```javascript
const ww = {
  name: 'WW',
  normal: function () {
    console.log(this.name)
  }
}

// 축약형
const ww = {
  name: 'WW',
  normal() {
    console.log(this.name)
  }
}
```


<br>

## 2. ES6 Classes

- 클래스 만들기 편리함

```javascript
function User(first, last) {
  this.firstName = first
  this.lastName = last
}
User.prototype.getFullName = function () {
  return `${this.firstName} ${this.lastName}`
}

const ww = new User('WW', 'Lee')
const kim = new User('Chulsoo', 'Kim')
const park = new User('Younghee', 'Park')

console.log(ww)
console.log(kim.getFullName())
console.log(park.getFullName())
```


<br>

```javascript
class User {
  constructor(first, last) {
    this.firstName = first
    this.lastName = last
  }
  getFullName() {
    return `${this.firstName} ${this.lastName}`
  }
}
```