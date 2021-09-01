---
title: "[React] Controlled, Uncontrolled Component"
excerpt: React Controlled, Uncontrolled Component
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
toc: true
toc_sticky: true
popular: true
date: "2021-09-01T23:30:00"
last_modified_at: 2021-09-01T23:30:00
---

## Controlled, Uncontrolled Component

- 상태를 가지고 있는 엘리먼트
  - input
  - select
  - textarea
  - ...
- 엘리먼트의 '상태'를 누가 관리하느냐
  - 엘리먼트를 가지고 있는 Component가 관리
    - Controlled
  - 엘리먼트의 상태를 관리하지 않고, 엘리먼트의 참조만 Component가 소유
    - Uncontrolled

<br>

### - Controlled Components

```jsx
// src/components/ControlledComponent.jsx

import React from "react";

class ControlledComponent extends React.Component {
  state = {
    value: "",
  };
  render() {
    const { value } = this.state;
    return (
      <div>
        <input value={value} onChange={this.change} />
        <button onClick={this.click}>전송</button>
      </div>
    );
  }

  change = (e) => {
    this.setState({ value: e.target.value });
  };

  click = () => {
    console.log(this.state.value);
  };
}

export default ControlledComponent;
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.scss";
import ControlledComponent from "./components/ControlledComponent";

function App() {
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <ControlledComponent />
      </header>
    </div>
  );
}
```

<br>

### - Uncontrolled Components

```jsx
// src/components/UncontrolledComponents.jsx
import React from "react";

class UncontorlledComponent extends React.Component {
  inputRef = React.createRef();

  render() {
    console.log("initial render", this.inputRef);
    return (
      <div>
        <input ref={this.inputRef} />
        <button onClick={this.click}>전송</button>
      </div>
    );
  }

  componentDidMount() {
    console.log("componentDidMount", this.inputRef);
  }

  click = () => {
    // input 엘리먼트의 현재 상태 값 (value) 를 꺼내서 전송
    // const input = document.querySelector("#my-input");
    // console.log(input.value);  // 지양
    console.log(this.inputRef.current.value);
  };
}

export default UncontrolledComponent;
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.scss";
import ControlledComponent from "./components/ControlledComponent";
import UncontrolledComponent from "./components/UncontrolledComponent";

function App() {
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <ControlledComponent />
        <UncontrolledComponent />
      </header>
    </div>
  );
}
```

<br>

![react-controll](https://user-images.githubusercontent.com/62803763/131693172-f21babbd-6be6-4de0-8228-06959b4c9f7f.PNG){: .align-center .open-new}
