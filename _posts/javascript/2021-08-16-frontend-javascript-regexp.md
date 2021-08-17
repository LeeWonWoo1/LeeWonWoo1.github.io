---
title: "[Javascript] 정규표현식 생성"
excerpt: 정규표현식 개요 및 생성
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
  - Reg
toc: true
toc_sticky: true
popular: true
date: '2021-08-16T21:00:00'
last_modified_at: 2021-08-16T21:00:00
---

## 1. 프로젝트 시작

```bash
# terminal

$ npm init -y
$ npm i parcel-bundler -D
```

- index.html 파일 생성
- main.js 파일 생성
- README.md 파일 생성

```json
// package.json

"scripts": {
  "dev": "parcel index.html",
  "build": "parcel build index.html"
},
```

<br>

```bash
# 개발서버 열기

$ npm run dev

# 개발서버가 버전문제로 실행되지 않는다면 다른버전 설치
$ npm i parcel-bundler@버전 -D
```

<br>

```html
<!-- index.html -->

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script src="./main.js"></script>
</head>

<body>
  <h1>Hello RegExp</h1>
</body>
```

<br>

```javascript
// main.js

console.log(123)
```


<br>

## 2. 정규표현식

- 문자열을 검색하고 대체하는 데 사용 가능한 형식 언어(패턴)
- 간단한 문자 검색부터 이메일, 패스워드 검사 등의 문자 일치 기능등을 수행
- 정규표현식 역할
    - 문자 검색(Search)
    - 문자 대체(replace)
    - 문자 추출(extract)
- 정규표현식 테스트 사이트
    - [https://regex101.com/](https://regex101.com/)
    - [https://regexr.com/](https://regexr.com/)
    - [https://regexper.com/](https://regexper.com/)


### - Javascript 정규식 생성

#### @ 생성자 함수 방식

- RegExp 생성자 함수를 호출하여 사용할 수 있음

```js
// new RegExg(표현식)
const regexp1 = new RegExp("^abc");

// new RegExg(표현식, 플래그)
const regexp2 = new RegExp("^abc", "gi");

new RegExp('표현', '옵션')
new RegExp('[a-z]', 'gi')
```

<br>

```js
// main.js

const str = `
010-1234-5678
theabc@gmail.com
https://www.omdbapi.com/?apikey=5f6c9466&s=frozen
The quick brown fox jumps over the lazy dog.
abbcccdddd
`

const regexp = new RegExp('the', '')
console.log(str.match(regexp))  // ["the", index: 15, input: "\n010-1234-5678\ntheabc@..."]

// 대소문자 구분 -> g 옵션
const regexp = new RegExp('the', 'g')
console.log(str.match(regexp)  // (2) ["the", "the"]

// 대소문자 구분X -> gi 옵션
const regexp = new RegExp('the', 'gi')
console.log(str.match(regexp)  // (3) ["the", "The", "the"]
```

<br>

#### @ Literal 방식

```js
// /표현식/
const regexp1 = /^abc/;

// /표현식/플래그
const regexp2 = /^abc/gi;

/표현/옵션
/[a-z]/gi
```

<br>

```js
const regexp = /the/gi
console.log(str.match(regexp)  // (3) ["the", "The", "the"]
```