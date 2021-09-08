---
title: "[React] 책장 만들기"
excerpt: Toy Project
categories:
  - React
tags:
  - - React
    - Redux
    - Typescript
    - Web
    - Node.js
toc: true
toc_sticky: true
popular: true
date: "2021-09-08T00:00:00"
last_modified_at: 2021-09-08T00:00:00
---

## 1. 라우팅 설정하기

```bash
# terminal

$ npx create-react-app my-books --template typescript
$ cd my-books
$ code .
```

<br>

```bash
# terminal

$ npm i react-router-dom
$ npm i --save-dev @types/react-router-dom
$ npm i react-error-boundary
```

<br>

```tsx
// src/App.tsx

import React from "react";
import { BrowserRouter, Route, Switch } from "react-router-dom";
import Home from "./pages/Home";
import Add from "./pages/Add";
import Detail from "./pages/Detail";
import Edit from "./pages/Edit";
import Signin from "./pages/Signin";
import NotFound from "./pages/NotFound";
import Error from "./pages/Error";
import { ErrorBoundary } from "react-error-boundary";

function App() {
  return (
    <ErrorBoundary FallbackComponent={Error}>
      <BrowserRouter>
        <Switch>
          <Route exact path="/edit/:id" component={Edit} />
          <Route exact path="/book/:id" component={Detail} />
          <Route exact path="/add" component={Add} />
          <Route exact path="/signin" component={Signin} />
          <Route exact path="/" component={Home} />
          <Route component={NotFound} />
        </Switch>
      </BrowserRouter>
    </ErrorBoundary>
  );
}

export default App;
```

<br>

```tsx
// src/pages/Home.tsx

import React from "react";

export default function Home() {
  return (
    <div>
      <h1>Home</h1>
    </div>
  );
}

// -------------------------------
// // src/pages/Add.tsx

import React from "react";

export default function Add() {
  return (
    <div>
      <h1>Add</h1>
    </div>
  );
}

// -------------------------------
// // src/pages/Detail.tsx

import React from "react";

export default function Detail() {
  return (
    <div>
      <h1>Detail</h1>
    </div>
  );
}

// -------------------------------
// // src/pages/Edit.tsx

import React from "react";

export default function Edit() {
  return (
    <div>
      <h1>Edit</h1>
    </div>
  );
}

// -------------------------------
// // src/pages/Signin.tsx

import React from "react";

export default function Signin() {
  return (
    <div>
      <h1>Signin</h1>
    </div>
  );
}

// -------------------------------
// // src/pages/NotFound.tsx

import React from "react";

export default function NotFound() {
  return (
    <div>
      <h1>NotFound</h1>
    </div>
  );
}

// -------------------------------
// // src/pages/Error.tsx

import React from "react";

export default function Error() {
  return (
    <div>
      <h1>Error</h1>
    </div>
  );
}
```

