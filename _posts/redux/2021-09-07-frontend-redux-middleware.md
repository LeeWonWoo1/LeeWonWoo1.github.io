---
title: "[Redux] Middleware"
excerpt: Redux 미들웨어
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
date: "2021-09-07T02:00:00"
last_modified_at: 2021-09-07T02:00:00
---

## Redux Middleware

- 미들웨어가 디스패치의 앞뒤에 코드를 추가할 수 있게 해줌
- 미들웨어가 여러개면 미들웨어가 순차적으로 실행됨
- 두 단계가 있음
  - 스토어를 만들 때, 미들웨어를 설정하는 부분
    - {createStore, applyMiddleware } from redux
  - 디스패치가 호출될 때 실제로 미들웨어를 통과하는 부분
- dispatch 메소드를 통해 store로 가고 있는 액션을 가로채는 코드

```js:src/redux/store.js
import { applyMiddleware, createStore } from "redux";
import todoApp from "./reducers/reducer";

function middleware1(store) {
  console.log("middleware1", 0);
  return (next) => {
    console.log("middleware1", 1, next);
    return (action) => {
      console.log("middleware1", 2);
      const returnValue = next(action);
      console.log("middleware1", 3);
      return returnValue;
    };
  };
}

function middleware2(store) {
  console.log("middleware2", 0);
  return (next) => {
    console.log("middleware2", 1, next);
    return (action) => {
      console.log("middleware2", 2);
      const returnValue = next(action);
      console.log("middleware2", 3);
      return returnValue;
    };
  };
}

const store = createStore(todoApp, applyMiddleware(middleware1, middleware2));

export default store;
```

