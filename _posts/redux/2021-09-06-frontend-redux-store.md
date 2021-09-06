---
title: "[Redux] createStore"
excerpt: Redux Basic - 2
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
date: "2021-09-06T20:00:00"
last_modified_at: 2021-09-06T20:00:00
---

## createStore

- 스토어를 만드는 함수
- store.getState() : 현재 store의 state를 가져오는 함수
- store.dispatch(액션) : 액션을 인자로 넣어 store의 상태를 변경시키는 함수
- store.dispatch(액션생성자()) : store의 상태를 변경시키는 함수
- store.unsubscribe = store.subscribe(() => {}) : store에 변경이 생겼을 때, () => {} 함수를 실행
  - 리턴이 unsubscribe
  - unsubscribe() 하면 구독된 함수 제거
- store.replaceReducer(다른 리듀서) : 원래 가지고 있던 리듀서를 다른 리듀서로 바꿈

```js
const store = createStore(리듀서);

createStore<S> (
  reducer: Reducer<S>,
  preloadedState: S,
  enhancer?: StoreEnhancer<S>
): Store<S>;
```

<br>

```js
// src/redux/store.js

import { createStore } from "redux";
import { todoApp } from "./reducers";

const store = createStore(todoApp);

export default store;
```

<br>

```js
// index.js

import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";
import store from "./redux/store";
import { addTodo } from "./redux/actions";

const unsubscribe = store.subscribe(() => {
  console.log(store.getState());
});

store.dispatch(addTodo("coding"));
store.dispatch(addTodo("read book"));
store.dispatch(addTodo("eat"));
unsubscribe();
store.dispatch(addTodo("coding"));
store.dispatch(addTodo("read book"));
store.dispatch(addTodo("eat"));

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById("root")
);

reportWebVitals();
```

