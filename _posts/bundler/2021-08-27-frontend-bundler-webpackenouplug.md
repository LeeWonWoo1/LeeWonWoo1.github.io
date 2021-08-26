---
title: "[Bundler] Webpack Entry, Output, Plugins"
excerpt: Webpack 프로젝트 세팅
categories:
- Bundler
tags:
- - Bundler
  - Web
  - NPM
  - Webpack
toc: true
toc_sticky: true
popular: true
date: '2021-08-27T02:00:00'
last_modified_at: 2021-08-27T02:00:00
---


## 1. 프로젝트 시작

```bash
# 프로젝트 생성

$ mkdir webpack-template-basic
$ cd webpack-template-basic
$ npm init -y
$ npm i -D webpack webpack-cli webpack-dev-server@next
```

<br>

```json
// package.json

"scripts": {
  "dev": "webpack-dev-server --mode development",
  "build": "webpack --mode production"
},

"devDependencies": {
  "webpack": "^5.51.1",  // Bundler가 동작하기 위한 핵심 패키지
  "webpack-cli": "^4.8.0",  // CLI를 지원하는 패키지
  "webpack-dev-server": "^4.0.0-rc.1"  // 페이지 자동 새로고침 패키지
}
```

<br>

```html
<!-- index.html -->

<head>
  <title>Hello Webpack!</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reset-css@5.0.1/reset.min.css"> <!-- reset.css -->
</head>

<body>
  <h1>Hello Webpack!!</h1>
</body>
```

<br>

```js
// js/main.js

console.log('Webpack!')
```


<br>

## 2. Entry, Output

```js
// webpack.config.js

// import
const path = require('path')  // path 전역 모듈

// export
module.exports = {
  entry: './js/main.js',  // 파일을 읽어들이기 시작하는 진입점 설정
  output: {    // 결과물(Bundle)을 반환하는 설정
    // path: path.resolve(__dirname, 'dist'),
    // filename: 'main.js',
    clean: true  // 새롭게 build 했을 때, 기존에 필요하지 않은 파일을 제거
  }
}
```

<br>

```bash
# terminal

$ npm run build
```


<br>

## 3. Plugins

```bash
# terminal

$ npm i -D html-webpack-plugin
```

<br>

```js
// webpack.config.js

const path = require('path')
const HtmlPlugin = require('html-webpack-plugin')

module.exports = {
  entry: './js/main.js',
  output: {
    clean: true
  },

  // 번들링 후 결과물의 처리 방식 등 다양한 플러그인들을 설정
  plugins: [
    new HtmlPlugin({
      template: './index.html'
    })
  ],
  devServer: {
    host: 'localhost'
  }
}
```

<br>

```bash
# terminal

$ npm run dev
```

<br>

![webpack1](https://user-images.githubusercontent.com/62803763/131008124-be95e4c1-7cef-467a-912f-336d9b9a468a.PNG){: .align-center .open-new}