![redux-middleware](https://user-images.githubusercontent.com/62803763/132250490-42c2ee7e-5e7d-4f2e-b38c-b97e5756d1a9.PNG){: .align-center .open-new}

<br>

### - Redux-devtools

```bash:terminal
$ npm i redux-devtools-extension -D
```

<br>

```js:src/redux/store.js
import { applyMiddleware, createStore } from "redux";
import todoApp from "./reducers/reducer";
import { composeWithDevTools } from "redux-devtools-extension";

const store = createStore(todoApp, composeWithDevTools(applyMiddleware()));

export default store;
```

<br>

[https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=ko](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=ko){:target="\_blank"}
{: .notice--info}

![redux-devtools1](https://user-images.githubusercontent.com/62803763/132250800-8ed58274-5939-42b7-b775-00c6ceb46290.PNG){: .align-center .open-new}

<br>

![redux-devtools2](https://user-images.githubusercontent.com/62803763/132251110-a8881f17-a550-4303-9975-1800f5a83fe0.PNG){: .align-center .open-new}

<br>

### - Redux-thunk

- Redux 미들웨어
- Redux에서 비동기 처리를 위한 라이브러리
- 액션 생성자를 활용하여 비동기 처리
- 액션 생성자가 액션을 리턴하지 않고, 함수를 리턴

```bash:terminal
$ npm i redux-thunk
```

<br>

```js:src/redux/store.js
import { applyMiddleware, createStore } from "redux";
import todoApp from "./reducers/reducer";
import { composeWithDevTools } from "redux-devtools-extension";
import thunk from "redux-thunk";

const store = createStore(todoApp, composeWithDevTools(applyMiddleware(thunk)));

export default store;
```

<br>

```js:src/redux/actions.js
import axios from "axios";

export const ADD_TODO = "ADD_TODO";
export const COMPLETE_TODO = "COMPLETE_TODO";

export function addTodo(text) {
  return {
    type: ADD_TODO,
    text,
  };
}

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

// users
export const GET_USERS_START = "GET_USERS_START";
export const GET_USERS_SUCCESS = "GET_USERS_SUCCESS";
export const GET_USERS_FAIL = "GET_USERS_FAIL";

export function getUsersStart() {
  return {
    type: GET_USERS_START,
  };
}

export function getUsersSuccess(data) {
  return {
    type: GET_USERS_SUCCESS,
    data,
  };
}

export function getUsersFail(error) {
  return {
    type: GET_USERS_FAIL,
    error,
  };
}

// Thunk
export function getUsersThunk() {
  return async (dispatch) => {
    try {
      dispatch(getUsersStart());
      const res = await axios.get("https://api.github.com/users");
      dispatch(getUsersSuccess(res.data));
    } catch (error) {
      dispatch(getUsersFail(error));
    }
  };
}
```

<br>

```jsx:src/containers/UserListContainer.jsx
import { useCallback } from "react";
import { useDispatch, useSelector } from "react-redux";
import UserList from "../components/UserList";
import { getUsersThunk } from "../redux/actions";

export default function UserListContainer() {
  const users = useSelector((state) => state.users.data);
  const dispatch = useDispatch();

  const getUsers = useCallback(() => {
    dispatch(getUsersThunk());
  }, [dispatch]);

  return <UserList users={users} getUsers={getUsers} />;
}
```

![redux-thunk](https://user-images.githubusercontent.com/62803763/132251837-d6b9e3c8-ddeb-46e4-82ed-1661ba63bb3d.PNG){: .align-center .open-new}

<br>

### - Redux-promise-middleware

```bash:terminal
$ npm i redux-promise-middleware
```

<br>

```js:src/redux/store.js

import { applyMiddleware, createStore } from "redux";
import todoApp from "./reducers/reducer";
import { composeWithDevTools } from "redux-devtools-extension";
import thunk from "redux-thunk";
import promise from "redux-promise-middleware";

const store = createStore(
  todoApp,
  composeWithDevTools(applyMiddleware(thunk, promise))
);

export default store;
```

<br>

```js:src/redux/actions.js
import axios from "axios";

export const ADD_TODO = "ADD_TODO";
export const COMPLETE_TODO = "COMPLETE_TODO";

export function addTodo(text) {
  return {
    type: ADD_TODO,
    text,
  };
}

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

// users
export const GET_USERS_START = "GET_USERS_START";
export const GET_USERS_SUCCESS = "GET_USERS_SUCCESS";
export const GET_USERS_FAIL = "GET_USERS_FAIL";

export function getUsersStart() {
  return {
    type: GET_USERS_START,
  };
}

export function getUsersSuccess(data) {
  return {
    type: GET_USERS_SUCCESS,
    data,
  };
}

export function getUsersFail(error) {
  return {
    type: GET_USERS_FAIL,
    error,
  };
}

// Thunk
export function getUsersThunk() {
  return async (dispatch) => {
    try {
      dispatch(getUsersStart());
      const res = await axios.get("https://api.github.com/users");
      dispatch(getUsersSuccess(res.data));
    } catch (error) {
      dispatch(getUsersFail(error));
    }
  };
}

const GET_USERS = "GET_USERS";

export const GET_USERS_PENDING = "GET_USERS_PENDING";
export const GET_USERS_FULFILLED = "GET_USERS_FULFILLED";
export const GET_USERS_REJECTED = "GET_USERS_REJECTED";

// Promise
export function getUsersPromise() {
  return {
    type: GET_USERS,
    payload: async () => {
      const res = await axios.get("https://api.github.com/users");
      return res.data;
    },
  };
}
```

<br>

```jsx:src/containers/UserListContainer.jsx

import { useCallback } from "react";
import { useDispatch, useSelector } from "react-redux";
import UserList from "../components/UserList";
import { getUsersPromise, getUsersThunk } from "../redux/actions";

export default function UserListContainer() {
  const users = useSelector((state) => state.users.data);
  const dispatch = useDispatch();

  const getUsers = useCallback(() => {
    dispatch(getUsersThunk(getUsersPromise()));
  }, [dispatch]);

  return <UserList users={users} getUsers={getUsers} />;
}
```

<br>

```js:src/redux/reducers/users.js
import {
  GET_USERS_FAIL,
  GET_USERS_FULFILLED,
  GET_USERS_PENDING,
  GET_USERS_REJECTED,
  GET_USERS_START,
  GET_USERS_SUCCESS,
} from "../actions";

const initialState = {
  loading: false,
  data: [],
  error: null,
};

export default function users(state = initialState, action) {
  if (action.type === GET_USERS_START || action.type === GET_USERS_PENDING) {
    return {
      ...state,
      loading: true,
      error: null,
    };
  }

  if (action.type === GET_USERS_SUCCESS) {
    return {
      ...state,
      loading: false,
      data: action.data,
    };
  }

  if (action.type === GET_USERS_FULFILLED) {
    return {
      ...state,
      loading: false,
      data: action.payload,
    };
  }

  if (action.type === GET_USERS_FAIL) {
    return {
      ...state,
      loading: false,
      error: action.error,
    };
  }

  if (action.type === GET_USERS_REJECTED) {
    return {
      ...state,
      loading: false,
      error: action.payload,
    };
  }

  return state;
}
```
