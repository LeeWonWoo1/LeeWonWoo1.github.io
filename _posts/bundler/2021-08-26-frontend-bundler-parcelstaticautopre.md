---
title: "[Bundler] Parcel static, autoprefixer"
excerpt: Parcel static, autoprefixer
categories:
- Bundler
tags:
- - Bundler
  - Web
  - NPM
  - Parcel
toc: true
toc_sticky: true
popular: true
date: '2021-08-26T20:00:00'
last_modified_at: 2021-08-26T20:00:00
---

## 1. Bundler 개요

- 웹에서는 HTML, CSS, Javascript가 동작
- 순수하게 HTML, CSS, Javascript로 코딩하는 것은 비효율적
- 따라서 다양한 기능들을 이용해 웹 개발을 하는데, 그것들은 웹에서 직접적으로 동작하지 않음
- 그것을 변환하는 과정을 거져 HTML, CSS, Javascript로 바꿔서 웹에서 동작시킴
- 즉, Vue.js, React, Sass 등을 Bundler를 통해 웹에서 동작시킬 수 있는 형태로 바꿀 수 있음
- Bundler 자체가 이해해서 변환해주는 것이 아니라 외부의 패키지의 도움을 받아 변환
- 수동의 작업을 Bundler에게 위임
- Parcel : 구성 없는 단순한 자동 번들링, 소/중형 프로젝트에 적합
- Webpack : 매우 꼼꼼한 구성, 중/대형 프로젝트에 적합

![parcel-start2](https://user-images.githubusercontent.com/62803763/130965363-814c28a7-46fb-4ff7-8681-2a5610300750.PNG){: .align-center .open-new}


<br>

## 2. 프로젝트 시작

```bash
# 프로젝트 생성

$ mkdir parcel-template-basic
$ cd parcel-template-basic
$ npm init -y
$ npm i -D parcel-bundler
```

<br>

```json
// package.json

"scripts": {
  "dev": "parcel index.html",
  "build": "parcel build index.html"
}
```

<br>

```html
<!-- index.html -->

<head>
  <title>Parcel Bundler</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reset-css@5.0.1/reset.min.css">  <!-- reset.css cdn-->
  <link rel="stylesheet" href="./scss/main.scss">
  <script defer src="./js/main.js"></script>
</head>

<body>
  <h1>Hello Parcel!!</h1>
</body>
```

<br>

```scss
// scss/main.scss

$color--black: #000;
$color--white: #fff;

body {
  background-color: $color--black;
  h1 {
    color: $color--white;
  }
}
```

<br>

```js
// js/main.js

console.log('Hello Parcel!')
```

<br>

![parcel-start](https://user-images.githubusercontent.com/62803763/130954644-502bc6bd-9e08-4836-b9fa-9c69dc65a993.PNG){: .align-center .open-new}


<br>

## 3. 정적 파일 연결

[https://www.icoconverter.com/](https://www.icoconverter.com/){:target="_blank"}에서 원하는 이미지 변경
{: .notice--info}

- 원본 이미지와 변환된 이미지를 프로젝트 폴더 루트 경로에 복사
- 원본 이미지는 images 폴더를 생성하고 이 폴더에 넣어줌

![parcel-start3](https://user-images.githubusercontent.com/62803763/130966112-e1e85b2e-8ab4-47c2-9211-95ee1c18b299.PNG){: .align-center .open-new}

<br>

```html
<!-- index.html -->

<body>
  <h1>Hello Parcel!!</h1>
  <img src="./images/bear.jpg" alt="Bear" />
</body>
```

<br>

- Favicon이 정상적으로 출력되지 않음
- 웹에서 확인하는 HTML 파일은 dist폴더에 있는 HTML 파일임
- 그것을 만들어내는 용도로 루트 경로에 있는 index.html 파일을 Parcel-Bundler가 사용
- 즉, favicon.ico파일을 dist 폴더로 넣어주면 됨
- 하지만 dist폴더는 언제든지 지울 수 있어야 하기 때문에 파일을 dist 폴더에 직접적으로 넣는 방식은 좋지 않음
- 따라서 해당하는 파일을 개발서버를 열거나 제품화시킬때 dist폴더로 자동으로 넣어줄 수 있는 패키지의 도움을 받아야 함

[https://www.npmjs.com/package/parcel-plugin-static-files-copy](https://www.npmjs.com/package/parcel-plugin-static-files-copy){:target="_blank"}에 접속해서 내용 확인
{: .notice--info}

```bash
# terminal

$ npm i -D parcel-plugin-static-files-copy
```

<br>

```json
// package.json

"staticFiles": {
  "staticPath": "static"
}
```

<br>

- 루트 경로에 static 폴더를 만들고 favicon.ico 파일을 넣어줌

![parcel-start4](https://user-images.githubusercontent.com/62803763/130968669-b4717529-8ed7-491a-a44c-78114fe83a4a.PNG){: .align-center .open-new}

<br>

- dist 파일에 favicon.ico 파일이 복사됨

![parcel-start5](https://user-images.githubusercontent.com/62803763/130984672-a80e377d-5aff-45cc-bece-0f2cde4893f2.PNG){: .align-center .open-new}

<br>

- Favicon 출력 확인

```bash
$ npm run dev
```


<br>

## 4. Autoprefixer

- Autoprefixer는 공급 업체 접두사(Vender Prefix)를 자동으로 붙여줄 수 있는 패키지
- CSS 스타일 보험
- Vender Prefix는 모든 브라우저에서 CSS의 기능을 동일하게 사용하기 위하여 브라우저의 제조사별 접두어를 CSS에 표기하는 것

```bash
# terminal

npm i -D postcss autoprefixer
```

<br>

```json
// package.json

// 현재 NPM 프로젝트에서 지원할 브라우저의 범위를 명시하는 용도
// 이 명시를 Autoprefixer 패키지가 활용
"browserslist": [
  "> 1%",  // 점유율이 1% 이상인 모든 브라우저
  "last 2 versions"  // 해당하는 브라우저의 마지막 2개 버전
]
```

<br>

```js
// .postcssrc.js
// 뒤에 rc(Runtime Configuration)가 붙은 파일은 구성 파일을 의미

// ESM : 브라우저 환경에서 동작
// CommonJS : Node.js 환경 동작

// import autoprefixer from 'autoprefixer'
const autoprefixer = require('autoprefixer')

// export {
//   plugins: [
//     autoprefixer
//   ]
// }
module.exports = {
  plugins: [
    autoprefixer
  ]
}


// ---------------------------------------------------------
// 간소화
module.exports = {
  plugins: [
    require('autoprefixer')
  ]
}
```

<br>

```scss
// scss/main.scss

$color--black: #000;
$color--white: #fff;

body {
  background-color: $color--black;
  h1 {
    color: $color--white;
    display: flex;
  }
}
```

<br>

```bash
# terminal

$ npm run dev
```

<br>

- Autoprefixer와 Postcss의 버전이 충돌하는 경우

```bash
# terminal

$ npm i -D autoprefixer@9
$ npm run dev
```

<br>

![parcel-start6](https://user-images.githubusercontent.com/62803763/130990211-bead634d-ef77-4607-a179-e4e613fd951a.PNG){: .align-center .open-new}