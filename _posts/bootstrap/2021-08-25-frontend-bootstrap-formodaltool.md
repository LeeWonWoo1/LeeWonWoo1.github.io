---
title: "[Bootstrap] 양식, 모달, 툴팁"
excerpt: Bootstrap Forms, Modal, Tooltips
categories:
- Bootstrap
tags:
- - Bootstrap
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-25T04:00:00'
last_modified_at: 2021-08-25T04:00:00
---

## 1. Bootstrap 양식

[Bootstrap 양식](https://getbootstrap.com/docs/5.1/forms/overview/){:target="_blank"}
{: .notice--info}

- 사용자에게 데이터를 입력받는 양식 제공


<br>

## 2. Bootstrap 모달

[Bootstrap 모달](https://getbootstrap.com/docs/5.1/components/modal/){:target="_blank"}
{: .notice--info}

```html
<!-- index.html -->

<body>
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
          <form>
            <div class="mb-3">
              <label for="exampleInputEmail1" class="form-label">Email address</label>
              <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
              <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
            </div>
            <div class="mb-3">
              <label for="exampleInputPassword1" class="form-label">Password</label>
              <input type="password" class="form-control" id="exampleInputPassword1">
            </div>
            <div class="mb-3 form-check">
              <input type="checkbox" class="form-check-input" id="exampleCheck1">
              <label class="form-check-label" for="exampleCheck1">Check me out</label>
            </div>
          </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
          <button type="submit" class="btn btn-primary">Submit</button>
        </div>
      </div>
    </div>
  </div>
</body>
```

<br>

```js
// main.js

// modal창 활성화 시, email 입력 form에 focus 하는 기능
const emailInputEl = document.querySelector('#exampleInputEmail1')
const modalEl = document.querySelector('#exampleModal')

modalEl.addEventListener('shown.bs.modal', function () {
  emailInputEl.focus()
})
```


<br>

## 3. Bootstrap 툴팁

[Bootstrap 툴팁](https://getbootstrap.com/docs/5.1/components/tooltips/){:target="_blank"}
{: .notice--info}

- 성능상의 이유로 포함되어 있지 않기 때문에, 직접 초기화해야 함

```html
<!-- index.html -->

<body>
  <button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="top"
    title="Tooltip on top">
    Tooltip on top
  </button>
  <button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="right"
    title="Tooltip on right">
    Tooltip on right
  </button>
  <button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="bottom"
    title="Tooltip on bottom">
    Tooltip on bottom
  </button>
  <button type="button" class="btn btn-secondary" data-bs-toggle="tooltip" data-bs-placement="left"
    title="Tooltip on left">
    Tooltip on left
  </button>
</body>
```

<br>

```js
// main.js

// 직접 초기화
var tooltipTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="tooltip"]'))
var tooltipList = tooltipTriggerList.map(function (tooltipTriggerEl) {
  return new bootstrap.Tooltip(tooltipTriggerEl)
})
```