---
title: "[Redux] Redux-saga"
excerpt: Redux-saga Middleware
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
date: "2021-09-07T21:00:00"
last_modified_at: 2021-09-07T21:00:00
---

## Redux-saga

- 미들웨어
- 제너레이터 객체를 만들어 내는 제너레이터 생성 함수를 이용
- 리덕스 사가 미들웨어를 설정하고, 사가 함수를 등록한 후, 사가 미들웨어 실행
- 등록된 사가 함수를 실행할 액션을 디스패치
- 제공되는 effect를 사용해서 비동기 로직이나 사이드 effect가 생기는 로직들을 컨트롤 할 수 있음

```bash
# terminal

$ npm i redux-saga
```

<br>

```js
// src/redux/store.js

import { applyMiddleware, createStore } from "redux";
import todoApp from "./modules/reducer";
import { composeWithDevTools } from "redux-devtools-extension";
import thunk from "redux-thunk";
import promise from "redux-promise-middleware";
import history from "../history";
import { routerMiddleware } from "connected-react-router";
import createSagaMiddleware from "redux-saga";
import rootSaga from "./modules/rootSaga";

const sagaMiddleware = createSagaMiddleware();

const store = createStore(
  todoApp,
  composeWithDevTools(
    applyMiddleware(
      thunk.withExtraArgument({ history }),
      promise,
      routerMiddleware(history),
      sagaMiddleware
    )
  )
);

sagaMiddleware.run(rootSaga);

export default store;
```

<br>

```js
// src/redux/modules/users.js

import axios from "axios";
import { push } from "connected-react-router";
import { put, delay, call, takeEvery } from "redux-saga/effects";

// 액션 타입 정의
export const GET_USERS_START = "redux-start/users/GET_USERS_START";
export const GET_USERS_SUCCESS = "redux-start/users/GET_USERS_SUCCESS";
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

function sleep(ms) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, ms);
  });
}

// redux-thunk
export function getUsersThunk() {
  return async (dispatch, getState, { history }) => {
    try {
      console.log(history);
      dispatch(getUsersStart());
      // sleep
      await sleep(2000);
      const res = await axios.get("https://api.github.com/users");
      dispatch(getUsersSuccess(res.data));
      history.push("/");
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

// redux-saga
const GET_USERS_SAGA_START = "GET_USERS_SAGA_START";

function* getUsersSaga(action) {
  try {
    yield put(getUsersStart());
    // sleep
    yield delay(2000);
    const res = yield call(axios.get, "https://api.github.com/users");
    yield put(getUsersSuccess(res.data));
    yield put(push("/"));
  } catch (error) {
    yield put(getUsersFail(error));
  }
}

export function getUsersSagaStart() {
  return {
    type: GET_USERS_SAGA_START,
  };
}

export function* usersSaga() {
  yield takeEvery(GET_USERS_SAGA_START, getUsersSaga);
}
```

<br>

```js
// src/redux/modules/rootSaga.js

import { all } from "@redux-saga/core/effects";
import { usersSaga } from "./users";

export default function* rootSaga() {
  yield all([usersSaga()]);
}
```

<br>

```jsx
// src/containers/UserListContainer.jsx

import { useCallback } from "react";
import { useDispatch, useSelector } from "react-redux";
import UserList from "../components/UserList";
import { getUsersSagaStart } from "../redux/modules/users";

export default function UserListContainer() {
  const users = useSelector((state) => state.users.data);
  const dispatch = useDispatch();

  const getUsers = useCallback(() => {
    dispatch(getUsersSagaStart());
  }, [dispatch]);

  return <UserList users={users} getUsers={getUsers} />;
}
```

![redux-router3](https://user-images.githubusercontent.com/62803763/132346773-74de849f-fc6b-4423-844d-1392add7fc0d.PNG){: .align-center .open-new}

![redux-router4](https://user-images.githubusercontent.com/62803763/132346777-d5324c3e-1735-4524-a837-e974d9ad1ff8.PNG){: .align-center .open-new}
