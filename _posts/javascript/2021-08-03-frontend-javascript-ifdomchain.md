---
title: "[Javascript] 조건문, DOM API, 메소드 체이닝"
excerpt: if, else, Document Object Model, Method Chaining 정리
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-03T01:00:00'
last_modified_at: 2021-08-03T01:00:00
---

## 1. 조건문

- 조건의 결과에 따라 다른 코드를 실행하는 구문

```javascript
let isShow = true;
let checked = false;

if (isShow) {
  console.log('Show');  // Show
}

if (checked) {
  console.log('Checked');
}
```

<br>

```javascript
let isShow = true;

if (isShow) {
  console.log('Show');  // Show
} else {
  console.log('Hide');
}
```


<br>

## 2. DOM API

```html
<body>
 <div class="box">Box!!</div>
</body>
```

```javascript
// HTML 요소 1개 검색
const boxEl = document.querySelector('.box');

// HTML 요소에 적용할 수 있는 메소드
boxEl.addEventListener();

// 인수 추가 가능
boxEl.addEventListener(1, 2);

// 1 - 이벤트(Event, 상황)
boxEl.addEventListener('click', 2);

// 2 - 핸들러(Handler, 실행할 함수)
boxEl.addEventListener('click', function () {
  console.log('Click!');
});
```

<br>

```javascript
// HTML 요소 1개 검색
const boxEl = document.querySelector('.box');

// 요소의 클래스 정보 객체 활용
boxEl.classList.add('active');
let isContains = boxEl.classList.contains('active');
console.log(isContains);  // true

boxEl.classList.remove('active');
isContains = boxEl.classList.contains('active');
console.log(isContains);  // false
```

<br>

```javascript
// HTML 요소 모두 검색
const boxEls = document.querySelectorAll('.box');
console.log(boxEls);

// 찾은 요소들 반복해서 함수 실행
// 익명 함수를 인수로 추가
boxEls.forEach(function () {});

// 첫 번째 매개변수 : 반복 중인 요소
// 두 번째 매개변수 : 반복 중인 번호
boxEls.forEach(function (boxEl, index) {});

// 출력
boxEls.forEach(function (boxEl, index) {
  boxEl.classList.add(`order-${index + 1}`);
  console.log(index, boxEl);
});
```

<br>

```javascript
const boxEl = document.querySelector('.box');

// Getter, 값을 얻는 용도
console.log(boxEl.textContent);  // BOX!!

// Setter, 값을 지정하는 용도
boxEl.textContent = 'Change!!';
console.log(boxEl.textContent);  // Change!!
```


<br>

## 3. 메소드 체이닝

```javascript
const a = 'Hello!';
// split : 문자를 인수 기준으로 쪼개서 배열로 반환
// reverse : 배열 뒤집기
// join : 배열을 인수 기준으로 문자로 병합해 반환
const b = a.split('').reverse().join('');  // 메소드 체이닝

console.log(a)  // Hello!
console.log(b)  // !olleH
```