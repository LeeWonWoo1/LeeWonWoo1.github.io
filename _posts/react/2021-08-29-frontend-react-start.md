---
title: "[React] 개요, 라이브러리"
excerpt: React 개요, 라이브러리
categories:
- React
tags:
- - React
  - Web
  - Node.js
toc: true
toc_sticky: true
popular: true
date: '2021-08-29T00:30:00'
last_modified_at: 2021-08-29T00:30:00
---

## 1. React Keyword


### - React vs Angular vs Vue

- React
    - JavaScript library for building user interfaces
    - User Interface를 표현하고, 동작하는 것에 초점
    - View를 다루는 Library
    - 오직 랜더링과 업데이트에만 관여되는 라이브러리
        - HTTP Client나 Style에 대한 기능들이 포함되지 않음
    - Library 지향
- Angular
    - 어떤 플랫폼에서도 하나의 코드 베이스로 결과물을 낼 수 있음
    - Full Development Story
    - 전반적인 모든 기능 제공(클라이언트, 인증 등)
    - Full Framework 지향
- Vue.js
    - Progressive JavaScript Framework
    - React처럼 View를 다루는 Library로 쓸 수 있음
    - Angular처럼 여러가지 생태계를 끌어와서 전반적인 기능 제공할 수 있음
    - Library처럼도, Framework처럼도 쓸 수 있음


<br>

### - Component

- 컴포넌트 기반의 개발
    - 독립적인 코드 블럭(HTML, CSS, JavaScript)
    - 작업의 단위

```html
<!-- HTML Element -->

<!-- 이미 정의되어 있는 Element -->
<img src="이미지 주소" />
<button class="클래스">버튼</button>
```

<br>

```html
<!-- 내가 만든 Component -->

<!-- HTML, CSS, JavaScript를 합쳐서 내가 만든 일종의 태그 -->
<사용자지정이름 name="LWW" />
<사용자지정이름 prop={false}>내용</사용자지정이름>
```


<br>

### - Virtual DOM

- **DOM을 직접 다루지 않음**

* DOM을 직접 제어하는 경우
    * 바뀐 부분만 정확히 바꿔야 함
* DOM을 직접 제어하지 않는 경우
    * 가상의 DOM Tree를 사용해서 이전 상태와 이후 상태를 비교하여, 바뀐 부분을 찾아내서 자동으로 바꿈


<br>

### - JSX

- 치환되는 템플릿이 아니라 순수한 JS로 transpile되는 문법(Babel, TypeScript)


<br>

### - Client Side Rendering & Server Side Rendering

1. 특정 웹 서비스에 접속하면 HTML이 다운로드
2. HTML이 화면에 보이면서 HTML 내부의 DOM요소가 보이거나, 스타일이 적용됨

> 이때 React는 JavaScript로 이루어진 하나의 커다란 웹 어플리케이션<br>
> 이 웹 어플리케이션은 JS가 전체 다운로드 되어야 실행 가능

#### @1. CSR

1. HTML 다운로드 시 빈 껍데기의 HTML이 내려옴
2. HTML 안에 있는 JS 파일을 다시 요청
3. JS 파일 안에는 React 웹 어플리케이션 전체가 들어있음
4. JS 앱을 다시 다운로드 받음
5. 다운로드 받은 후에 스크립트가 브라우저에서 로드, 실행됨
6. 이렇게 실행되면 이제서야 React 웹 어플리케이션이 실행됨
7. React가 실행되면, React Component들이 화면에 그려짐
8. 이때 화면이 보이고, 유저가 인터렉션이 가능함

> JS가 전부 다운로드 되어 React 애플리케이션이 정상 실행되기 전까지 화면이 보이지 않음<br>
> JS가 전부 다운로드 되어 React 애플리케이션이 정상 실행된 후, 화면이 보이면서 유저가 인터렉션 가능<br>
> SSR을 활용하지 않는다면 React는 기본적으로 CSR로 동작

#### @2. SSR

1. 최초에 이미 HTML로 표현되어 있는 HTML을 다운
2. HTML 안의 JS를 다시 요청하는 과정에서는 HTML의 구성요소가 Render되고 있기 때문에 화면이 보임
3. 대신 화면 안의 동작들은 JS가 실행되지 않았기 때문에 동작하지 않음
4. 유저는 찰나의 순간에 동작하지 않는 Render된 결과물을 볼 수 있음
5. 이 결과물을 보는 중간에 JS가 다운로드 됨
6. JS에 React 앱이 다운로드 되고, 소스코드를 실행하면 React가 실행됨
7. React 앱이 실행되면 실제로 JS를 통해 Component가 HTML 상에 다시 동작하는 순간부터 유저가 동작할 수 있음

