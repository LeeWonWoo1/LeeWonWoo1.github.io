---
title: "[Bundler] Parcel"
excerpt: Bundler Parcel
categories:
- Bundler
tags:
- - Bundler
  - Web
  - Parcel
toc: true
toc_sticky: true
popular: true
date: '2021-08-26T20:00:00'
last_modified_at: 2021-08-26T20:00:00
---

## 1. Bundler 개요

- 웹에서는 HTML, CSS, Javascript가 동작
- 순수하게 HTML, CSS, Javascript로 코딩하는 것은 비효율적
- 따라서 다양한 기능들을 이용해 웹 개발을 하는데, 그것들은 웹에서 직접적으로 동작하지 않음
- 그것을 변환하는 과정을 거져 HTML, CSS, Javascript로 바꿔서 웹에서 동작시킴
- 즉, Vue.js, React, Sass 등을 Bundler를 통해 웹에서 동작시킬 수 있는 형태로 바꿀 수 있음
- Bundler 자체가 이해해서 변환해주는 것이 아니라 외부의 패키지의 도움을 받아 변환
- 수동의 작업을 Bundler에게 위임
- parcel : 구성 없는 단순한 자동 번들링, 소/중형 프로젝트에 적합
- webpack : 매우 꼼꼼한 구성, 중/대형 프로젝트에 적합


<br>

## 2. 프로젝트 시작

```bash
# 프로젝트 생성

$ mkdir parcel-template-basic
$ cd parcel-template-basic
$ npm init -y
$ npm i -D parcel-bundler
```

<br>

```json
// package.json

"scripts": {
  "dev": "parcel index.html",
  "build": "parcel build index.html"
}
```

<br>

```html
<!-- index.html -->

<head>
  <title>Parcel Bundler</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reset-css@5.0.1/reset.min.css">  <!-- reset.css cdn-->
  <link rel="stylesheet" href="./scss/main.scss">
  <script defer src="./js/main.js"></script>
</head>

<body>
  <h1>Hello Parcel!!</h1>
</body>
```

<br>

```scss
// scss/main.scss

$color--black: #000;
$color--white: #fff;

body {
  background-color: $color--black;
  h1 {
    color: $color--white;
  }
}
```

<br>

```js
// js/main.js

console.log('Hello Parcel!')
```

<br>

![parcel-start](https://user-images.githubusercontent.com/62803763/130954644-502bc6bd-9e08-4836-b9fa-9c69dc65a993.PNG)


<br>

## 3. 정적 파일 연결

ico converter
직접 삽입하는 파일을 dist 폴더에 넣는 방식은 좋지 않음
해당하는 파일을 개발서버를 열거나 제품화시킬때 dist폴더로 자동으로 넣어줄 수 있는 패키지의 도움을 받아야 함
parcel plugin static files copy