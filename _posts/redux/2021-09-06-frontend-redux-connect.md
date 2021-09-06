---
title: "[Redux] Redux를 React에 연결"
excerpt: Redux Basic - 4
categories:
  - Redux
tags:
  - - Redux
    - Web
    - Node.js
    - React
toc: true
toc_sticky: true
popular: true
date: "2021-09-06T23:00:00"
last_modified_at: 2021-09-06T23:00:00
---

## 1. react-redux 안쓰고 연결하기

- 단일 store를 만들고, subscribe와 getState를 이용하여, 변경되는 state 데이터를 얻어, props로 계속 아래로 전달
- componentDidMount : subscribe
- componentWillUnmount : unsubscribe

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import TodoList from "./components/TodoList";
import TodoForm from "./components/TodoForm";

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <TodoList />
        <TodoForm />
      </header>
    </div>
  );
}

export default App;
```

<br>

```js
// src/index.js

import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";
import store from "./redux/store";
import ReduxContext from "./contexts/ReduxContext";

ReactDOM.render(
  <React.StrictMode>
    <ReduxContext.Provider value={store}>
      <App />
    </ReduxContext.Provider>
  </React.StrictMode>,
  document.getElementById("root")
);

reportWebVitals();
```

<br>

```js
// src/contexts/ReduxContext.js

import { createContext } from "react";

const ReduxContext = createContext();

export default ReduxContext;
```

<br>

```js
// src/hooks/useReduxState.js

import { useContext, useEffect, useState } from "react";
import ReduxContext from "../contexts/ReduxContext";

export default function useReduxState() {
  const store = useContext(ReduxContext);
  const [state, setState] = useState(store.getState());

  useEffect(() => {
    const unsubscribe = store.subscribe(() => {
      setState(store.getState());
    });
    return () => {
      unsubscribe();
    };
  }, [store]);

  return state;
}
```

<br>

```js
// src/hooks/useReduxDispatch.js

import { useContext } from "react";
import ReduxContext from "../contexts/ReduxContext";

export default function useReduxDispatch() {
  const store = useContext(ReduxContext);

  return store.dispatch;
}
```

<br>

```jsx
// src/components/TodoList.jsx

import useReduxState from "../hooks/useReduxState";

export default function TodoList() {
  const state = useReduxState();

  return (
    <ul>
      {state.todos.map((todo) => {
        return <li>{todo.text}</li>;
      })}
    </ul>
  );
}
```

<br>

```jsx
// src/components/TodoForm.jsx

import { useRef } from "react";
import useReduxDispatch from "../hooks/useReduxDispatch";
import { addTodo } from "../redux/actions";

export default function TodoForm() {
  const inputRef = useRef();
  const dispatch = useReduxDispatch();

  return (
    <div>
      <input ref={inputRef} />
      <button onClick={click}>추가</button>
    </div>
  );

  function click() {
    dispatch(addTodo(inputRef.current.value));
  }
}
```

![redux-connect1](https://user-images.githubusercontent.com/62803763/132232973-7257e44b-0172-422c-a99e-17ba44742597.PNG){: .align-center .open-new}

<br>

## 2. react-redux 쓰고 연결하기

**react-redux**
<br>

- Provider Component를 제공
- connect 함수를 통해 컨테이너를 만들어 줌
  - 컨테이너는 스토어의 state와 dispatch(액션)을 연결한 component에 props로 넣어주는 역할
  - 필요한 것은
    - 어떤 state를 어떤 props에 연결할 것인지에 대한 정의
    - 어떤 dispatch(액션)을 어떤 props에 연결할 것인지에 대한 정의
    - 그 props를 보낼 component를 정의

```bash
# terminal

$ npm i react-redux
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import TodoListContainer from "./containers/TodoListContainer";
import TodoFormContainer from "./containers/TodoFormContainer";

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <TodoListContainer />
        <TodoFormContainer />
      </header>
    </div>
  );
}

export default App;
```

<br>

```js
// src/index.js

import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";
import store from "./redux/store";
import { Provider } from "react-redux";

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById("root")
);

reportWebVitals();
```

<br>

```jsx
// src/components/TodoList.jsx

export default function TodoList({ todos }) {
  return (
    <ul>
      {todos.map((todo) => {
        return <li>{todo.text}</li>;
      })}
    </ul>
  );
}
```

<br>

```jsx
// src/components/TodoForm.jsx

import { useRef } from "react";

export default function TodoForm({ add }) {
  const inputRef = useRef();

  return (
    <div>
      <input ref={inputRef} />
      <button onClick={click}>추가</button>
    </div>
  );

  function click() {
    add(inputRef.current.value);
  }
}
```

<br>

```jsx
// src/containers/TodoListContainer.jsx

import { useSelector } from "react-redux";
import TodoList from "../components/TodoList";

function TodoListContainer() {
  const todos = useSelector((state) => state.todos);

  return <TodoList todos={todos} />;
}

export default TodoListContainer;
```

<br>

```jsx
// src/containers/TodoFormContainer.jsx

import { useCallback } from "react";
import { useDispatch } from "react-redux";
import TodoForm from "../components/TodoForm";
import { addTodo } from "../redux/actions";

export default function TodoFormContainer() {
  const dispatch = useDispatch();

  const add = useCallback(
    (text) => {
      dispatch(addTodo(text));
    },
    [dispatch]
  );

  return <TodoForm add={add} />;
}
```

<br>

![redux-connect2](https://user-images.githubusercontent.com/62803763/132241919-d0b20659-ebb1-4882-b125-1b93a906c8af.PNG){: .align-center .open-new}
