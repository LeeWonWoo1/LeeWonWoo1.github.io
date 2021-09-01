---
title: "[React] Hooks & Context - 1"
excerpt: Basic Hooks, Custom Hooks
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
toc: true
toc_sticky: true
popular: true
date: "2021-09-02T00:00:00"
last_modified_at: 2021-09-02T00:00:00
---

## 1. Basic Hooks

- Component 사이에서 상태와 관련된 로직을 재사용하기 어려움
  - 컨테이너 방식 말고, 상태와 관련된 로직
- 복잡한 Component들은 이해하기 어려움
- Class는 사람과 기계를 혼동시킴
  - 컴파일 단계에서 코드를 최적화하기 어렵게 만듦
- this.state는 로직에서 레퍼런스를 공유하기 때문에 문제가 발생할 수 있음

```jsx
// src/components/Example1.jsx

import React from "react";

export default class Example1 extends React.Component {
  state = { count: 0 };

  render() {
    const { count } = this.state;
    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={this.click}>Click me</button>
      </div>
    );
  }

  click = () => {
    this.setState({ count: this.state.count + 1 });
  };
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example1 from "./components/Example1";

function App() {
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <Example1 />
      </header>
    </div>
  );
}
```

<br>

![react-hook2](https://user-images.githubusercontent.com/62803763/131696107-551f5c8e-1fdf-468d-a88f-91ca34639f85.PNG){: .align-center .open-new}

<br>

```jsx
// src/components/Example2.jsx

import React from "react";

export default function Example2() {
  const [count, setCount] = React.useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={click}>Click me</button>
    </div>
  );

  function click() {
    setCount(count + 1);
  }
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example1 from "./components/Example1";
import Example2 from "./components/Example2";

function App() {
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <Example1 />
        <Example2 />
      </header>
    </div>
  );
}
```

<br>

![react-hook1](https://user-images.githubusercontent.com/62803763/131695897-61233345-fb0b-4fb8-968e-051435b42f16.PNG){: .align-center .open-new}

<br>

```jsx
// src/components/Example3.jsx

import React from "react";

// useState => count
// useState => { count: 0 }
export default function Example3() {
  const [state, setState] = React.useState({ count: 0 });

  return (
    <div>
      <p>You clicked {state.count} times</p>
      <button onClick={click}>Click me</button>
    </div>
  );

  function click() {
    setState((state) => ({
      count: state.count + 1,
    }));
  }
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example1 from "./components/Example1";
import Example2 from "./components/Example2";
import Example3 from "./components/Example3";

function App() {
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <Example1 />
        <Example2 />
        <Example3 />
      </header>
    </div>
  );
}
```

<br>

![react-hook3](https://user-images.githubusercontent.com/62803763/131700983-cc2aed54-649e-4dd6-9c48-7ec279f467fa.PNG){: .align-center .open-new}

<br>

- useState
  - state를 대체 할 수 있음
- useEffect
  - Lifecycle 훅을 대체 할 수 있음
    - componentDidMount
    - componentDidUpdate
    - componentWillUnmount

```jsx
// src/components/Example4.jsx

import React from "react";

export default class Example4 extends React.Component {
  state = { count: 0 };

  render() {
    const { count } = this.state;
    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={this.click}>Click me</button>
      </div>
    );
  }

  componentDidMount() {
    console.log("componentDidMount", this.state.count);
  }

  componentDidUpdate() {
    console.log("componentDidUpdate", this.state.count);
  }

  click = () => {
    this.setState({ count: this.state.count + 1 });
  };
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example1 from "./components/Example1";
import Example2 from "./components/Example2";
import Example3 from "./components/Example3";
import Example4 from "./components/Example4";

function App() {
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <Example1 />
        <Example2 />
        <Example3 />
        <Example4 />
      </header>
    </div>
  );
}
```

<br>

![react-hook4](https://user-images.githubusercontent.com/62803763/131702033-e27e5e40-06a9-4aa8-805a-c0c2741a0d1b.PNG){: .align-center .open-new}

<br>

```jsx
// src/components/Example5.jsx

import React from "react";

export default function Example5() {
  const [count, setCount] = React.useState(0);

  React.useEffect(() => {
    console.log("componentDidMount");

    return () => {
      // cleanup
      // componentWillUnmount
    };
  }, []);

  React.useEffect(() => {
    console.log("componentDidMount & componentDidUpdate by count", count);

    return () => {
      // cleanup
      console.log("cleanup by count", count);
    };
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={click}>Click me</button>
    </div>
  );

  function click() {
    setCount(count + 1);
  }
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example1 from "./components/Example1";
import Example2 from "./components/Example2";
import Example3 from "./components/Example3";
import Example4 from "./components/Example4";
import Example5 from "./components/Example5";

function App() {
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <Example5 />
      </header>
    </div>
  );
}
```

<br>

![react-hook5](https://user-images.githubusercontent.com/62803763/131703641-edf02d91-d7ae-4c4d-b2e8-577e614299db.PNG){: .align-center .open-new}

<br>

## 2. Custom Hooks

```js
// src/hooks/useWindowWidth.js

import { useState, useEffect } from "react";

export default function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const resize = () => {
      setWidth(window.innerWidth);
    };

    window.addEventListener("resize", resize);

    return () => {
      window.removeEventListener("resize", resize);
    };
  }, []);

  return width;
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example5 from "./components/Example5";
import useWindowWidth from "./hooks/useWindowWidth";

function App() {
  const width = useWindowWidth();
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <Example5 />
        {width}
      </header>
    </div>
  );
}
```

<br>

![react-hook6](https://user-images.githubusercontent.com/62803763/131705386-5e15f3d6-3e1d-4e17-8823-f2f8e58c1639.PNG){: .align-center .open-new}

<br>

```jsx
// src/hocs/withHasMounted.jsx

import React from "react";

export default function withHasMounted(Component) {
  class NewComponent extends React.Component {
    state = {
      hasMounted: false,
    };
    render() {
      const { hasMounted } = this.state;
      return <Component {...this.props} hasMounted={hasMounted} />;
    }
    componentDidMount() {
      this.setState({ hasMounted: true });
    }
  }

  NewComponent.displayName = `withHasMounted(${Component.name})`;

  return NewComponent;
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import useWindowWidth from "./hooks/useWindowWidth";
import withHasMounted from "./hocs/withHasMounted";

function App({ hasMounted }) {
  const width = useWindowWidth();

  console.log(hasMounted);

  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        {width}
      </header>
    </div>
  );
}

export default withHasMounted(App);
```

<br>

![react-hook7](https://user-images.githubusercontent.com/62803763/131706440-c1b9d413-ad6f-4f44-a124-809b0bc593c6.PNG){: .align-center .open-new}

<br>

```js
// src/hooks/useHasMounted.js

import { useState } from "react";

export default function useHasMounted() {
  const [hasMounted, setHasMounted] = useState(false);

  useEffect(() => {
    setHasMounted(true);
  }, []);

  return hasMounted;
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import useWindowWidth from "./hooks/useWindowWidth";
import withHasMounted from "./hocs/withHasMounted";
import useHasMounted from "./hooks/useHasMounted";

function App({ hasMounted }) {
  const width = useWindowWidth();
  const hasMountedFromHooks = useHasMounted();

  console.log(hasMounted, hasMountedFromHooks);

  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        {width}
      </header>
    </div>
  );
}

export default withHasMounted(App);
```

<br>

![react-hook8](https://user-images.githubusercontent.com/62803763/131707145-50f06a59-8350-43ba-8ec7-82ee8219d8c0.PNG){: .align-center .open-new}
