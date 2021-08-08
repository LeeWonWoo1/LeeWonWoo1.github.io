---
title: "[Javascript] 반복문"
excerpt: for문
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-09T00:00:00'
last_modified_at: 2021-08-09T00:00:00
---

## 반복문 for

```javascript
// for (시작조건; 종료조건; 변화조건) {}

// ul태그 내부에 li태그 10개 생성하는 예제
const ulEl = document.querySelector('ul');

for (let i = 0; i < 10; i += 1) {
  const li = document.createElement('li');   
  li.textContent = `list-${i + 1}`
  
  // 짝수 번호의 li태그를 클릭하면 문자 출력하는 부분
  if ((i+1) % 2 === 0) {  
      li.addEventListener('click', function () {
        console.log(li.textContent);
      });
  }
  ulEl.appendChild(li);
}
```