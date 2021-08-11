---
title: "[Javascript] this"
excerpt: this
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-11T19:00:00'
last_modified_at: 2021-08-10T19:00:00
---

## this

- 일반 함수는 호출 위치에 따라 this 정의
- 화살표 함수는 자신이 선언된 함수 범위에서 this 정의

```javascript
const ww = {
  name: 'WW',
  // 일반 함수
  normal: function () {
    console.log(this.name)
  },
  // 화살표 함수
  arrow: () => {
    console.log(this.name)
  }
}

ww.normal()  // WW
ww.arrow()  // Undefined
```

<br>

```javascript
const kim = {
  name: 'Kim',
  normal: ww.normal,
  arrow: ww.arrow
}

kim.normal()  // Kim
kim.arrow()  // Undefined
```

<br>

```javascript
function User(name) {
  this.name = name
}
User.prototype.normal = function () {
  console.log(this.name)
}
User.prototype.arrow = () => {
  console.log(this.name)
}

const ww = new User('WW')

ww.normal()  // WW
ww.arrow()  // undefined
```

<br>

- setTimeout나 setInterval 함수를 사용할 때는 콜백으로 일반함수보다 화살표 함수를 쓰는 것이 활용도가 높음

```javascript
const timer = {
  name: 'LWW!!',
  timeout: function () {
     setTimeout(function () {
       console.log(this.name)
     }, 2000)
  }
}
timer.timeout()  // 2초 뒤 undefined
```

<br>

```javascript
const timer = {
  name: 'LWW!!',
  timeout: function () {
     setTimeout(() => {
       console.log(this.name)
     }, 2000)
  }
}
timer.timeout()  // 2초 뒤 LWW!!
```