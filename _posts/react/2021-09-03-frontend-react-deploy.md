---
title: "[React] Deploy React App"
excerpt: React App 배포하기
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
toc: true
toc_sticky: true
popular: true
date: "2021-09-03T20:00:00"
last_modified_at: 2021-09-03T20:00:00
---

## 1. SPA 프로젝트 배포 이해하기

- npm run build
  - Production 모드로 빌드되어, 'build' 폴더에 배포를 위한 파일 생성
    - 이렇게 만들어진 파일들을 웹서버를 통해 사용자가 접근할 수 있도록 처리
  - build/static 폴더 안에 JS, CSS 파일들이 생성
    - 파일 이름에 hash 값이 붙음
    - long term caching techniques
- 특징
  - 모든 요청을 서버에 하고 받아오는 형태가 아님
  - 라우팅 경로에 상관없이 React App을 받아 실행
  - 라우팅은 받아온 React App을 실행 후 적용
  - static 파일을 제외한 모든 요청을 index.html로 응답해 주도록 작업
- serve -s build
- AWS S3에 배포
- node.js express
- NginX

<br>

## 2. serve 패키지로 React App 배포

```bash
# terminal

$ npm install serve -g
$ serve -s build  # -s옵션은 어떤 라우팅으로 요청해도 index.html 응답
```

<br>

## 3. AWS S3에 React App 배포

![react-deploy1](https://user-images.githubusercontent.com/62803763/131993906-5d52adb4-d43b-4f46-b713-21c42a6a3439.PNG){: .align-center .open-new}

![react-deploy2](https://user-images.githubusercontent.com/62803763/131993951-1a1734cc-07eb-4831-9366-c0c195651a39.PNG){: .align-center .open-new}

![react-deploy3](https://user-images.githubusercontent.com/62803763/131993960-258c5b68-54b0-4ef4-9338-b4c58406f9fb.PNG){: .align-center .open-new}

![react-deploy4](https://user-images.githubusercontent.com/62803763/131993969-4caf5c15-1ffa-400b-9a6d-09fa0fd6ce31.PNG){: .align-center .open-new}

![react-deploy5](https://user-images.githubusercontent.com/62803763/131993976-25e72111-4ab3-4fe6-9e34-a5c921a7b759.PNG){: .align-center .open-new}

![react-deploy6](https://user-images.githubusercontent.com/62803763/131993983-d6ca422c-8a80-42b3-af9e-a5c865ae644d.PNG){: .align-center .open-new}

![react-deploy7](https://user-images.githubusercontent.com/62803763/131993990-3e28490b-2063-4853-8ca2-3ff9286aceb0.PNG){: .align-center .open-new}

![react-deploy8](https://user-images.githubusercontent.com/62803763/131993996-85ffe726-ea78-4007-88c8-57f9d4f44e71.PNG){: .align-center .open-new}

![react-deploy9](https://user-images.githubusercontent.com/62803763/131994002-fa22fc37-511c-483d-9db5-cc7c5cc45312.PNG){: .align-center .open-new}

![react-deploy10](https://user-images.githubusercontent.com/62803763/131994008-d6b42598-2077-4ae9-9797-c43d6559604c.PNG){: .align-center .open-new}

![react-deploy11](https://user-images.githubusercontent.com/62803763/131994013-ce0a6692-2e1a-4249-b4d3-975c41d669ee.PNG){: .align-center .open-new}

<br>

## 3. NginX로 React App 배포

- 추후 업로드

<br>

## 4. node.js express로 React App 배포

```bash
# terminal

$ npm i express
$ code .
```

<br>

```js
// server.js

const express = require("express");
const path = require("path");

const app = express();

app.use(express.static(path.join(__dirname, "build")));

app.get("*", (req, res) => {
  res.sendFile(path.join(__dirname, "build", "index.html"));
});

app.listen(9000);
```

<br>

```bash
# terminal

$ node server.js
```

<br>

## 5. Server Side Rendering 이해하기

- 서버에서 응답을 가져올 때, 기존처럼 static file만을 가져오는 것이 아니라, 먼저 서버에서 응답 값을 만들어서 내려주고, 그 후에 static file을 내려줌
- static file을 다 내려받고, React App을 브라우저에서 실행한 뒤에는 SPA처럼 동작
- React Component를 브라우저가 아니라 Node.js에서 사용
- ReactDOMServer.renderToString(&#60;App/&#62;);
  - 결과가 문자열
  - 이것을 응답으로 내려줌
- 라우팅, 리덕스와 같은 처리를 서버에서 진행하고 내려줌
- JSX가 포함된 React 코드를 서버에서 읽을 수 있도록 babel 설정을 해야 함

```js
// server.js

const express = require("express");
const path = require("path");
const ReactDOMServer = require("react-dom/server");
const React = require("react");
const fs = require("fs");

// <div>Hello</div>
console.log(
  ReactDOMServer.renderToString(React.createElement("div", null, "Hello"))
);

const app = express();

app.use(express.static(path.join(__dirname, "build")));

app.get("/test", (req, res) => {
  const ssr = ReactDOMServer.renderToString(
    React.createElement("div", null, "Hello")
  );
  const indexHtml = fs
    .readFileSync(path.join(__dirname, "build", "index.html"))
    .toString()
    .replace('<div id="root"></div>', `<div id="root">${ssr}</div>`);
  res.send();

  console.log(indexHtml);

  res.send(indexHtml);
});

app.get("*", (req, res) => {
  res.sendFile(path.join(__dirname, "build", "index.html"));
});

app.listen(9000);
```