![react-book1](https://user-images.githubusercontent.com/62803763/132529851-6db5ab01-d221-42c2-8dfd-b19d1bdb9ebd.PNG){: .align-center .open-new}

<br>

## 2. 로그인, 로그아웃 처리

```bash
# terminal

$ npm i redux react-redux redux-saga
$ npm i redux-devtools-extension redux-actions
$ npm i @types/react-redux @types/redux-actions -D
```

<br>

### - 스토어 설정

```ts
// src/redux/create.ts

import { applyMiddleware, createStore } from "redux";
import { composeWithDevTools } from "redux-devtools-extension";
import reducer from "./modules/reducer";
import createSagaMiddleware from "redux-saga";
import rootSaga from "./modules/rootSaga";

const create = () => {
  const sagaMiddleware = createSagaMiddleware();

  const store = createStore(
    reducer,
    composeWithDevTools(applyMiddleware(sagaMiddleware))
  );

  sagaMiddleware.run(rootSaga);

  return store;
};

export default create;
```

<br>

```ts
// src/redux/modules/auth.ts

import { createActions, handleActions } from "redux-actions";

interface AuthState {
  token: string | null;
  loading: boolean;
  error: Error | null;
}

const initialState: AuthState = {
  token: null,
  loading: false,
  error: null,
};

const prefix = "my-books/auth";

export const { pending, success, fail } = createActions(
  "PENDING",
  "SUCCESS",
  "FAIL",
  { prefix }
);

const reducer = handleActions<AuthState, string>(
  {
    PENDING: (state) => ({
      ...state,
      loading: true,
      error: null,
    }),
    SUCCESS: (state, action) => ({
      token: action.payload,
      loading: false,
      error: null,
    }),
    FAIL: (state, action: any) => ({
      ...state,
      loading: false,
      error: action.payload,
    }),
  },
  initialState,
  { prefix }
);

export default reducer;

// saga
export function* authSaga() {}
```

<br>

```ts
// src/redux/modules/reducers.ts

import { combineReducers } from "redux";
import auth from "./auth";

const reducer = combineReducers({
  auth,
});

export default reducer;
```

<br>

```ts
// src/redux/modules/rootSaga.ts

import { all } from "redux-saga/effects";
import { authSaga } from "./auth";

export default function* rootSaga() {
  yield all([authSaga()]);
}
```

<br>

### - 로그인 페이지 설계

```bash
# terminal

$ npm i antd
$ npm i @ant-design/icons
```

<br>

```tsx
// src/index.tsx

import React from "react";
import ReactDOM from "react-dom";
import "antd/dist/antd.css";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";
import create from "./redux/create";
import { Provider } from "react-redux";

const store = create();

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById("root")
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

<br>

```tsx
// src/pages/Signin.tsx

import React from "react";
import SigninContainer from "../containers/SigninContainer";

export default function Signin() {
  return <SigninContainer />;
}
```

<br>

```tsx
// src/components/Signin.tsx

import { Button, Col, Input, Row } from "antd";
import { useRef } from "react";
import { LoginReqType } from "../types";
import styles from "./Signin.module.css";

interface SigninProps {
  login: (reqData: LoginReqType) => void;
}

const Signin: React.FC<SigninProps> = ({ login }) => {
  const emailRef = useRef<Input>(null);
  const passwordRef = useRef<Input>(null);

  return (
    <Row align="middle" className={styles.signin_row}>
      <Col span={24}>
        <Row className={styles.signin_contents}>
          <Col span={12}>
            <img
              src="/bg_signin.png"
              alt="Signin"
              className={styles.signin_bg}
            />
          </Col>
          <Col span={12}>
            <div className={styles.signin_title}>My Books</div>
            <div className={styles.signin_subtitle}>
              Please Note Your Opinion
            </div>
            <div className={styles.signin_underline} />
            <div className={styles.email_title}>
              Email
              <span className={styles.required}> *</span>
            </div>
            <div className={styles.input_area}>
              <Input
                placeholder="Email"
                autoComplete="email"
                name="email"
                className={styles.input}
                ref={emailRef}
              />
            </div>
            <div className={styles.password_title}>
              Password
              <span className={styles.required}> *</span>
            </div>
            <div className={styles.input_area}>
              <Input
                placeholder="Password"
                type="password"
                autoComplete="current-password"
                className={styles.input}
                ref={passwordRef}
              />
            </div>
            <div className={styles.button_area}>
              <Button size="large" className={styles.button} onClick={click}>
                Sign In
              </Button>
            </div>
          </Col>
        </Row>
      </Col>
    </Row>
  );

  function click() {
    const email = emailRef.current!.state.value;
    const password = passwordRef.current!.state.value;

    login({ email, password });
  }
};

export default Signin;
```

<br>

```ts
// src/types.ts

export type LoginReqType = {
  email: string;
  password: string;
};
```

<br>

```css
/* src/components/Signin.module.css */

.signin_row {
  height: 100vh;
}

.signin_title {
  text-align: center;
  font-size: 30px;
  font-weight: bold;
  color: #642828;
  text-transform: uppercase;
  margin-top: 80px;
}

.signin_subtitle {
  text-align: center;
  font-size: 20px;
  font-weight: bold;
  text-transform: uppercase;
}

.signin_underline {
  width: 200px;
  height: 6px;
  margin-right: auto;
  margin-left: auto;
  margin-top: 20px;
  background: linear-gradient(to right, #803b32, #ddb49b);
}

.signin_contents {
  margin-top: 50px;
  background-color: #f3f7f8;
  margin-left: auto;
  margin-right: auto;
  width: 800px;
}

.signin_bg {
  width: 100%;
}

.email_title {
  font-family: Roboto;
  font-size: 12px;
  font-weight: bold;
  margin-top: 40px;
  text-align: left;
  padding-left: 40px;
}

.password_title {
  font-family: Roboto;
  font-size: 12px;
  font-weight: bold;
  margin-top: 10px;
  text-align: left;
  padding-left: 40px;
}

.required {
  color: #971931;
}

.input_area {
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 40px;
  padding-right: 40px;
}

.input {
  width: 100%;
  border-radius: 1px;
  border-width: 1px;
  font-family: Roboto;
}

.button_area {
  text-align: center;
  padding-left: 40px;
  padding-right: 40px;
  margin-top: 20px;
}

.button {
  border-color: #28546a;
  background-color: #28546a;
  text-transform: uppercase;
  border-radius: 1px;
  border-width: 2px;
  color: white;
  width: 100%;
}

.button:hover {
  background-color: #28546a;
  color: white;
}
```

<br>

```tsx
// src/containers/SigninContainer.tsx

import { useCallback } from "react";
import { useDispatch } from "react-redux";
import Signin from "../components/Signin";
import { login as loginSagaStart } from "../redux/modules/auth";

export default function SigninContainer() {
  const dispatch = useDispatch();
  const login = useCallback(
    (reqData) => {
      dispatch(loginSagaStart(reqData));
    },
    [dispatch]
  );

  return <Signin login={login} />;
}
```

<br>

```ts
// src/redux/modules/auth.ts

import { call, put, select, takeEvery } from "@redux-saga/core/effects";
import { Action, createActions, handleActions } from "redux-actions";
import UserService from "../../services/UserService";
import TokenService from "../../services/TokenService";
import { AuthState, LoginReqType } from "../../types";
import { push } from "connected-react-router";

const initialState: AuthState = {
  token: null,
  loading: false,
  error: null,
};

const prefix = "my-books/auth";

export const { pending, success, fail } = createActions(
  "PENDING",
  "SUCCESS",
  "FAIL",
  { prefix }
);

const reducer = handleActions<AuthState, string>(
  {
    PENDING: (state) => ({
      ...state,
      loading: true,
      error: null,
    }),
    SUCCESS: (state, action) => ({
      token: action.payload,
      loading: false,
      error: null,
    }),
    FAIL: (state, action: any) => ({
      ...state,
      loading: false,
      error: action.payload,
    }),
  },
  initialState,
  { prefix }
);

export default reducer;

// saga
export const { login, logout } = createActions("LOGIN", "LOGOUT", { prefix });

function* loginSaga(action: Action<LoginReqType>) {
  try {
    yield put(pending());
    const token: string = yield call(UserService.login, action.payload);
    TokenService.set(token);
    yield put(success(token));
    yield put(push("/"));
  } catch (error: any) {
    yield put(fail(new Error(error?.response?.data?.error || "UNKNOWN_ERROR")));
  }
}

function* logoutSaga() {
  try {
    yield put(pending());
    const token: string = yield select((state) => state.auth.token);
    yield call(UserService.logout, token);
    TokenService.set(token);
  } catch (error) {
  } finally {
    TokenService.remove();
    yield put(success(null));
  }
}

export function* authSaga() {
  yield takeEvery(`${prefix}/LOGIN`, loginSaga);
  yield takeEvery(`${prefix}/LOGOUT`, logoutSaga);
}
```

<br>

```bash
# terminal

$ npm i axios
```

<br>

```ts
// src/services/UserService.ts

import axios from "axios";
import { LoginReqType } from "../types";

const USER_API_URL = "https://api.marktube.tv/v1/me";

export default class UserService {
  public static async login(reqData: LoginReqType): Promise<string> {
    const response = await axios.post(USER_API_URL, reqData);
    return response.data.token;
  }

  public static async logout(token: string): Promise<void> {
    await axios.delete(USER_API_URL, {
      headers: { Authorization: `Bearer ${token}` },
    });
  }
}
```

<br>

```ts
// src/services/TokenService.ts

const LOCAL_STORAGE_TOKEN_KEY_NAME = "token";

export default class TokenService {
  public static get(): string | null {
    return localStorage.getItem(LOCAL_STORAGE_TOKEN_KEY_NAME);
  }

  public static set(token: string): void {
    localStorage.setItem(LOCAL_STORAGE_TOKEN_KEY_NAME, token);
  }

  public static remove(): void {
    localStorage.removeItem(LOCAL_STORAGE_TOKEN_KEY_NAME);
  }
}
```

<br>

```bash
# terminal

$ npm i connected-react-router
```

<br>

```ts
// src/redux/create.ts

import { applyMiddleware, createStore } from "redux";
import { composeWithDevTools } from "redux-devtools-extension";
import reducer from "./modules/reducer";
import createSagaMiddleware from "redux-saga";
import rootSaga from "./modules/rootSaga";
import { routerMiddleware } from "connected-react-router";
import history from "../history";
import TokenService from "../services/TokenService";

const create = () => {
  const token = TokenService.get();

  const sagaMiddleware = createSagaMiddleware();

  const store = createStore(
    reducer(history),
    {
      auth: {
        token,
        loading: false,
        error: null,
      },
    },
    composeWithDevTools(
      applyMiddleware(sagaMiddleware, routerMiddleware(history))
    )
  );

  sagaMiddleware.run(rootSaga);

  return store;
};

export default create;
```

<br>

```ts
// src/history.ts

import { createBrowserHistory } from "history";

const history = createBrowserHistory();

export default history;
```

<br>

```ts
// src/redux/modules/reducer.ts

import { connectRouter } from "connected-react-router";
import { combineReducers } from "redux";
import auth from "./auth";
import { History } from "history";

const reducer = (history: History<unknown>) =>
  combineReducers({
    auth,
    router: connectRouter(history),
  });

export default reducer;
```

<br>

```tsx
// src/App.tsx

import React from "react";
import { Route, Switch } from "react-router-dom";
import Home from "./pages/Home";
import Add from "./pages/Add";
import Detail from "./pages/Detail";
import Edit from "./pages/Edit";
import Signin from "./pages/Signin";
import NotFound from "./pages/NotFound";
import Error from "./pages/Error";
import { ErrorBoundary } from "react-error-boundary";
import { ConnectedRouter } from "connected-react-router";
import history from "./history";

function App() {
  return (
    <ErrorBoundary FallbackComponent={Error}>
      <ConnectedRouter history={history}>
        <Switch>
          <Route exact path="/edit/:id" component={Edit} />
          <Route exact path="/book/:id" component={Detail} />
          <Route exact path="/add" component={Add} />
          <Route exact path="/signin" component={Signin} />
          <Route exact path="/" component={Home} />
          <Route component={NotFound} />
        </Switch>
      </ConnectedRouter>
    </ErrorBoundary>
  );
}

export default App;
```

<br>

```tsx
// src/pages/Signin.tsx

import React from "react";
import { useSelector } from "react-redux";
import { Redirect } from "react-router";
import SigninContainer from "../containers/SigninContainer";
import { RootState } from "../types";

export default function Signin() {
  const token = useSelector<RootState, string | null>(
    (state) => state.auth.token
  );

  if (token !== null) {
    return <Redirect to="/" />;
  }

  return <SigninContainer />;
}
```

<br>

```ts
// src/types.ts

import { RouterState } from "connected-react-router";
import { AnyAction, Reducer } from "redux";

export type LoginReqType = {
  email: string;
  password: string;
};

export interface AuthState {
  token: string | null;
  loading: boolean;
  error: Error | null;
}

export interface RootState {
  auth: AuthState;
  router: Reducer<RouterState<unknown>, AnyAction>;
}
```

<br>

```tsx
// src/pages/Home.tsx

import React from "react";
import { useDispatch, useSelector } from "react-redux";
import { Redirect } from "react-router-dom";
import { logout } from "../redux/modules/auth";
import { RootState } from "../types";

export default function Home() {
  const dispatch = useDispatch();
  const token = useSelector<RootState, string | null>(
    (state) => state.auth.token
  );

  if (token === null) {
    return <Redirect to="/signin" />;
  }

  return (
    <div>
      <h1>Home</h1>
      <button onClick={click}>logout</button>
    </div>
  );

  function click() {
    dispatch(logout());
  }
}
```

<br>

![react-book2](https://user-images.githubusercontent.com/62803763/132553080-5967cd06-f0c6-42d5-9d1e-66d92e1fdedd.PNG){: .align-center .open-new}

![react-book3](https://user-images.githubusercontent.com/62803763/132553087-64853601-a8a9-4d45-b960-4ef55173377e.PNG){: .align-center .open-new}

![react-book4](https://user-images.githubusercontent.com/62803763/132553089-74c818eb-ef39-40f7-86db-25ba2840999c.PNG){: .align-center .open-new}
