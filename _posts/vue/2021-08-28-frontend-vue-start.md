---
title: "[Vue.js] 개요, 시작"
excerpt: 
categories:
- Vue
tags:
- - Vue
  - Web
  - NPM
toc: true
toc_sticky: true
popular: true
date: '2021-08-28T01:30:00'
last_modified_at: 2021-08-28T01:30:00
---

## 1. Vue.js란?

- 사용자 인터페이스를 만들기 위한 프로그레시브 프레임워크
- 점진적 채택할 수 있도록 설계
- 다른 라이브러리나 기존 프로젝트와의 통합이 쉬움
- 현대적 도구 및 지원 라이브러리와 함께 사용하면 정교한 단일 페이지 응용프로그램을 완벽하게 지원할 수 있음
- 반응성이 뛰어남


<br>

## 2. Vue.js 시작 방법


### - CDN

- 프로토 타이핑 또는 학습 목적으로 사용할 시 CDN으로 간편하게 사용

```html
<!-- html -->

<script src="https://unpkg.com/vue@next"></script>
<div id="app">
  <h1>{{ message }}</h1>
</div>
```

<br>

```js
// js

Vue.createApp({
  data() {
    return {
      message: 'Hello Vue!'
    }
  }
}).mount('#app')
```


<br>

### - CLI

- 단일 페이지 App을 빠르게 구축할 수 있는 공식 CLI 제공

```bash
# terminal

$ npm i -g @vue/cli
$ vue create vue3-test
버전 선택
$ cd vue3-test
$ code .
```

<br>

- 코드 가독성을 위해 Vetur 확장 프로그램 설치

![vue1](https://user-images.githubusercontent.com/62803763/131162619-1260cf03-2c13-4ad7-8f41-e9e6654c86ef.PNG){: .align-center .open-new}

```vue
// App.vue 구성

// HTML
<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>  // 제거하고 시작
</template>

// JavaScript
<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

// CSS
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```


<br>

### - Webpack

```bash
# terminal

$ npx degit LeeWonWoo1/webpack-template-basic vue3-webpack-template
$ cd vue3-webpack-template
$ code . -r
$ npm i vue@next
$ npm i -D vue-loader@next vue-style-loader @vue/compiler-sfc
```

<br>

```js
// webpack.config.js

const path = require('path')
const HtmlPlugin = require('html-webpack-plugin')
const CopyPlugin = require('copy-webpack-plugin')
const { VueLoaderPlugin } = require('vue-loader')

module.exports = {
  resolve: {
    extensions: ['.js', '.vue']  // js, vue 확장자를 명시하지 않아도 에러 발생 막음
  },
  entry: './src/main.js',
  output: {
    clean: true
  },
  module: {
    rules: [
      {
        test: /\.vue$/,  // .vue로 끝나는 파일
        use: 'vue-loader'  // Webpack에서 vue 파일을 읽어내는 용도
      },
      {
        test: /\.s?css$/,
        use: [
          // 순서 중요!
          'vue-style-loader',  // Vue 파일 내의 style 태그를 해석해서 동작시키는 용도
          'style-loader',
          'css-loader',
          'postcss-loader',
          'sass-loader'
        ]
      },
      {
        test: /\.js$/,
        use: [
          'babel-loader'
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
    }),
    new VueLoaderPlugin()  // 생성자 함수로 호출
  ],
  devServer: {
    host: 'localhost'
  }
}
```

<br>

- 루트 경로에 src 폴더를 생성하고
- src 폴더 안에 main.js 파일 만들기
- src 폴더 안에 App.vue 파일 만들기
- 기존 js 폴더는 삭제

```vue
// App.vue

<template>
  <h1>{{ message }}</h1>
</template>

<script>
export default {
  data() {
    return {
      message: "Hello Vue!!",
    };
  },
};
</script>
```

<br>

```js
// main.js

import { createApp } from 'vue'
import App from './App'

createApp(App).mount('#app')
```

<br>

```html
<!-- index.html -->

<body>
  <div id="app"></div>
</body>
```

<br>

```bash
# terminal

$ npm run dev
```

<br>

![vue2](https://user-images.githubusercontent.com/62803763/131166398-3f601b46-7609-45d3-92d2-5d552c69c2ee.PNG){: .align-center .open-new}

<br>

- 기존 static 폴더 내부의 images 폴더를 src 폴더 내부로 이동
- images 폴더의 이름을 assets로 변경
- src 폴더 내부에 components 폴더 생성
- components 폴더 내부에 HelloWorld.vue 파일 생성

<br>

![vue3](https://user-images.githubusercontent.com/62803763/131167339-b53403b7-5219-44f1-9b4c-37d1a7f32c3b.PNG){: .align-center .open-new}

<br>

```bash
# terminal

$ npm i -D file-loader
```

<br>

```js
// webpack.config.js

const path = require('path')
const HtmlPlugin = require('html-webpack-plugin')
const CopyPlugin = require('copy-webpack-plugin')
const { VueLoaderPlugin } = require('vue-loader')

module.exports = {
  resolve: {
    extensions: ['.js', '.vue'],
    alias: {  // 경로 별칭
      '~': path.resolve(__dirname, 'src'),
      'assets': path.resolve(__dirname, 'src/assets')
    }  
  },
  entry: './src/main.js',
  output: {
    clean: true
  },
  module: {
    rules: [
      {
        test: /\.vue$/,
        use: 'vue-loader'
      },
      {
        test: /\.s?css$/,
        use: [
          'vue-style-loader',
          'style-loader',
          'css-loader',
          'postcss-loader',
          'sass-loader'
        ]
      },
      {
        test: /\.js$/,
        use: [
          'babel-loader'
        ]
      },
      {
        test: /\.(png|jpe?g|gif|webp)$/,  // png, jpg, jpeg, git, webp로 끝나는 파일
        use: 'file-loader'
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
    }),
    new VueLoaderPlugin()
  ],
  devServer: {
    host: 'localhost'
  }
}
```

<br>

```vue
// HelloWorld.vue

<template>
  <img src="~assets/bear.jpg" alt="Bear" />
</template>
```

<br>

```vue
// App.vue

<template>
  <h1>{{ message }}</h1>
  <HelloWorld />
</template>

<script>
import HelloWorld from "~/components/HelloWorld";

export default {
  components: {
    HelloWorld,
  },
  data() {
    return {
      message: "Hello Vue!!",
    };
  },
};
</script>
```

<br>

![vue4](https://user-images.githubusercontent.com/62803763/131168909-7a0cdfaf-34f1-4492-8599-8b3d62c3500d.PNG){: .align-center .open-new}