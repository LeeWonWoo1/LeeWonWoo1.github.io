---
title: "[Javascript] ECMA, Data type 확인"
excerpt: Parcel-Bundler와 lodash
categories:
- Javascript
tags:
- - Javascript
  - Node.js
  - NPM
  - Parcel
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-07T20:00:00'
last_modified_at: 2021-08-07T20:00:00
---

## 1. ECMA

- Javascript를 표준화 해주는 국제 표준화 기구 
- ES2015(ES6) 때 Javascript의 전성기가 시작됨
- Internet explorer 같은 구버전의 브라우저는 ES5버전 이하만 지원
- 바벨같은 플러그인의 도움을 받으면 ES6버전 이후의 최신 버전 기술들을 구형 브라우저에서도 동작할 수 있는 ES5버전대의 Javascript 문법으로 변환시켜 줄 수 있음


<br>

## 2. 연습용 프로젝트 초기화

```bash
npm init -y
npm i parcel-bundler -D
# scripts에 "dev": "parcel index.html"
# scripts에 "build": "parcel build index.html"
npm run dev
```


<br>

## 3. Data Type 확인

typeof : 특정한 데이터의 타입을 알아낼 수 있음

```javascript
console.log(typeof 'Hello World!');  // string
console.log(typeof 123);  // number
console.log(typeof true);  // boolean
console.log(typeof undefined);  // undefined
console.log(typeof null);  // object
console.log(typeof {});  // object
console.log(typeof []);  // object
```

데이터 타입을 확인할 때 typeof 키워드로는 객체데이터, 배열데이터를 확인할 수 없음

```javascript
function getType(data) {
  return Object.prototype.toString.call(data)
}

console.log(getType(123));  // [object Number]
console.log(getType(false));  // [object Boolean]
```

<br>

```javascript
function getType2(data) {
  return Object.prototype.toString.call(data).slice(8, -1);
}

console.log(getType(123));  // Number
console.log(getType(false));  // Boolean
console.log(typeof null);  // Null
console.log(typeof {});  // Object
console.log(typeof []);  // Array
```


<br>

사용한 함수를 다른 Javascript 파일에서도 사용하기 위해 함수를 사용할 파일에서 import

```javascript
// 내보내기 할 함수
export default function getType2(data) {
  return Object.prototype.toString.call(data).slice(8, -1);
}

// 함수를 사용할 파일
import getType2 from './getType'
```