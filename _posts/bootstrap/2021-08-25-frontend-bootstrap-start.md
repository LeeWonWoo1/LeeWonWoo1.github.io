---
title: "[Bootstrap] 개요"
excerpt: Bootstrap 개요
categories:
- Bootstrap
tags:
- - Bootstrap
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-25T03:00:00'
last_modified_at: 2021-08-25T03:00:00
---

## 1. Bootstrap이란?

- 동적인 웹 사이트 및 웹 응용 개발을 위한 프론트엔드 프레임워크
- UI를 따로 구현하지 않아도 미리 정의된 컴포넌트를 자신의 프로젝트에 적용할 수 있음
- 5.0 버전부터 Tree Shaking을 지원
    - 단일 번들을 최적화할 때 사용
    - 필요하지 않은 코드를 제거하는 기술


<br>

## 2. CDN 프로젝트 생성

[Bootstrap](https://getbootstrap.com/docs/5.1/getting-started/introduction/){:target="_blank"}
{: .notice--info}

```bash
# 프로젝트 생성

$ mkdir bootstrap-test
$ cd bootstrap-test
$ code .
```

<br>

```html
<!-- index.html -->

<head>
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-U1DAWAznBHeqEIlVSCgzq+c9gqGAJn5c/t99JyeKa9xxaYpSvHU5awsuZVVFIhvj" crossorigin="anonymous"></script>
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