---
title: "[React] Component를 만드는 법"
excerpt: React Component를 만들기
categories:
- React
tags:
- - React
  - Web
  - Node.js
toc: true
toc_sticky: true
popular: true
date: '2021-08-29T02:30:00'
last_modified_at: 2021-08-29T02:30:00
---

## 1. Component를 만드는 법

- Hooks **이전**
    - Component 내부에 상태가 있다면 : class
    - Component 내부에 상태가 없다면
        - Lifecycle을 사용해야 한다면 : class
        - Lifecycle에 관계 없다면 : function
- Hooks **이후**
    - class
    - function

```js
import React from 'react';

// Class Component 정의
class ClassComponent extends React.Component {
  render() {
    return <div>Hello</div>;
  }
}

// 사용
<ClassComponent />
```

<br>

```js
import React from 'react';

// Function Component 정의 1
function FunctionComponent() {
  return <div>Hello</div>;
}

// Function Component 정의 2
const FunctionComponent = () => <div>Hello</div>;

// 사용
<FunctionComponent />
```


<br>

## 2. React.createElement로 Component 만들기

```js
// React.createElement 요소

React.createElement(
  type, // 태그 이름 문자열 | React Component | React.Fragment
  [props],  // React Component에 넣어주는 데이터 객체
  [...children]  // 자식으로 넣어주는 요소들
);
```


<br>

### - 태그 이름 문자열 type

```html
<!-- index.html -->

<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script type="text/javascript">
    console.log(React);
    console.log(ReactDOM);

    // 1. 태그 이름 문자열 type
    // <h1>type이 "태그 이름 문자열" 입니다.</h1>
    ReactDOM.render(
      React.createElement('h1', null, `type이 "태그 이름 문자열" 입니다.`),
      document.querySelector('#root')
    );
  </script>
</body>
```

<br>

![react-component1](https://user-images.githubusercontent.com/62803763/131227087-b313c01f-196c-452b-a43d-595136c41e7a.PNG){: .align-center .open-new}


<br>

### - React Component type

```html
<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script type="text/javascript">
    console.log(React);
    console.log(ReactDOM);

    // 2. React Component type
    const Component = () => {
      return React.createElement('p', null, `type 이 "React Component 입니다."`);
    }

    // <Component></Component> => <Component /> => <p>type 이 "React Component 입니다.</p>
    ReactDOM.render(
      React.createElement(Component, null, null), document.querySelector('#root')
    );
  </script>
</body>
```

<br>

![react-component2](https://user-images.githubusercontent.com/62803763/131227279-da0db5ba-8948-49cf-b4f9-f72ea2bc93ef.PNG){: .align-center .open-new}


<br>

### - React.Fragment

```html
<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script type="text/javascript">
    console.log(React);
    console.log(ReactDOM);

    // 3. React.Fragment
    ReactDOM.render(
      React.createElement(React.Fragment, null, 
        `type 이 "React Fragment" 입니다.`,
        `type 이 "React Fragment" 입니다.`,
        `type 이 "React Fragment" 입니다.`
      ),
      document.querySelector('#root')
    );
  </script>
</body>
```

<br>

![react-component3](https://user-images.githubusercontent.com/62803763/131227521-3d43a82f-6959-4624-ad80-6488566e7c4b.PNG){: .align-center .open-new}


<br>

### - 복잡한 React Element 모임(createElement 한계)

- 정상작동 하지만, 가독성이 매우 떨어짐

```html
<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script type="text/javascript">
    console.log(React);
    console.log(ReactDOM);

    // 4. 복잡한 React Element 모임(createElement 한계)
    // <div>
    //   <div>
    //     <h1>주제</h1>
    //     <ul>
    //       <li>React</li>
    //       <li>Vue</li>
    //     </ul>
    //   </div>
    // </div>
    
    ReactDOM.render(
      React.createElement(
        'div', 
        null, 
        React.createElement(
          'div', 
          null, 
          React.createElement('h1', null, "주제"),
          React.createElement(
            'ul', 
            null, 
            React.createElement('li', null, "React"),
            React.createElement('li', null, 'Vue')
          )
        )
      ),
      document.querySelector('#root')
    )
  </script>
```

<br>

![react-component4](https://user-images.githubusercontent.com/62803763/131227764-00f56284-7357-444a-be84-41a14b6fe25a.PNG){: .align-center .open-new}


<br>

## 3. JSX

- JSX 문법으로 작성된 코드는 순수한 JavaScript로 Compile하여 사용
- Babel 사용
    - [https://babeljs.io/setup#installation](https://babeljs.io/setup#installation){:target="_blank"}
- JSX를 사용하는 이유
    - React.createElement보다 가독성 측면에서 압도적
    - babel과 같은 compile 과정에서 문법적 오류를 인지하기 쉬움

```html
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<script type="text/babel">
```

<br>

```html
<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    console.log(React);
    console.log(ReactDOM);

    // 우리가 작성한 어떤 코드 => 순수하게 실행할 수 있는 JavaScript
    // babel
    ReactDOM.render(
      <div>
        <div>
          <h1>주제</h1>
          <ul>
            <li>React</li>
            <li>Vue</li>
          </ul>
        </div>
      </div>,
      document.querySelector('#root')
    );
  </script>
</body>
```

<br>

![react-component4](https://user-images.githubusercontent.com/62803763/131227764-00f56284-7357-444a-be84-41a14b6fe25a.PNG){: .align-center .open-new}


<br>

### - JSX 문법

- 최상위 요소가 하나여야 함
- 최상위 요소 리턴하는 경우, ()로 감싸야 함
- 자식들을 바로 Rendering하고 싶으면, <>자식들</>를 사용 => Fragment
- JavaScript 표현식을 사용하려면, {표현식}을 이용
- if문은 사용할 수 없음
    - 삼항 연산자 혹은 && 사용
- style을 이용해 inline 스타일링 가능
- class 대신 className을 사용해 class를 적용할 수 있음
- 자식요소가 있으면 꼭 닫아야 하고, 자식요소가 없으면 열면서 닫아야 함
    - &#60;p&#62;abc&#60;/p&#62;
    - &#60;br /&#62;