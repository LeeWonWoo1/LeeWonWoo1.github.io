---
title: "[React] Component Styling - 2"
excerpt: Styled Component, React Shadow, Ant Design
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
    - CSS
    - SCSS
toc: true
toc_sticky: true
popular: true
date: "2021-09-01T21:00:00"
last_modified_at: 2021-09-01T21:00:00
---

## 1. Styled Components

- import 방식이 아니라 별도의 라이브러리를 이용해 스타일을 편하게 작업
- 오염되지 않는 스타일링

```bash
# terminal

$ npm i styled-components
```

<br>

```jsx
// src/components/StyledButton.jsx

import styled from "styled-components";

const StyledButton = styled.button`
  background: transparent;
  border-radius: 3px;
  border: 2px solid palevioletred;
  color: palevioletred;
  margin: 0 1em;
  padding: 0.25em 1em;
  font-size: 20px;
`;

export default StyledButton;
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import StyledButton from "./components/StyledButton";

function App() {
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <p>
          <StyledButton>버튼</StyledButton>
        </p>
      </header>
    </div>
  );
}
```

<br>

![react-styling3](https://user-images.githubusercontent.com/62803763/131675550-fee31db3-ee91-495e-a3b9-25572c9eabe8.PNG){: .align-center .open-new}

<br>

```jsx
// src/components/StyledButton.jsx

import styled from "styled-components";

const StyledButton = styled.button`
  background: transparent;
  border-radius: 3px;
  border: 2px solid palevioletred;
  color: palevioletred;
  margin: 0 1em;
  padding: 0.25em 1em;
  font-size: 20px;

  ${(props) =>
    props.primary &&
    css`
      background: palevioletred;
      color: white;
    `}
`;

export default StyledButton;
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import StyledButton from "./components/StyledButton";
import styled, { createGlobalStyle } from "styled-components";

const PrimaryStyledButton = styled(StyledButton)`
  background: palevioletred;
  color: white;
`;

const UppercaseButton = (props) => (
  <button {...props} children={props.children.toUpperCase()} />
);

const MyButton = (props) => (
  <button className={props.className} children={`MyButton ${props.children}`} />
);

const StyledMyButton = styled(MyButton)`
  background: transparent;
  border-radius: 3px;
  border: 2px solid ${(props) => props.color || "palevioletred"};
  color: ${(props) => props.color || "palevioletred"};
  margin: 0 1em;
  padding: 0.25em 1em;
  font-size: 20px;

  :hover {
    border: 2px solid red;
  }

  ::before {
    content: "@";
  }
`;

const GlobalStyle = createGlobalStyle`
button {
  color: yellow;
}
`;

function App() {
  return (
    <div className="App">
      <GlobalStyle />
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <p>
          <StyledButton>버튼</StyledButton>
          <StyledButton primary>버튼</StyledButton>
          <PrimaryStyledButton>버튼</PrimaryStyledButton>
          <StyledButton as="a" href="/">
            버튼
          </StyledButton>
          <StyledButton as={UppercaseButton}>button</StyledButton>
          <StyledMyButton>button</StyledMyButton>
          <StyledMyButton color="green">button</StyledMyButton>
        </p>
      </header>
    </div>
  );
}
```

<br>

![react-styling4](https://user-images.githubusercontent.com/62803763/131677881-15055984-38d5-4200-8989-1c5d040f35c6.PNG){: .align-center .open-new}

<br>

```jsx
// src/components/StyledA.jsx

import styled from "styled-components";

const StyledA = styled.a.attrs((props) => ({
  target: "_BLANK",
}))`
  color: ${(props) => props.color};
`;

export default StyledA;
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import StyledButton from "./components/StyledButton";
import styled, { createGlobalStyle } from "styled-components";
import StyledA from './components/StyledA";

const PrimaryStyledButton = styled(StyledButton)`
  background: palevioletred;
  color: white;
`;

const UppercaseButton = (props) => (
  <button {...props} children={props.children.toUpperCase()} />
);

const MyButton = (props) => (
  <button className={props.className} children={`MyButton ${props.children}`} />
);

const StyledMyButton = styled(MyButton)`
  background: transparent;
  border-radius: 3px;
  border: 2px solid ${(props) => props.color || "palevioletred"};
  color: ${(props) => props.color || "palevioletred"};
  margin: 0 1em;
  padding: 0.25em 1em;
  font-size: 20px;

  :hover {
    border: 2px solid red;
  }

  ::before {
    content: "@";
  }
`;

const GlobalStyle = createGlobalStyle`
button {
  color: yellow;
}
`;

function App() {
  return (
    <div className="App">
      <GlobalStyle />
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <p>
          <StyledButton>버튼</StyledButton>
          <StyledButton primary>버튼</StyledButton>
          <PrimaryStyledButton>버튼</PrimaryStyledButton>
          <StyledButton as="a" href="/">
            버튼
          </StyledButton>
          <StyledButton as={UppercaseButton}>button</StyledButton>
          <StyledMyButton>button</StyledMyButton>
          <StyledMyButton color="green">button</StyledMyButton>
          <StyledA href="https://google.com">태그</StyledA>
        </p>
      </header>
    </div>
  );
}
```

<br>

![react-styling5](https://user-images.githubusercontent.com/62803763/131678677-c798769e-e0e9-462e-9698-9512ec16e629.PNG){: .align-center .open-new}

<br>

## 2. React Shadow

- HTML안에 본래 HTML에 영향을 주지 않는 별도의 HTML 덩어리
- HTML에서 Shadow DOM을 이용해 오염되지 않도록 함

```bash
# terminal

$ npm i react-shadow
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import root from "react-shadow";

const styles = `
src/App.css 내용

p {
  color: yellow;
}
`;

function App() {
  return (
    <root.div>
      <div className="App">
        <header className="header">
          <img src={logo} className="logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
      <style stype="text/css">{styles}</style>
    </root.div>
  );
}
```

<br>

```js
// src/index.js

ReactDOM.render(
  <React.StrictMode>
    <App />
    <p>Hello</p>
  </React.StrictMode>
  document.getElementById("root")
);
```

<br>

![react-styling6](https://user-images.githubusercontent.com/62803763/131680616-1df60e94-5dfb-454a-b646-15b470839ebf.PNG){: .align-center .open-new}

<br>

## 3. Ant Design

[https://ant.design/](https://ant.design/){:target="\_blank"}
{: .notice--info}

```bash
# terminal

$ npm i antd
```

<br>

```js
// src/index.js

import "antd/dist/antd.css";
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import { Calendar } from "antd";

function App() {
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <Calendar />;
      </header>
    </div>
  );
}
```

<br>

![react-styling7](https://user-images.githubusercontent.com/62803763/131682127-1eecf66a-a19b-4985-afac-4b1826093993.PNG){: .align-center .open-new}

<br>

```bash
# terminal

$ npm install --save @ant-design/icons
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import { Calendar } from "antd";
import { GithubOutlined } from "@ant-design/icons";

function App() {
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <p>
          <GithubOutlined />
        </p>
        <Calendar />;
      </header>
    </div>
  );
}
```

<br>

![react-styling8](https://user-images.githubusercontent.com/62803763/131682865-9055f257-a2d9-4399-b908-74c4e30eed7b.PNG){: .align-center .open-new}

<br>

```js
// import { Row, Col } from 'antd';

import { Row, Col } from "antd";

function MyCol({ span }) {
  return (
    <Col span={span}>
      <div style={{ height: 50, backgroundColor: "red", opacity: 0.7 }} />
    </Col>
  );
}

// <Col span={24 중에 어느정도 차지할 지 정수} />
// <Row gutter={16 + 8n의 정수} />
export default function App() {
  return (
    <div className="App">
      <Row gutter={16}>
        <MyCol span={12} />
        <MyCol span={12} />
      </Row>
      <Row gutter={16}>
        <MyCol span={8} />
        <MyCol span={8} />
        <MyCol span={8} />
      </Row>
      <Row gutter={16}>
        <MyCol span={6} />
        <MyCol span={6} />
        <MyCol span={6} />
        <MyCol span={6} />
      </Row>
    </div>
  );
}
```

<br>

![react-styling9](https://user-images.githubusercontent.com/62803763/131684209-26c8b2bf-a740-48c3-9cbe-fe333653a7fd.PNG){: .align-center .open-new}

<br>

![react-styling10](https://user-images.githubusercontent.com/62803763/131684567-6ca1e51f-4f0a-4643-80c1-89b5aa2c82f1.PNG){: .align-center .open-new}

<br>

```js
// import { Row, Col } from 'antd';

import { Row, Col } from "antd";

function MyCol({ span, offset }) {
  return (
    <Col span={span} offset={offset}>
      <div style={{ height: 50, backgroundColor: "red", opacity: 0.7 }} />
    </Col>
  );
}

// <Col offset={24 중 건너띄고 싶은 정수} />
export default function App() {
  return (
    <div className="App">
      <Row gutter={16}>
        <MyCol span={12} offset={12} />
      </Row>
      <Row gutter={16}>
        <MyCol span={8} />
        <MyCol span={8} offset={8} />
      </Row>
      <Row gutter={16}>
        <MyCol span={6} />
        <MyCol span={6} offset={3} />
        <MyCol span={6} offset={3} />
      </Row>
    </div>
  );
}
```

<br>

![react-styling11](https://user-images.githubusercontent.com/62803763/131685028-7ee8c083-2363-4bc0-a0f0-52ecfa8fad5c.PNG){: .align-center .open-new}

<br>

```js
// import { Row, Col } from 'antd';

import { Row, Col } from "antd";

function MyCol({ span, offset }) {
  const opacity = Math.round(Math.random() * 10) / 10;
  return (
    <Col span={span} offset={offset}>
      <div style={{ height: 50, backgroundColor: "red", opacity }} />
    </Col>
  );
}

// <Row type="flex" justify="좌우정렬" align="위아래정렬" />
export default function App() {
  return (
    <div className="App">
      <Row
        style={{
          height: 300,
        }}
        justify="start"
        align="top"
      >
        <MyCol span={4} />
        <MyCol span={4} />
        <MyCol span={4} />
        <MyCol span={4} />
      </Row>
    </div>
  );
}
```

<br>

![react-styling12](https://user-images.githubusercontent.com/62803763/131685588-787589c8-2264-4806-ac85-4520afe130f8.PNG){: .align-center .open-new}
