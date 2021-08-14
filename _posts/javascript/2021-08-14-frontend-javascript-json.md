---
title: "[Javascript] Json"
excerpt: JavaScript Object Notation
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
  - Json
toc: true
toc_sticky: true
popular: true
date: '2021-08-14T18:00:00'
last_modified_at: 2021-08-14T18:00:00
---

## Json

- Javascript의 데이터를 표현하는 하나의 포맷
- 속성-값 쌍
- AJAX 통신을 위해, XML을 대체하는 주요 데이터 포맷


### - 자료형

- Number
- String(큰따옴표만 허용)
- Boolean
- Array
- Object
- null


### - 문법

```json
//myData.json

{
  "string": "LWW",
  "number": 123,
  "boolean": true,
  "null": null,
  "object": {},
  "array": []
  // "undefined": undefined -> 에러
}
```

<br>

```javascript
// main.js

import myData from './myData.json'

console.log(myData)  // {string: "LWW", number: 123, boolean: true, ...}

const user = {
  name: 'LWW',
  age: 45,
  emails: [
    'abcdefg@gmail.com',
    'opqrstu@naver.com'
  ],
  // javascript에서 속성 이름을 따옴표로 묶어줄 수 있음
  // javascript에서 속성 이름에 특수기호가 들어가는 경우 따옴표로 묶어줌
  // 'companyName@#^@#*$': {}
  // json 문법은 속성을 큰따옴표로 묶어주어야 함
}

console.log('user', user)  // user {name: "LWW", age: 45, emails: Array(2)}

// json 파일은 하나의 문자 데이터
// stringify -> 데이터를 문자 데이터화 시킴
const str = JSON.stringify(user)
console.log('str', str)  // str {"name":"LWW","age":45,"emails":[abcdefg@...]}
console.log(typeof str)  // string

// 실제 javascript 데이터처럼 출력
// parse -> 문자 데이터를 javascript 데이터처럼 변경
const obj = JSON.parse(str)
console.log('obj', obj)  // obj {string: "LWW", number: 123, boolean: true, ...}
```