![redux-store1](https://user-images.githubusercontent.com/62803763/132213673-a5e6fa08-9dfb-41ea-976d-0bd0826704a7.PNG){: .align-center .open-new}

<br>

### - 스토어 만들기

```js
// src/redux/store.js

import { todoApp } from "./reducers";
import { createStore } from "redux";
import { addTodo } from "./actions";

const store = createStore(todoApp);
console.log(store);

console.log(store.getState());

setTimeout(() => {
  store.dispatch(addTodo("hello"));
}, 1000);

export default store;
```

<br>

```js
// index.js

import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import * as serviceWorker from "./serviceWorker";

import store from "./redux/store";

store.subscribe(() => {
  const state = store.getState();
  console.log("store changed", state);
});

ReactDOM.render(<App />, document.getElementById("root"));

serviceWorker.unregister();
```

![redux-store2](https://user-images.githubusercontent.com/62803763/132217143-80248be0-55c6-43c3-8827-b147a557a51e.PNG){: .align-center .open-new}

<br>

### - 로직 추가하기

1. action 정의
2. action 생성자 만들기
3. reducer 수정

```js
// src/redux/actions.js

// action 정의

// 액션의 type 정의
// 액션의 타입 -> 액션 생성자 이름
// ADD_TODO -> addTodo
export const ADD_TODO = "ADD_TODO";
export const COMPLETE_TODO = 'COMPLETE_TODO';

// 액션 생산자
// 액션의 타입은 미리 정의한 타입으로부터 가져와서 사용
// 사용자가 인자로 주지 않음
export function addTodo(text) {
  return { type: ADD_TODO, text};  // { type: ADD_TODO, text: text}
```

<br>

```js
// src/redux/actions.js

// action 생성자 만들기

export const ADD_TODO = "ADD_TODO";
export const COMPLETE_TODO = 'COMPLETE_TODO';

export function addTodo(text) {
  return { type: ADD_TODO, text};

export function completeTodo(index) {
  return { type: COMPLETE_TODO, index };  // { type: COMPLETE_TODO, index: index }
}
```

<br>

```js
// src/redux/reducer.js

// reducer 수정

import { ADD_TODO, COMPLETE_TODO } from "./actions";

export function todoApp(previousState, action) {
  if (previousState === undefined) {
    return [];
  }

  if (action.type === ADD_TODO) {
    return [...previousState, { text: action.text, completed: false }];
  }

  if (action.type === COMPLETE_TODO) {
    const newState = [];
    for (let i = 0; i < previousState.length; i++) {
      newState.push(
        i === action.index
          ? { ...previousState[i], completed: true }
          : { ...previousState[i] }
      );
    }
    return newState;
  }
  return previousState;
}
```

![redux-store3](https://user-images.githubusercontent.com/62803763/132217315-c8c7a17c-3ea3-40ff-a30d-fcd377c5d059.PNG){: .align-center .open-new}

<br>

```js
// src/redux/store.js

// dispatch

import { todoApp } from "./reducers";
import { createStore } from "redux";
import { addTodo, completeTodo } from "./actions";

const store = createStore(todoApp);
console.log(store);

console.log(store.getState());

setTimeout(() => {
  store.dispatch(addTodo("hello"));
  setTimeout(() => {
    store.dispatch(completeTodo(0));
  }, 1000);
}, 1000);

export default store;
```

![redux-store4](https://user-images.githubusercontent.com/62803763/132217540-167b70af-523e-49f8-a577-ed3165ea5a85.PNG){: .align-center .open-new}

<br>

- 애플리케이션이 커지면, state가 복잡해 짐
- 리듀서를 크게 만들고, state를 변경하는 모든 로직을 담을 수 있음
- 리듀서를 분할해서 만들고, 합치는 방법을 사용할 수 있음
  - todos만 변경하는 액션들을 처리하는 A 리듀서 함수를 만들고,
  - filter만 변경하는 액션들을 처리하는 B 리듀서 함수를 만들고,
  - A와 B를 합침

```js
[
  {
    text: "Hello",
    completed: false
  }
]

// ------------------------------

{
  todos: [
    {
      text: "Hello",
      completed: false
    }
  ],
  filter: "SHOW_ALL"
}
```

<br>

### - 한번에 다하는 리듀서

```js
// src/redux/reducer.js

import { ADD_TODO, COMPLETE_TODO } from "./actions";

export function todoApp(previousState, action) {
  if (previousState === undefined) {
    return { todos: [], filter: "SHOW_ALL" };
  }

  if (action.type === ADD_TODO) {
    return {
      todos: [...previousState.todos, { text: action.text, completed: false }],
      filter: previousState.filter,
    };
  }

  if (action.type === COMPLETE_TODO) {
    const newState = [];
    for (let i = 0; i < previousState.todos.length; i++) {
      newState.push(
        i === action.index
          ? { ...previousState.todos[i], completed: true }
          : { ...previousState.todos[i] }
      );
    }
    return { todos, filter: previousState.filter };
  }
  return previousState;
}
```

![redux-store5](https://user-images.githubusercontent.com/62803763/132223849-c6b80397-e56e-4caa-bd03-be1212ba49da.PNG){: .align-center .open-new}

<br>

### - 리듀서 분리

```js
// src/redux/reducer.js

export function todos(previousState, action) {
  if (previousState === undefined) {
    return [];
  }

  if (action.type === ADD_TODO) {
    return [...previousState, { text: action.text, completed: false }];
  }

  if (action.type === COMPLETE_TODO) {
    const newState = [];
    for (let i = 0; i < previousState.length; i++) {
      newState.push(
        i === action.index
          ? { ...previousState[i], completed: true }
          : { ...previousState[i] }
      );
    }
    return newState;
  }
  return previousState;
}

export function filter(previousState, action) {
  if (previousState === undefined) {
    return "SHOW_ALL";
  }
  return previousState;
}
```

<br>

### - 리듀서 합치기

```js
export function todoApp(previousState = {}, action) {
  return {
    todos: todos(previousState.todos, action),
    filter: filter(previousState.filter, acition),
  };
}
```

![redux-store6](https://user-images.githubusercontent.com/62803763/132224337-51d34a61-d060-48a8-b03c-a81417140f95.PNG){: .align-center .open-new}
