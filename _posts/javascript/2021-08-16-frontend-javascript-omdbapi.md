---
title: "[Javascript] OMDb API"
excerpt: 영화 DB를 요청해 프로젝트에 적용
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
  - Json
  - OMDb
toc: true
toc_sticky: true
popular: true
date: '2021-08-16T21:00:00'
last_modified_at: 2021-08-16T21:00:00
---

## OMDb API

자세한 내용은 **omdb api** 검색
{: .notice--notice}

1. Usage 부분의 주소를 복사해 검색창에 붙여넣기
2. api key를 입력
3. https://www.omdbapi.com/?apikey=5f6c9466&s=frozen
4. JSON 포맷의 정보가 출력됨
5. axios 패키지 설치

```bash
$ npm i axios
$ npm run dev
```

<br>

```javascript
// main.js

import axios from 'axios'

function fetchMovies() {
  // 해당하는 정보를 가져옴
  // http's'로 요청
  axios
    .get('https://www.omdbapi.com/?apikey=5f6c9466&s=frozen')
    .then(res => {
      console.log(res)
      const h1El = document.querySelector('h1')
      const imgEl = document.querySelector('img')
      h1El.textContent = res.data.Search[0].Title  // 제목 출력
      imgEl.src = res.data.Search[0].Poster  // 포스터 출력
    })
}
fetchMovies()  // {data: {...}, status: 200, statusText: "", headers: {..} ..}
```

<br>

```html
<!-- 영화 제목과 포스터 사진 출력 -->
<body>
  <h1>Hello world!</h1>
  <img src="" alt="" width="200" />
</body>
```


<br>

### - Query String

- 문자를 사용해 어떤 내용을 검색
- 주소?속성=값&속성=값&속성=값