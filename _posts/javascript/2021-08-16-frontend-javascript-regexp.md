---
title: "[Javascript] 정규표현식 프로젝트-1"
excerpt: 정규표현식 개요 및 프로젝트 시작
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