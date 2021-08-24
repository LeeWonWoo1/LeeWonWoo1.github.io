---
title: "[Bootstrap] 커스터마이징, 성능 최적화"
excerpt: Bootstrap 테마 색상 Customizing, Tree Shaking
categories:
- Bootstrap
tags:
- - Bootstrap
  - Web
  - NPM
toc: true
toc_sticky: true
popular: true
date: '2021-08-25T04:30:00'
last_modified_at: 2021-08-25T04:30:00
---

## 1. NPM 프로젝트 생성

- Bootstrap에서 사용자가 필요로하는 기능만 가지고 올 수 있음
- 기본적인 테마를 입맛에 맞게 커스터마이징 할 수 있음

```bash
$ npm init -y
$ npm i -D parcel-bundler
$ npm i bootstrap@next
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
  <link rel="stylesheet" href="./scss/main.scss">
  <script defer src="./main.js"></script>
</head>

<body>
  <div class="dropdown">
    <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown"
      aria-expanded="false">
      Dropdown button
    </button>
    <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
      <li><a class="dropdown-item" href="#">Action</a></li>
      <li><a class="dropdown-item" href="#">Another action</a></li>
      <li><a class="dropdown-item" href="#">Something else here</a></li>
    </ul>
  </div>
</body>
```

<br>

```scss
// scss/main.scss

@import "../node_modules/bootstrap/scss/bootstrap";
```

<br>

```js
// main.js

import bootstrap from 'bootstrap/dist/js/bootstrap.bundle'
```


<br>

## 2. 테마 색상 커스터마이징

[Bootstrap 색상 커스터마이징](https://getbootstrap.com/docs/5.1/customize/color/){:target="_blank"}
{: .notice--info}

```html
<!-- index.html -->

<body>
  <div class="dropdown">
    <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown"
      aria-expanded="false">
      Dropdown button
    </button>
    <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
      <li><a class="dropdown-item" href="#">Action</a></li>
      <li><a class="dropdown-item" href="#">Another action</a></li>
      <li><a class="dropdown-item" href="#">Something else here</a></li>
    </ul>
  </div>

  <div class="spinner-border text-secondary" role="status">
    <span class="visually-hidden">Loading...</span>
  </div>
</body>
```

<br>

```scss
// scss/main.scss

@import "../node_modules/bootstrap/scss/functions";
@import "../node_modules/bootstrap/scss/variables";
@import "../node_modules/bootstrap/scss/mixins";

$theme-colors: (
  "primary":    $primary,
  "secondary":  royalblue,  // 색상 변경
  "success":    $success,
  "info":       $info,
  "warning":    $warning,
  "danger":     $danger,
  "light":      $light,
  "dark":       $dark
);

@import "../node_modules/bootstrap/scss/bootstrap";
```


<br>

## 3. 성능 최적화

[Bootstrap 성능 최적화](https://getbootstrap.com/docs/5.1/customize/optimize/){:target="_blank"}
{: .notice--info}

```html
<!-- index.html -->

<body>
  <div class="dropdown">
    <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown"
      aria-expanded="false">
      Dropdown button
    </button>
    <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
      <li><a class="dropdown-item" href="#">Action</a></li>
      <li><a class="dropdown-item" href="#">Another action</a></li>
      <li><a class="dropdown-item" href="#">Something else here</a></li>
    </ul>
  </div>

  <div class="spinner-border text-secondary" role="status">
    <span class="visually-hidden">Loading...</span>
  </div>

  <!-- Button trigger modal -->
  <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
    Launch demo modal
  </button>

  <!-- Modal -->
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          ...
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
          <button type="button" class="btn btn-primary">Save changes</button>
        </div>
      </div>
    </div>
  </div>
</body>
```

<br>

```js
// main.js

// 개별 속성 import
import Dropdown from 'bootstrap/js/dist/dropdown'
import Modal from 'bootstrap/js/dist/modal'

// 초기화 코드
const dropdownElementList = [].slice.call(document.querySelectorAll('.dropdown-toggle'))
dropdownElementList.map(function (dropdownToggleEl) {
  return new Dropdown(dropdownToggleEl)
})

// 초기화 코드
new Modal(document.querySelector('#exampleModal'), {
  backdrop: 'static'  // 배경을 클릭하면 모달이 꺼지지 않도록 함
})
```