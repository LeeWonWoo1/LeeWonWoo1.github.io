---
title: "[Redux] Ducks Pattern"
excerpt: Redux Reducer Bundles
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
date: "2021-09-07T03:00:00"
last_modified_at: 2021-09-07T03:00:00
---

## Ducks Pattern

- src/redux
  - create.js
- src/redux/modules
  - module1.js
  - module2.js
  - ...
  - reducer.js (or index.js)

```js:src/redux/modules/filter.js
// 액션 타입 정의
const SHOW_ALL = "redux-start/filter/SHOW_ALL";
const SHOW_COMPLETE = "redux-start/filter/SHOW_COMPLETE";

// 액션 생성 함수
export function showAll() {
  return { type: SHOW_ALL };
}

export function showComplete() {
  return { type: SHOW_COMPLETE };
}

// 초기값
const initialState = "ALL";

// 리듀서
export default function reducer(previousState = initialState, action) {
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

```js:src/redux/modules/todos.js
// 액션 타입 정의
export const ADD_TODO = "redux-start/todos/ADD_TODO";
export const COMPLETE_TODO = "redux-start/todos/COMPLETE_TODO";

// 액션 생성 함수
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

// 초기값
const initialState = [];

// 리듀서
export default function reducer(previousState = initialState, action) {
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

```js:src/redux/modules/todos.js
import axios from "axios";

// 액션 타입 정의
// Github API 호출을 시작
export const GET_USERS_START = "redux-start/users/GET_USERS_START";

// Github API 호출에 대한 응답이 성공적으로 돌아온 경우
export const GET_USERS_SUCCESS = "redux-start/users/GET_USERS_SUCCESS";

// Github API 호출에 대한 응답이 실패한 경우
export const GET_USERS_FAIL = "redux-start/users/GET_USERS_FAIL";

// redux-promise-middleware
const GET_USERS = "redux-start/users/GET_USERS";

export const GET_USERS_PENDING = "redux-start/users/GET_USERS_PENDING";
export const GET_USERS_FULFILLED = "redux-start/users/GET_USERS_FULFILLED";
export const GET_USERS_REJECTED = "redux-start/users/GET_USERS_REJECTED";

// 액션 생성 함수
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

// 초기값
const initialState = {
  loading: false,
  data: [],
  error: null,
};

// 리듀서
export default function reducer(state = initialState, action) {
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
      error: action.PAYLOAD,
    };
  }

  return state;
}

// redux-thunk
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

// redux-promise-middleware
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

```js:src/redux/modules/reducers.js
import { combineReducers } from "redux";
import todos from "./todos";
import filter from "./filter";
import users from "./users";

const reducer = combineReducers({
  todos,
  filter,
  users,
});

export default reducer;
```

<br>

```jsx:src/containers/UserListContainer.jsx
import { useCallback } from "react";
import { useDispatch, useSelector } from "react-redux";
import UserList from "../components/UserList";
import { getUsersPromise, getUsersThunk } from "../redux/modules/users";

export default function UserListContainer() {
  const users = useSelector((state) => state.users.data);
  const dispatch = useDispatch();

  const getUsers = useCallback(() => {
    dispatch(getUsersThunk(getUsersPromise()));
  }, [dispatch]);

  return <UserList users={users} getUsers={getUsers} />;
```

<br>

```jsx:src/containers/TodoFormContainer.jsx
import { useCallback } from "react";
import { useDispatch } from "react-redux";
import TodoForm from "../components/TodoForm";
import { addTodo } from "../redux/modules/todos";

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

- src/redux/reducers 폴더 삭제
- src/redux/actions.js 파일 삭제

<br>

![redux-duckspattern](https://user-images.githubusercontent.com/62803763/132254872-17fb5880-723e-474f-a013-dcbf4979152c.PNG){: .align-center .open-new}
