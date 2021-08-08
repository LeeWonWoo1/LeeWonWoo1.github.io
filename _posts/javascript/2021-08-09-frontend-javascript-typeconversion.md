---
title: "[Javascript] 형 변환"
excerpt: 참 같은 값 Truthy, 거짓 같은 값 Falsy
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-09T01:00:00'
last_modified_at: 2021-08-09T01:00:00
---

## 형 변환


### - Truthy

```javascript
// Truthy(참 같은 값)
// true, 1, 2, {}, [], 'false', -17 '4.14' ...

if (true) {
  console.log(123);  // 123
}

if ('false') {
  console.log(123);  // 123
}
```


<br>

### - Falsy

```javascript
// Falsy(거짓 같은 값)
// false, null, undefined, 0, '', -0, NaN

if (false) {
  console.log(123);  // 출력되지 않음
}

if (undefined) {
  console.log(123);  // 출력되지 않음
}

if (0) {
  console.log(123);  // 출력되지 않음
}
```
