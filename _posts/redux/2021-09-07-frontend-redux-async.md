---
title: "[Redux] Async Action with Redux"
excerpt: 비동기 처리를 위한 액션
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
date: "2021-09-07T01:00:00"
last_modified_at: 2021-09-07T01:00:00
---

## Async Action with Redux

- 비동기 작업을 어디서 하느가가 제일 중요
- 액션을 분리
  - Start
  - Success
  - Fail
  - ...
- dispatch를 할 때 해줌
  - 리듀서는 동기적인 것 -> Pure
  - dispatch도 동기적인 것

<br>

### - 미들웨어를 사용하지 않고 비동기 처리

```bash
# terminal

$ npm i axios
```

<br>

```js
// src/redux/reducers/reducer.js

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

// users

// Github API 호출을 시작
export const GET_USERS_START = "GET_USERS_START";

// Github API 호출에 대한 응답이 성공적으로 돌아온 경우
export const GET_USERS_SUCCESS = "GET_USERS_SUCCESS";

// Github API 호출에 대한 응답이 실패한 경우
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
```

<br>

```js
// src/redux/reducers/users.js

import { GET_USERS_FAIL, GET_USERS_START, GET_USERS_SUCCESS } from "../actions";

const initialState = {
  loading: false,
  data: [],
  error: null,
};

export default function users(state = initialState, action) {
  if (action.type === GET_USERS_START) {
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

  if (action.type === GET_USERS_FAIL) {
    return {
      ...state,
      loading: false,
      error: action.error,
    };
  }

  return state;
}
```

<br>

```js
// src/App.js

import "./App.css";
import TodoListContainer from "./containers/TodoListContainer";
import TodoFormContainer from "./containers/TodoFormContainer";
import UserListContainer from "./containers/UserListContainer";

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <UserListContainer />
        <TodoListContainer />
        <TodoFormContainer />
      </header>
    </div>
  );
}

export default App;
```

<br>

```jsx
// src/components/UserList.jsx

import { useEffect } from "react";

export default function UserList({ users, getUsers }) {
  useEffect(() => {
    getUsers();
  }, [getUsers]);

  if (users.length === 0) {
    return <p>현재 유저 정보 없음</p>;
  }

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.login}</li>
      ))}
    </ul>
  );
}
```

<br>

```jsx
// src/containers/UserListContainer.jsx

import { useCallback } from "react";
import { useDispatch, useSelector } from "react-redux";
import UserList from "../components/UserList";
import { getUsersFail, getUsersStart, getUsersSuccess } from "../redux/actions";
import axios from "axios";

export default function UserListContainer() {
  const users = useSelector((state) => state.users.data);
  const dispatch = useDispatch();

  const getUsers = useCallback(async () => {
    try {
      dispatch(getUsersStart());
      const res = await axios.get("https://api.github.com/users");
      dispatch(getUsersSuccess(res.data));
    } catch (error) {
      dispatch(getUsersFail(error));
    }
  }, [dispatch]);

  return <UserList users={users} getUsers={getUsers} />;
}
```

<br>

![redux-async](https://user-images.githubusercontent.com/62803763/132249142-b20f60ad-21db-4f2b-b295-1c04048cce32.PNG){: .align-center .open-new}
