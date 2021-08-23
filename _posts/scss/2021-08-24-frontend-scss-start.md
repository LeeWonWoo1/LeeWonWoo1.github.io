---
title: "[SCSS] SCSS 속성 - 정렬, 전환, 변환"
excerpt: SCSS 속성인 정렬, 전환, 변환 정리
categories:
- SCSS
tags:
- - SASS
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-24T02:00:00'
last_modified_at: 2021-08-24T02:00:00
---

## 1. SCSS

- css를 쉽게 사용하기 위해 강력한 기능을 제공하는 도구
- css 전처리 도구
- css로 변환해서 동작
- 변수를 만들어서 재활용할 수 있음
- 중첩 기능 제공
- less, stylus보다 더 많이 사용하고 성숙도가 높으며, 안정적인 기능을 제공
- sass와 scss 중 표준 css와 호환되는 scss 사용 
- sass와 scss는 중괄호와 세미콜론의 여부 차이(mixin 제외)

```bash
# 프로젝트 생성

$ mkdir scss-test
$ cd scss-test
$ npm init -y
$ npm i -D parcel-bundler
```

<br>

```json
// package.json

"scripts": {
  "dev": "parcel index.html",
  "build": "parcel build index.html"
},
```

<br>

```html
<!-- index.html -->

<head>
  <title>Document</title>
  <link rel="stylesheet" href="./main.scss" />
</head>

<body>
  <div class="container">
    <h1>Hello SCSS!</h1>
  </div>
</body>
```

<br>

```scss
// main.scss

$color: tomato;

.container {
  h1 {
    color: $color;
  }
}
```

<h1 style="color: tomato;">Hello SCSS!</h1>