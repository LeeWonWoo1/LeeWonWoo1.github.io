---
title: "[Bundler] Webpack Autoprefixer, Babel"
excerpt: Webpack Autoprefixer, Babel
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
date: '2021-08-27T03:30:00'
last_modified_at: 2021-08-27T03:30:00
---

## 1. Autoprefixer

- Autoprefixer는 공급 업체 접두사(Vender Prefix)를 자동으로 붙여줄 수 있는 패키지
- CSS 스타일 보험
- Vender Prefix는 모든 브라우저에서 CSS의 기능을 동일하게 사용하기 위하여 브라우저의 제조사별 접두어를 CSS에 표기하는 것

```bash
# terminal

$ npm i -D postcss autoprefixer postcss-loader
```

<br>

```js
// webpack.config.js

const path = require('path')
const HtmlPlugin = require('html-webpack-plugin')
const CopyPlugin = require('copy-webpack-plugin')

module.exports = {
  entry: './js/main.js',
  output: {
    clean: true
  },

  module: {
    rules: [
      {
        test: /\.s?css$/,
        use: [
          'style-loader',
          'css-loader',
          'postcss-loader',  // sass-loader롤 통해 해석된 내용에 공급업체 접두사를 적용하는 용도
          'sass-loader'
        ]
      }
    ]
  },
  plugins: [
    new HtmlPlugin({
      template: './index.html'
    }),
    new CopyPlugin({
      patterns: [
        { from: 'static' }
      ]
    })
  ],
  devServer: {
    host: 'localhost'
  }
}
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
// .postcssrc.js

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
    font-size: 50px;
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

![webpack4](https://user-images.githubusercontent.com/62803763/131019905-29a20efd-eede-4820-9b01-89e651fcee37.PNG){: .align-center .open-new}

![webpack5](https://user-images.githubusercontent.com/62803763/131019993-66708a01-cbb7-43aa-8b2e-6c7001b197f4.PNG){: .align-center .open-new}


<br>

## 2. Babel

- 컴파일러
- 최신의 문법으로 만든 Javascript 코드를 구형 브라우저에서도 동작할 수 있는 ES5 버전으로 컴파일 해줌

```bash
# terminal

$ npm i -D @babel/core @babel/preset-env @babel/plugin-transform-runtime
$ npm i -D babel-loader
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
// webpack.config.js

const path = require('path')
const HtmlPlugin = require('html-webpack-plugin')
const CopyPlugin = require('copy-webpack-plugin')

module.exports = {
  entry: './js/main.js',
  output: {
    clean: true
  },
  module: {
    rules: [
      {
        test: /\.s?css$/,
        use: [
          'style-loader',
          'css-loader',
          'postcss-loader',
          'sass-loader'
        ]
      },
      {
        test: /\.js$/,  // .js로 끝나는 파일
        use: [
          'babel-loader'  // Webpack에서 js파일을 읽어내는 용도
        ]
      }
    ]
  },
  plugins: [
    new HtmlPlugin({
      template: './index.html'
    }),
    new CopyPlugin({
      patterns: [
        { from: 'static' }
      ]
    })
  ],
  devServer: {
    host: 'localhost'
  }
}
```
