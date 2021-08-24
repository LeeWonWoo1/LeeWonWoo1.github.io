---
title: "[SCSS] SCSS 반복문, 함수, 가져오기"
excerpt: SCSS For, Function, Import
categories:
- SCSS
tags:
- - SCSS
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-24T19:00:00'
last_modified_at: 2021-08-24T19:00:00
---

## 1. SCSS 반복문

```scss
// for (let i = 0; i < 10; i += 1) {
//    console.log(`loop-${i}`)
// }
// 보간 : #{}
// scss

@for $i from 1 through 10 {
  .box {
    .box:nth-child(#{$i}) {
      width: 100px * $i;
    }
  }
}
```

<br>

```css
.box:nth-child(1) {
  width: 100px;
}
.box:nth-child(2) {
  width: 200px;
}
.box:nth-child(3) {
  width: 300px;
}
...
.box:nth-child(10) {
  width: 1000px;
}
```


<br>

## 2. SCSS 함수

```scss
// scss

@mixin center {
  display: flex;
  justify-content: center;
  align-items: center;
}

@function ratio($size, $ratio) {
  @return $size * $ratio
}

.box {
  $width: 100px;
  width: $width;
  height: ratio($width, 9/16);
  @include center;
}
```

<br>

```css
/* css */

.box {
  width: 160px;
  height: 90px;
  display: flex;
  justify-content: center;
  align-items: center;
}
```


<br>

## 3. SCSS 색상 내장 함수

```html
<!-- html -->

<div class="box"></div>
<div class="box built-in"></div>
```

<br>

```scss
// scss

.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
  &:hover {
    // mix() -> 두 색을 섞어서 새로운 색을 출력
    background-color: mix($color, red);

    // lighten() -> 색상을 밝게 만들어 줌
    background-color: lighten($color, 10%);

    // darken() -> 색상을 어둡게 만들어 줌
    background-color: darken($color, 10%);
  }
  &.built-in {
    // saturate() -> 색상의 채도를 올림
    background-color: saturate($color, 40%);

    // desaturate() -> 색상의 채도를 낮춤
    background-color: desaturate($color, 40%);

    // grayscale() -> 색상을 회색으로 만들어 줌
    background-color: graysclae($color);

    // invert() -> 색상을 반전시킴
    background-color: invert($color);

    // rgba() -> 색상을 반투명하게 함
    background-color: rgba($color, .5);
  }
}
```


<br>

## 4. SCSS 가져오기

```html
<!-- index.html -->

<head>
  <title>Document</title>
  <link rel="stylesheet" href="./main.scss" />
</head>

<body>
  <div class="container">
    <h1>Hello SCSS!!</h1>
  </div>
</body>
```

<br>

```scss
// main.scss

// 간소화된 문법(url 함수, 확장자 표기 안해도 작동)
@import "./sub", "./sub2";

$color: royalblue;

.container {
  h1 {
    color: $color;
  }
}


// sub.scss

body {
  .container {
    background-color: orange;
  }
}


// sub2.scss

body {
  background-color: royalblue;
}
```