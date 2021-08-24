---
title: "[SCSS] SCSS 변수, 연산, 재활용"
excerpt: SCSS Variable, Opeation, Mixins
categories:
- SCSS
tags:
- - SCSS
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-24T18:00:00'
last_modified_at: 2021-08-24T18:00:00
---

## 1. SCSS 변수(Variables)

```scss
// scss

$size: 100px;  // 전역변수

.container {
  $color: red;  // 지역변수
  position: fixed;
  top: $size;
  .item {
    $size: 200px;  // 재할당
    color: $color;
    width: $size;
    height: $size;
    transform: translateX($size);
  }
  left: $size;  // 범위 밖이지만, 재할당된 값으로 바뀜
}
.box {
  color: $color;  // Error!
}
```

<br>

```css
/* css */

.container {
  position: fixed;
  top: 100px;
  left: 200px;
}
.cotainer .item {
  color: red;
  width: 200px;
  height: 200px;
  transform: translateX(100px);
}
```


<br>

## 2. SCSS 연산(Operation)

```scss
// scss

div {
  width: 20px + 20px;
  height: 40px - 10px;
  font-size: 10px * 2;
  margin: 30px / 2;  // 연산하지 않음(단축 속성)
  padding: 20px % 7;
}
span {
  font-size: 10px;
  line-height: 10px;
  font-family: serif;
  font: 10px / 10px serif; // 연산하지 않음(단축 속성)
}
```

<br>

```css
/* css */

div {
  width: 40px;
  height: 30px;
  font-size: 20px;
  margin: 30px/2;
  padding: 6px;
}
span {
  font-size: 10px;
  line-height: 10px;
  font-family: serif;
  font: 10px / 10px serif;
}
```

<br>

```scss
// scss 나누기 연산

// 방법 1 : 괄호
div {
  margin: (30px / 2);
}

// 방법 2 : 변수
span {
  $size: 30px;
  font-size: $size / 2;
}

// 방법 3 : 다른 산술연산 포함
h1 {
  font-size: 10px + 12px / 2;
}
```

<br>

```css
/* css 나눗셈 결과*/

div {
  margin: 15px
}
span {
  font-size: 15px
}
h1 {
  font-size: 16px;
}
```

<br>

```scss
// scss 연산은 단위가 일치해야 함

div {
  width: 100% - 200px;  // Error!
}

.box {
  width: calc(100% - 200px);  // calc 함수 사용
}
```


<br>

## 3. SCSS 재활용(Mixins)

```html
<div class="container">
  <div class="item">
    Mixin!
  </div>
</div>
```

<br>

```css
.container {
  width: 200px;
  height: 200px;
  background-color: orange;
  display: flex;
  justify-content: center;
  align-items: center;
}
.container .item {
  width: 100px;
  height: 100px;
  background-color: royalblue;
}
```

<div class="container" style="width: 200px; height: 200px; background-color: orange; display: flex; justify-content: center; align-items: center;">
  <div class="item" style="width: 100px; height: 100px; background-color: royalblue; display: flex; justify-content: center; align-items: center;">
    Mixin!
  </div>
</div>

<br>

```scss
// ex 1) scss 재활용

@mixin center {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  @include center;
  .item {
    @include center;
  }
}
.box {
  @include center;
}
```

<br>

```css
/* ex 1) css */

.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container .item {
  display: flex;
  justify-content: center;
  align-items: center;
}
.box {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

<br>

```scss
// ex 2) scss 재활용($매개변수: 인수)

@mixin box($size: 100px, $color: tomato) {
  width: $size;
  height: $size;
  background-color: $color;
}
.container {
  @include box(200px, red);
  .item {
    @include box($color: green);  // 키워드 인수
  }
}
.box {
  @include box();
}
```

<br>

```css
/* ex 2) css */

.container {
  width: 200px;
  height: 200px;
  background-color: red;
}
.container .item {
  width: 100px;
  height: 100px;
  background-color: green;
}
.box {
  width: 100px;
  height: 100px;
  background-color: tomato;
}
```