> JS가 전부 다운로드 되지 않아도, 일단 화면은 보이지만 유저가 사용할 수 없음<br>
> JS가 전부 다운로드 되어 React 어플리케이션이 정상 실행된 후, 유저가 사용 가능<br>
> 유저가 찰나의 화면을 먼저 보는 것이 의미 있다면 SSR 기능 활용


<br>

## 2. Library

- React 핵심 모듈로 React가 하는 일 알아보기

```js
// 1. React Component -> HTMLElement 연결
import ReactDOM from 'react-dom';

// 2. React Component 만들기
import React from 'react';
```

<br>

- { React Component } - JS, JSX ==> &#60; HTMLElement &#62;
    - ReactDOM 라이브러리 이용

```js
ReactDOM.render(
  <HelloMessage name="LWW" />,
  document.getElementById('hello-example')
);

class HelloMessage extends React.Component {
  render() {
    return (
      <div>
        Hello {this.props.name}
      </div>
    )
  }
}
```

<br>

- { React Component } 만들 때 사용하는 API
    - [https://ko.reactjs.org/docs/react-api.html](https://ko.reactjs.org/docs/react-api.html){:target="_blank"}
- React, ReactDOM Library를 CDN을 통해 사용해보기
    - [https://ko.reactjs.org/docs/cdn-links.html](https://ko.reactjs.org/docs/cdn-links.html){:target="_blank"}

```bash
# terminal

$ mkdir what-is-react
$ cd what-is-react
$ npm init -y
$ code .
$ npx serve
```

<br>

![react-cdn1](https://user-images.githubusercontent.com/62803763/131225496-d0ae1cc3-4061-464b-906d-a97a94bd580a.PNG){: .align-center .open-new}

<br>

```html
<!-- index.html -->

<body>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script type="text/javascript">
    console.log(React);
    console.log(ReactDOM);
  </script>
</body>
```

<br>

![react-cdn2](https://user-images.githubusercontent.com/62803763/131225506-f15f6d6e-f542-43ab-a07e-3d03111115be.PNG){: .align-center .open-new}

<br>

- Component를 활용한 프론트엔드
    - Component를 정의하고, 실제 DOM에 Component를 그려줌

```html
<!-- index.html -->

<head>
  <title>Example</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      border: 0;
    }
    #root p {
      color: white;
      font-size: 20px;
      background-color: royalblue;
      text-align: center;
      width: 100px;
    }
    #btn_plus {
      background-color: orange;
      border: 2px solid #000;
      font-size: 15px;
      width: 200px;
    }
  </style>
</head>

<body>
  <div id="root"></div>
  <button id="btn_plus">+</button>

  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>

  <script type="text/javascript">
    const component = {
      message: 'init',
      count: 0,
      render() {
        return `<p>${this.message} : ${this.count}</p>`;
      }
    };

    function render(rootElement, component) {
      rootElement.innerHTML = component.render();
    }

    // 초기화 
    render(document.querySelector('#root'), component);

    document.querySelector('#btn_plus').addEventListener('click', () => {
      component.message = 'update';
      component.count = component.count + 1;
      render(document.querySelector('#root'), component);
    });
  </script>
</body>
```

<br>

![react-cdn3](https://user-images.githubusercontent.com/62803763/131225967-a6abd834-55b6-4a2a-8df8-15536b9ca893.PNG){: .align-center .open-new}

<br>

- React를 활용한 프론트엔드

```html
<!-- index.html -->

<body>
  <div id="root"></div>
  <button id="btn_plus">+</button>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script type="text/javascript">
    console.log(React);
    console.log(ReactDOM);

    const Component = props => {
      return React.createElement('p', null, `${props.message} : ${props.count}`);
    }

    ReactDOM.render(
      React.createElement(Component, {message: 'init', count: 0}, null), 
      document.querySelector('#root'));

    document.querySelector('#btn_plus').addEventListener('click', () => {
      ReactDOM.render(
        React.createElement(
          Component, 
          {message: 'update', count: 77}, 
          null
        ), 
        document.querySelector('#root')
      );
    });
  </script>
</body>
```

<br>

![react-cdn4](https://user-images.githubusercontent.com/62803763/131226266-9463daaf-832a-4b3d-9f45-a50914360def.PNG){: .align-center .open-new}