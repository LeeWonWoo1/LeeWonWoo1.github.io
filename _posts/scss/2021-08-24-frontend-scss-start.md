---
title: "[SCSS] SCSS 개요, 참조, 중첩"
excerpt: SCSS Overview, Meister, Nesting
categories:
- SCSS
tags:
- - SCSS
  - Web
  - NPM
toc: true
toc_sticky: true
popular: true
date: '2021-08-24T02:00:00'
last_modified_at: 2021-08-24T02:00:00
---

## 1. SCSS

**SCSS 테스트 페이지** [https://sassmeister.com](https://sassmeister.com){:target="_blank"}
{: .notice--info}

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


<br>

## 2. SCSS 주석

- /*  */ : SCSS에서 CSS로 컴파일해도 코드 안에 포함
- // : SCSS에서 CSS로 컴파일하면 코드 안에 포함되지 않음


<br>

## 3. 중첩 With SassMeister

```html
<div class="container">
  <ul>
    <li>
      <div class="name">LWW</div>
      <div class="age">43</div>
    </li>
  </ul>
</div>
```

<br>

```css
/* css */
/* 상위 선택자를 반복적으로 작성해야 함 */

.container > ul li {
  font-size: 40px;
}
.container > ul li .name {
  color: royalblue;
}
.container > ul li .age {
  color: orange;
}
```

<br>

```scss
// scss
// 중첩(Nesting)

.container {
  > ul {
    li {
      font-size: 40px;
      .name {
        color: royalblue;
      }
      .age {
        color: orange;
      }
    }
  }
}
```

<div class="name" style="font-size: 40px; color: royalblue;">LWW</div>
<div class="age" style="font-size: 40px; color: orange;">43</div>


<br>

## 4. 상위 선택자 참조

- &는 자신이 포함된 영역의 상위 선택자를 참조

```scss
// ex 1) scss

.btn {
  position: absolute;
  &.active {
    color: red;
  }
}

.list {
  li {
    &:last-child {
      margin-right: 0;
    }
  }
}
```

<br>

```css
/* ex 1) css */

.btn {
  position: absolute;
}
.btn.active {
  color: red;
}
.list li:last-child {
  margin-right: 0;
}
```

<br>

```scss
// ex 2) scss

.fs {
  &-small { font-size: 12px; }
  &-medium { font-size: 14px; }
  &-large { font-size: 16px; }
}
```

<br>

```css
/* ex 2) css */

.fs-small {
  font-size: 12px;
}
.fs-medium {
  font-size: 14px;
}
.fs-large {
  font-size: 16px;
}
```


<br>

## 5. 중첩된 속성

- 선택자처럼 사용하고, 뒤에 : 기호를 붙임
- 중괄호가 끝나는 부분에 ; 붙여줌

```scss
// scss

.box {
  font: {
    weight: bold;
    size: 10px;
    family: sans-serif;
  };
  margin: {
    top: 10px;
    left: 20px;
  };
  padding: {
    top: 10px;
    bottom: 40px;
    left: 20px;
    right: 30px;
  };
}
```

<br>

```css
/* css */

.box {
  font-weight: bold;
  font-size: 10px;
  font-family: sans-serif;
  margin-top: 10px;
  margin-left: 20px;
  padding-top: 10px;
  padding-bottom: 40px;
  padding-left: 20px;
  padding-right: 30px;
}
```