---
title: "[Javascript] 얕은 복사, 깊은 복사"
excerpt: Shallow copy, Deep copy
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-12T21:00:00'
last_modified_at: 2021-08-12T21:00:00
---

## 1. 얕은 복사(Shallow copy)

```javascript
const user = {
  name: 'LWW',
  age: 45,
  emails: ['abcdefg@gmail.com']
}
const copyUser = user
console.log(copyUser === user)  // true

// user 데이터를 수정했는데, copyUser 데이터도 같이 변경됨
user.age = 29
console.log('user', user)  // user {name: "LWW", age: 29, emails: Array(1)}
console.log('copyUser', copyUser)  // copyUser {name: "LWW", age: 29, emails: Array(1)}

user.emails.push('opqrstu@naver.com')
console.log(user.emails === copyUser.emails)  // true
```

<br>

```javascript
const user = {
  name: 'LWW',
  age: 45,
  emails: ['abcdefg@gmail.com']
}

// Object.assign(대상객체, 출처객체) 활용
const copyUser = Object.assign({}, user)
console.log(copyUser === user)  // false

user.age = 29
console.log('user', user)  // user {name: "LWW", age: 29, emails: Array(1)}
console.log('copyUser', copyUser)  // copyUser {name: "LWW", age: 45, emails: Array(1)}

user.emails.push('opqrstu@naver.com')
console.log(user.emails === copyUser.emails)  // true
```

<br>

```javascript
const user = {
  name: 'LWW',
  age: 45,
  emails: ['abcdefg@gmail.com']
}

// 전개 연산자 활용
const copyUser = {...user}
console.log(copyUser === user)  // false

user.age = 29
console.log('user', user)  // user {name: "LWW", age: 29, emails: Array(1)}
console.log('copyUser', copyUser)  // copyUser {name: "LWW", age: 45, emails: Array(1)}

user.emails.push('opqrstu@naver.com')
console.log(user.emails === copyUser.emails)  // true
```


<br>

## 2. 깊은 복사(Deep copy)

- 참조 데이터 내부에 또 다른 참조 데이터가 있는 경우 **_깊은 복사_** 고려

```javascript
const user = {
  name: 'LWW',
  age: 45,
  emails: ['abcdefg@gmail.com']
}
const copyUser = {...user}
console.log(copyUser === user)  // false

user.age = 29
console.log('user', user)  // user {name: "LWW", age: 29, emails: Array(1)}
console.log('copyUser', copyUser)  // copyUser {name: "LWW", age: 45, emails: Array(1)}

// 얕은 복사로는 속의 내용까지 복사되지 않음
user.emails.push('opqrstu@naver.com')
console.log(user.emails === copyUser.emails)  // true
console.log('user', user)  // user {name: "LWW", age: 29, emails: Array(2)}
console.log('copyUser', copyUser)  // copyUser {name: "LWW", age: 45, emails: Array(2)}
```

<br>

- 깊은 복사는 javascript로 직접 구현하기 복잡하기 때문에 lodash 패키지 활용

```bash
$ npm i lodash
$ npm run dev
```

<br>

```javascript
// lodash 패키지 import
import _ from 'lodash'

const user = {
  name: 'LWW',
  age: 45,
  emails: ['abcdefg@gmail.com']
}

// lodash 패키지의 깊은 복사 cloneDeep 메서드 사용
const copyUser = _.cloneDeep(user)
console.log(copyUser === user)  // false

user.age = 29
console.log('user', user)  // user {name: "LWW", age: 29, emails: Array(1)}
console.log('copyUser', copyUser)  // copyUser {name: "LWW", age: 45, emails: Array(1)}

user.emails.push('opqrstu@naver.com')
console.log(user.emails === copyUser.emails)  // false
console.log('user', user)  // user {name: "LWW", age: 29, emails: Array(2)}
console.log('copyUser', copyUser)  // copyUser {name: "LWW", age: 45, emails: Array(1)}
```

<br>

- 참고
- lodash 검색
- documentation 버튼 누름
- clone 검색


<br>

**결론!**  얕은복사 : Object.assign, 전개 연산자 사용 // 깊은복사 : lodash 패키지 사용
{: .notice--danger}