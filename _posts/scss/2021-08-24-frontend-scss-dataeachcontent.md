---
title: "[SCSS] SCSS 데이터 종류, @each, @content"
excerpt: SCSS 데이터 종류, 반복문 @each, 재활용 @content
categories:
- SCSS
tags:
- - SCSS
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-24T22:00:00'
last_modified_at: 2021-08-24T22:00:00
---

## 1. SCSS 데이터 종류

```scss
// scss

$number: 1;  // .5, 100px, 1em
$string: bold;  // relative, "../images/a.png"
$color: red;  // blue, #FFFF00, rgba(0,0,0,.1)
$boolean: true;  // false
$null: null;
$list: orange, royalblue, yellow;
$map: (
  o: orange,
  r: royalblue,
  y: yellow
);
.box {
  width: 100px;
  color: red;
  position: null;
}
```

<br>

```css
/* css */

.box {
  width: 100px;
  color: red;
}
```


<br>

## 2. 반복문 @each

```scss
// scss

$list: orange, royalblue, yellow;
$map: (
  o: orange,
  r: royalblue,
  y: yellow
);

@each $c in $list {
  .box1{
    color: $c;
  }
}

@each $key, $value in $map {
  .box2-#{$k} {
    color: $v;
  }
}
```

<br>

```css
/* css */

.box1 {
  color: orange;
}
.box1 {
  color: royalblue;
}
.box1 {
  color: yellow;
}
.box2-o {
  color: orange;
}
.box2-r {
  color: royalblue;
}
.box2-y {
  color: yellow;
}
```


<br>

## 3. 재활용 @content

```scss
// scss

@mixin left-top {
  position: absolute;
  top: 0;
  left: 0;
  @content;
}
.container {
  width: 100px;
  height: 100px;
  @include left-top;
}
.box {
  width: 200px;
  height: 300px;
  @include left-top {
    bottom: 0;
    right: 0;
    margin: auto;
  }
}
```

<br>

```css
/* css */

.container {
  width: 100px;
  height: 100px;
  position: absolute;
  top: 0;
  left: 0; 
}
.box {
  width: 200px;
  height: 300px;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;  
}
```