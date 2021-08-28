---
title: "[Bundler] Webpack Static, Module, SCSS"
excerpt: Webpack Static, Module, SCSS
categories:
- Bundler
tags:
- - Bundler
  - Web
  - Node.js
  - Webpack
toc: true
toc_sticky: true
popular: true
date: '2021-08-27T02:30:00'
last_modified_at: 2021-08-27T02:30:00
---

## 1. 정적 파일 연결

[https://www.icoconverter.com/](https://www.icoconverter.com/){:target="_blank"}에서 원하는 이미지 변경
{: .notice--info}

- 원본 이미지와 변환된 이미지를 프로젝트 폴더 루트 경로에 복사
- static 폴더를 생성하고 favicon.ico와 원본 이미지를 이 폴더에 넣어줌
- static 폴더 안에 images 폴더를 생성하고 원본 이미지를 이 폴더에 넣어줌

<br>

![webpack2](https://user-images.githubusercontent.com/62803763/131009400-4431c426-e90b-4088-8202-9239b9d13c75.PNG){: .align-center .open-new}

<br>

```html
<!-- index.html -->

<body>
  <h1>Hello Webpack!!</h1>
  <img src="./images/bear.jpg" alt="Bear">
</body>
```

<br>

```bash
# terminal

$ npm i -D copy-webpack-plugin
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
  plugins: [
    new HtmlPlugin({
      template: './index.html'
    }),
    // static 폴더 안의 내용이 copy되어 dist폴더로 들어가는 plugin
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

```bash
# terminal

$ npm run dev
```


<br>

## 2. Module


static 폴더 안에 css 폴더 생성하고 main.css 파일 생성

```css
/* static/css/main.css */

body {
  background-color: orange;
}
```

<br>

```html
<!-- index.html -->

<head>
  <title>Hello Webpack!</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reset-css@5.0.1/reset.min.css">
  <link rel="stylesheet" href="./css/main.css">
</head>
```

<br>

```bash
# terminal

$ npm run dev
```


<br>

루트 경로에 css 폴더 생성하고 main.css 파일 생성

```css
/* css/main.css */

body {
  background-color: orange;
}
```

<br>

```js
// js/main.js

import '../css/main.css'

console.log('Webpack!')
```


<br>

CSS 파일을 읽을 수 있는 패키지 설치

```bash
# terminal

$ npm i -D css-loader style-loader
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
        test: /\.css$/,  // .css로 끝나는 파일
        use: [  // 순서 중요!!
          'style-loader',  // HTML의 style 태그에 해석된 내용을 삽입하는 용도
          'css-loader'  // Javascript에서 css파일을 해석하는 용도
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

```bash
# terminal

$ npm run dev
```


<br>

## 3. SCSS


루트 경로에 scss 폴더 생성하고 main.scss 파일 생성

```bash
# terminal

$ npm i -D sass-loader sass
```

<br>

```scss
/* scss/main.css */

$color--black: #000;
$color--white: #fff;

body {
  background-color: $color--black;
  h1 {
    color: $color--white;
    font-size: 50px;
  }
}
```

<br>

```js
// js/main.js

import '../scss/main.scss'

console.log('Webpack!')
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
        test: /\.s?css$/,  // .scss or .css로 끝나는 파일
        use: [
          'style-loader',
          'css-loader',
          'sass-loader'  // Webpack에서 scss파일을 읽어내는 용도
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

```bash
# terminal

$ npm run dev
```

<br>

![webpack3](https://user-images.githubusercontent.com/62803763/131016215-65f30e10-5e59-42f5-891a-15fddeeccae7.PNG){: .align-center .open-new}
