---
title: "[Bundler] Parcel Babel, CLI"
excerpt: Parcel Babel, CLI
categories:
- Bundler
tags:
- - Bundler
  - Web
  - Node.js
  - Parcel
toc: true
toc_sticky: true
popular: true
date: '2021-08-27T00:00:00'
last_modified_at: 2021-08-27T00:00:00
---

## 1. Babel

- 컴파일러
- 최신의 문법으로 만든 Javascript 코드를 구형 브라우저에서도 동작할 수 있는 ES5 버전으로 컴파일 해줌

```bash
# terminal

npm i -D @babel/core @babel/preset-env

# async, await 등 비동기 문법 동작용 패키지
npm i -D @babel/plugin-transform-runtime  
```

<br>

```json
// package.json

"browserslist": [
  "> 1%",  // 점유율이 1% 이상인 모든 브라우저
  "last 2 versions"  // 해당하는 브라우저의 마지막 2개 버전
]
```

<br>

```js
// .babelrc.js

module.exports = {
  presets: ['@babel/preset-env'],
  plugins: [
    ['@babel/plugin-transform-runtime']
  ]
}
```

<br>

```js
// js/main.js

console.log('Hello Parcel!')

async function test() {
  const promise = Promise.resolve(123)
  console.log(await promise)
}

test()
```

<br>

```bash
# terminal

$ npm run dev
```

<br>

![parcel-babel](https://user-images.githubusercontent.com/62803763/130994524-147a42da-954f-4af9-b1ad-e82a01d93b49.PNG){: .align-center .open-new}


<br>

## 2. CLI

[https://ko.parceljs.org/cli.html](https://ko.parceljs.org/cli.html){:target="_blank"}에서 내용 확인
{: .notice--info}

- 빠른 모듈 교체(HMR) : 런타임에서 페이지 새로고침 없이 수정된 내용을 자동으로 갱신

```json
// package.json

  "scripts": {
    // 포트 번호 변경
    "dev": "parcel index.html --port 7777",
    "build": "parcel build index.html"
  },
```

<br>

```bash
$ npm run dev  # localhost:7777
```