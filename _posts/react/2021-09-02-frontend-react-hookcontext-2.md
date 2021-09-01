---
title: "[React] Hooks & Context - 2"
excerpt: Additional Hooks, React Router Hooks
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
toc: true
toc_sticky: true
popular: true
date: "2021-09-02T01:00:00"
last_modified_at: 2021-09-02T01:00:00
---

## 1. Additional Hooks

- useReducer
  - 다수의 하위값을 포함하는 복잡한 정적 로직을 만드는 경우
  - 다음 state가 이전 state에 의존적인 경우
  - Redux를 안다면 쉽게 사용 가능

```jsx
// src/components/Example6.jsx

// reducer => state를 변경하는 로직이 담겨 있는 함수
const reducer = (state, action) => {
  if (action.type === "PLUS") {
    return {
      count: state.count + 1,
    };
  }
  return state;
};

// dispatch => action 객체를 넣어서 실행

// action => 객체이고 필수 프로퍼티로 type을 가짐

export default function Example6() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>You clicked {state.count} times</p>
      <button onClick={click}>Click me</button>
    </div>
  );

  function click() {
    dispatch({ type: "PLUS" });
  }
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example6 from "./components/Example6";
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
        <Example6 />
        {width}
      </header>
    </div>
  );
}

export default withHasMounted(App);
```

<br>

![react-hook9](https://user-images.githubusercontent.com/62803763/131708958-b49311eb-dd61-4caa-9434-5ce49bf8ba9d.PNG){: .align-center .open-new}

<br>

```jsx
// src/components/Example7.jsx

import { useState, useMemo } from "react";

function sum(persons) {
  console.log("sum...");
  return persons.map((person) => person.age).reduce((l, r) => l + r, 0);
}

export default function Example7() {
  const [value, setValue] = useState("");
  const [persons] = useState([
    { name: "LWW", age: 29 },
    { name: "Amy", age: 38 },
  ]);

  const count = useMemo(() => {
    return sum(persons);
  }, [persons]);

  const click = useCallback(() => {
    console.log(value);
  });

  return (
    <div>
      <input value={value} onChange={change} />
      <p>{count}</p>
      <button onClick={click}>click</button>
    </div>
  );

  function change(e) {
    setValue(e.target.value);
  }
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example7 from "./components/Example7";
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
        <Example7 />
        {width}
      </header>
    </div>
  );
}

export default withHasMounted(App);
```

<br>

![react-hook10](https://user-images.githubusercontent.com/62803763/131710620-4949b17b-2f2d-450d-b08e-517312c95d49.PNG){: .align-center .open-new}

<br>

```jsx
// src/components/Example8.jsx

import { useState } from "react";

export default function Example8() {
  const [value, setValue] = useState("");
  const input1Ref = createRef();
  const input2Ref = useRef();

  console.log(input1Ref.current, input2Ref.current);

  return (
    <div>
      <input value={value} onChange={change} />
      <input ref={input1Ref} />
      <input ref={input2Ref} />
    </div>
  );

  function change(e) {
    setValue(e.target.value);
  }
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example7 from "./components/Example8";
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
        <Example8 />
        {width}
      </header>
    </div>
  );
}

export default withHasMounted(App);
```

<br>

![react-hook11](https://user-images.githubusercontent.com/62803763/131711404-f4154991-91fd-4c07-808d-c2412f8721ac.PNG){: .align-center .open-new}

<br>

## 2. React Router Hooks

```jsx
// src/components/LoginButton.jsx

import { useHistory, withRouter } from "react-router-dom";

export default function LoginButton() {
  const history = useHistory();
  function login() {
    setTimeout(() => {
      history.push("/");
    }, 1000);
  }

  return <button onClick={login}>로그인하기</button>;
});
```

<br>

![react-router11](https://user-images.githubusercontent.com/62803763/131381551-73430641-c3a7-40a6-b7d4-1420dd9ab241.PNG){: .align-center .open-new}

![react-router12](https://user-images.githubusercontent.com/62803763/131381838-d753c963-ea27-4b3c-ae5a-791efc1510c5.PNG){: .align-center .open-new}

<br>

```jsx
// src/pages/Profile.jsx

export default function Profile() {
  const params = useParams();
  const id = params.id;
  console.log(id, typeof id);
  return (
    <div>
      <h2>Profile 페이지</h2>
      {id && <p>id는 {id}입니다.</p>}
    </div>
  );
}
```

<br>

![react-router10](https://user-images.githubusercontent.com/62803763/131379030-267ecaec-e468-4263-a740-7e6219ec12cb.PNG){: .align-center .open-new}
