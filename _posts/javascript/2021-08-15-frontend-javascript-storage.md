---
title: "[Javascript] Storage"
excerpt: Local Storage, Session Storage
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
  - Json
  - Storage
toc: true
toc_sticky: true
popular: true
date: '2021-08-15T22:00:00'
last_modified_at: 2021-08-15T22:00:00
---

## Local Storage

자세한 내용은 **local storage mdn** 검색
{: .notice--notice}

- 개발자 도구 Application 탭을 통해 확인
- 데이터가 만료되지 않음 (반영구적)
- 데이터를 문자 데이터로 저장하는 것을 권고

```javascript
const user = {
  name: 'LWW',
  age: 45,
  emails: [
    'abcdefg@gmail.com',
    'opqrstu@naver.com'
  ]
}

// 문자 데이터로 변환해서 저장해야 함
localStorage.setItem('user', user)  // Key: user, Value: [object Object]

// 문자 데이터로 변환
JSON.stringify('user', JSON.stringify(user))  // Key: user, Value: {"name":"LWW","age":...}
console.log(localStorage.getItem('user'))  // {"name":"LWW","age":45,"emails":["abc...]}

// 객체 데이터로 변환
console.log(JSON.parse(localStorage.getItem('user')))  // {name: "LWW", age: 45, emails: Array(2)}

// 데이터 삭제
localStorage.removeItem('user')


// 데이터 가져옴
const str = localStorage.getItem('user')
const obj = JSON.parse(str)

// 데이터 수정
obj.age = 29
console.log(obj)  // {name: "LWW", age: 29, emails: Array(2)}

// 데이터 저장
localStorage.setItem('user', JSON.stringify(obj))  // Key: user, Value: {"name":"LWW","age":29,...}
```


- 위의 방법은 매우 원시적
- 따라서 **Lowdb** 사용
- lodash 패키지의 기능을 사용해서 Local Storage를 하나의 DB처럼 쉽게 관리해 줄 수 있음