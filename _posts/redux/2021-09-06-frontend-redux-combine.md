---
title: "[Redux] combineReducers"
excerpt: Redux Basic - 3
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
date: "2021-09-06T22:00:00"
last_modified_at: 2021-09-06T22:00:00
---

## combineReducers

- Redux에서 제공하는 combineReducers 사용

```js
import { combineReducers } from "redux";

const todoApp = combineReducers({
  todos,
  filter,
});
```

<br>

```js
// src/redux/actions.js

export const ADD_TODO = "ADD_TODO";
export const COMPLETE_TODO = "COMPLETE_TODO";

// { type: ADD_TODO, text: text}
export function addTodo(text) {
  return {
    type: ADD_TODO,
    text,
  };
}

// { type: COMPLETE_TODO, index: index }
export function completeTodo(index) {
  return {
    type: COMPLETE_TODO,
    index,
  };
}

export const SHOW_ALL = "SHOW_ALL";
export const SHOW_COMPLETE = "SHOW_COMPLETE";

export function showAll() {
  return { type: SHOW_ALL };
}

export function showComplete() {
  return { type: SHOW_COMPLETE };
}
```

<br>

```js
// src/redux/reducers/reducer.js

import { combineReducers } from "redux";
import todos from "./todos";
import filter from "./filter";

const reducer = combineReducers({
  todos,
  filter,
});

export default reducer;
```

<br>

```js
// src/redux/reducers/todos.js

import { ADD_TODO, COMPLETE_TODO } from "../actions";

const initialState = [];

export default function todos(previousState = initialState, action) {
  if (action.type === ADD_TODO) {
    return [...previousState, { text: action.text, done: false }];
  }

  if (action.type === COMPLETE_TODO) {
    return previousState.map((todo, index) => {
      if (index === action.index) {
        return { ...todo, done: true };
      }
      return todo;
    });
  }

  return previousState;
}
```

<br>

```js
// src/redux/reducers/filter.js

import { SHOW_COMPLETE, SHOW_ALL } from "../actions";

const initialState = "ALL";

export default function filter(previousState = initialState, action) {
  if (action.type === SHOW_COMPLETE) {
    return "COMPLETE";
  }

  if (action.type === SHOW_ALL) {
    return "ALL";
  }

  return previousState;
}
```

<br>

```js
// src/redux/store.js

import { createStore } from "redux";
import todoApp from "./reducers/reducer";

const store = createStore(todoApp);

export default store;
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
import { addTodo, completeTodo, showComplete } from "./redux/actions";

store.subscribe(() => {
  console.log(store.getState());
});

store.dispatch(addTodo("할일"));
store.dispatch(completeTodo(0));
store.dispatch(showComplete());

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById("root")
);

reportWebVitals();
```

![redux-combine](https://user-images.githubusercontent.com/62803763/132228135-30e0abfa-3885-4a17-b2f4-73ef2928f9fe.PNG){: .align-center .open-new}
