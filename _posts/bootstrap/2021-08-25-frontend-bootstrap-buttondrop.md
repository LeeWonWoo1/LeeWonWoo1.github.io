---
title: "[Bootstrap] 버튼, 드롭다운"
excerpt: Bootstrap Button, Dropdown
categories:
- Bootstrap
tags:
- - Bootstrap
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-25T03:30:00'
last_modified_at: 2021-08-25T03:30:00
---

## 1. Bootstrap 버튼, 버튼 그룹

[Bootstrap 버튼](https://getbootstrap.com/docs/5.1/components/buttons/){:target="_blank"}
{: .notice--info}

```html
<!-- index.html -->
<body>
  <!-- 버튼 그룹 -->
  <div class="btn-group">

    <!-- 기본 버튼 -->
    <button type="button" class="btn btn-primary">Primary</button>
    <button type="button" class="btn btn-secondary">Secondary</button>
    <button type="button" class="btn btn-success">Success</button>
    <button type="button" class="btn btn-danger">Danger</button>
    <button type="button" class="btn btn-warning">Warning</button>
    <button type="button" class="btn btn-info">Info</button>
    <button type="button" class="btn btn-light">Light</button>
    <button type="button" class="btn btn-dark">Dark</button>
    <button type="button" class="btn btn-link">Link</button>
    
    <!-- 아웃라인 버튼 -->
    <div class="btn btn-outline-primary">ABC</div>
    <div class="btn btn-outline-success">ABC</div>

    <!-- 버튼 사이즈 -->
    <div class="btn btn-primary btn-lg">ABC</div>
    <div class="btn btn-primary btn-sm">ABC</div>

    <!-- 버튼 비활성화 -->
    <div class="btn btn-primary btn-lg" disabled>ABC</div>
  </div>
</body>
```


<br>

## 2. Bootstrap 드롭다운, 리스트

[Bootstrap 드롭다운](https://getbootstrap.com/docs/5.1/components/dropdowns/){:target="_blank"}
{: .notice--info}

[Bootstrap 리스트 그룹](https://getbootstrap.com/docs/5.1/components/list-group/){:target="_blank"}
{: .notice--info}

```html
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

  <ul class="list-group">
    <li class="list-group-item list-group-item-action">An item</li>
    <li class="list-group-item list-group-item-action active">A second item</li>
    <li class="list-group-item list-group-item-action">A third item</li>
    <li class="list-group-item list-group-item-action">A fourth item</li>
    <li class="list-group-item list-group-item-action">And a fifth one</li>
  </ul>
</body>
```