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

<br>

## 3. 책 목록 보여주기

```ts
// src/redux/modules/books.ts

import { createActions, handleActions } from "redux-actions";
import { BooksState, BookType } from "../../types";

const initialState: BooksState = {
  books: null,
  loading: false,
  error: null,
};

const prefix = "my-books/books";

export const { pending, success, fail } = createActions(
  "PENDING",
  "SUCCESS",
  "FAIL",
  { prefix }
);

const reducer = handleActions<BooksState, BookType[]>(
  {
    PENDING: (state) => ({ ...state, loading: true, error: null }),
    SUCCESS: (state, action) => ({
      books: action.payload,
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

export function* booksSaga() {}
```

<br>

```ts
// src/redux/modules/rootSaga.ts

import { all } from "redux-saga/effects";
import { authSaga } from "./auth";
import { booksSaga } from "./books";

export default function* rootSaga() {
  yield all([authSaga(), booksSaga()]);
}
```

<br>

```tsx
// src/components/List.tsx

export default function List() {
  return (
    <div>
      <h1>List</h1>
      <button onClick={click}>logout</button>
    </div>
  );

  function click() {}
}
```

<br>

```tsx
// src/containers/ListContainer.tsx

import List from "../components/List";

export default function ListContainer() {
  return <List />;
}
```

<br>

```tsx
// src/pages/Home.tsx

import React from "react";
import { useSelector } from "react-redux";
import { Redirect } from "react-router-dom";
import { RootState } from "../types";
import ListContainer from "../containers/ListContainer";

export default function Home() {
  const token = useSelector<RootState, string | null>(
    (state) => state.auth.token
  );

  if (token === null) {
    return <Redirect to="/signin" />;
  }

  return <ListContainer />;
}
```

<br>

```tsx
// src/components/Layout.tsx

import styles from "./Layout.module.css";

const Layout: React.FC = ({ children }) => (
  <div className={styles.layout}>{children}</div>
);

export default Layout;
```

<br>

```css
/* src/components/Layout.module.css */

.layout {
  margin-left: auto;
  margin-right: auto;
  width: 800px;
  margin-bottom: 50px;
}
```

<br>

```tsx
// src/components/List.tsx

import { Button, PageHeader, Table } from "antd";
import { BookType } from "../types";
import Layout from "./Layout";

interface ListProps {
  books: BookType[] | null;
  loading: boolean;
}

const List: React.FC<ListProps> = ({ books, loading }) => {
  const goAdd = () => {};
  const logout = () => {};

  return (
    <Layout>
      <PageHeader
        title={<div>Book List</div>}
        extra={[
          <Button key="2" type="primary" onClick={goAdd}>
            Add Book
          </Button>,
          <Button key="1" type="primary" onClick={logout}>
            Logout
          </Button>,
        ]}
      />
      <Table
        dataSource={[]}
        columns={[
          {
            title: "Book",
            dataIndex: "book",
            key: "book",
            render: () => <div>book</div>,
          },
        ]}
        loading={books === null || loading}
        showHeader={false}
        rowKey="bookId"
        pagination={false}
      />
    </Layout>
  );
};

export default List;
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

export interface BooksState {
  books: BookType[] | null;
  loading: boolean;
  error: Error | null;
}

export interface RootState {
  auth: AuthState;
  books: BooksState;
  router: Reducer<RouterState<unknown>, AnyAction>;
}

export interface BookType {
  bookId: number;
  title: string;
  author: string;
  createdAt: string;
  url: string;
}
```

<br>

```tsx
// src/containers/ListContainer.tsx

import { useSelector } from "react-redux";
import List from "../components/List";
import { BookType, RootState } from "../types";

export default function ListContainer() {
  const books = useSelector<RootState, BookType[]>(
    (state) => state.books.books
  );
  return <List books={books} />;
}
```

<br>

```ts
// src/redux/modules/reducer.ts

import { connectRouter } from "connected-react-router";
import { combineReducers } from "redux";
import auth from "./auth";
import books from "./books";
import { History } from "history";

const reducer = (history: History<unknown>) =>
  combineReducers({
    auth,
    books,
    router: connectRouter(history),
  });

export default reducer;
```

<br>

```tsx
// src/containers/ListContainer.tsx

import { useCallback } from "react";
import { useDispatch, useSelector } from "react-redux";
import List from "../components/List";
import { BookType, RootState } from "../types";
import { getBooks as getBooksSagaStart } from "../redux/modules/books";

export default function ListContainer() {
  const books = useSelector<RootState, BookType[] | null>(
    (state) => state.books.books
  );
  const loading = useSelector<RootState, boolean>(
    (state) => state.books.loading
  );

  const dispatch = useDispatch();

  const getBooks = useCallback(() => {
    dispatch(getBooksSagaStart());
  }, [dispatch]);

  return <List books={books} loading={loading} getBooks={getBooks} />;
}
```

<br>

```tsx
// src/components/List.tsx

import { Button, PageHeader, Table } from "antd";
import { useEffect } from "react";
import { BookType } from "../types";
import Layout from "./Layout";
import Book from "./Book";

interface ListProps {
  books: BookType[] | null;
  loading: boolean;
  getBooks: () => void;
}

const List: React.FC<ListProps> = ({ books, loading, getBooks }) => {
  useEffect(() => {
    getBooks();
  }, [getBooks]);

  const goAdd = () => {};
  const logout = () => {};

  return (
    <Layout>
      <PageHeader
        title={<div>Book List</div>}
        extra={[
          <Button key="2" type="primary" onClick={goAdd}>
            Add Book
          </Button>,
          <Button key="1" type="primary" onClick={logout}>
            Logout
          </Button>,
        ]}
      />
      <Table
        dataSource={books || []}
        columns={[
          {
            title: "Book",
            dataIndex: "book",
            key: "book",
            render: (text, record) => <Book {...record} />,
          },
        ]}
        loading={books === null || loading}
        showHeader={false}
        rowKey="bookId"
        pagination={false}
      />
    </Layout>
  );
};

export default List;
```

<br>

```ts
// src/redux/modules/books.ts

import { call, put, select, takeLatest } from "@redux-saga/core/effects";
import { createActions, handleActions } from "redux-actions";
import { BooksState, BookType } from "../../types";
import BookService from "../../services/BookService";

const initialState: BooksState = {
  books: null,
  loading: false,
  error: null,
};

const prefix = "my-books/books";

export const { pending, success, fail } = createActions(
  "PENDING",
  "SUCCESS",
  "FAIL",
  { prefix }
);

const reducer = handleActions<BooksState, BookType[]>(
  {
    PENDING: (state) => ({ ...state, loading: true, error: null }),
    SUCCESS: (state, action) => ({
      books: action.payload,
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
export const { getBooks } = createActions("GET_BOOKS", {
  prefix,
});

function* getBooksSaga() {
  try {
    yield put(pending());
    const token: string = yield select((state) => state.auth.token);
    const books: BookType[] = yield call(BookService.getBooks, token);
    yield put(success(books));
  } catch (error: any) {
    yield put(fail(new Error(error?.response?.data?.error || "UNKNOWN_ERROR")));
  }
}

export function* booksSaga() {
  yield takeLatest(`${prefix}/GET_BOOKS`, getBooksSaga);
}
```

<br>

```ts
// src/services/BookService.ts

import axios from "axios";
import { BookType } from "../types";

const BOOK_API_URL = "https://api.marktube.tv/v1/book";

export default class BookService {
  public static async getBooks(token: string): Promise<BookType[]> {
    const response = await axios.get(BOOK_API_URL, {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });
    return response.data;
  }
}
```

<br>

```bash
# terminal

$ npm i moment
```

<br>

```tsx
// src/components/Book.tsx

import { Link } from "react-router-dom";
import {
  BookOutlined,
  DeleteOutlined,
  EditOutlined,
  HomeOutlined,
} from "@ant-design/icons";
import { BookType } from "../types";
import moment from "moment";
import { Button, Tooltip } from "antd";
import styles from "./Book.module.css";

interface BookProps extends BookType {}

const Book: React.FC<BookProps> = ({
  bookId,
  title,
  author,
  createdAt,
  url,
}) => (
  <div className={styles.book}>
    <div className={styles.title}>
      <Link to={`/book/${bookId}`} className={styles.link_detail_title}>
        <BookOutlined /> {title}
      </Link>
    </div>
    <div className={styles.author}>
      <Link to={`/book/${bookId}`} className={styles.link_detail_author}>
        {author}
      </Link>
    </div>
    <div className={styles.created}>
      {moment(createdAt).format("MM-DD-YYYY hh:mm a")}
    </div>
    <div className={styles.tooltips}>
      <Tooltip title={url}>
        <a
          href={url}
          target="_BLANK"
          rel="noreferrer"
          className={styles.link_url}
        >
          <Button
            size="small"
            type="primary"
            shape="circle"
            icon={<HomeOutlined />}
            className={styles.button_url}
          />
        </a>
      </Tooltip>
      <Tooltip title="Edit">
        <Button
          size="small"
          shape="circle"
          icon={<EditOutlined />}
          className={styles.button_edit}
        />
      </Tooltip>
      <Tooltip title="Delete">
        <Button
          size="small"
          type="primary"
          shape="circle"
          danger
          icon={<DeleteOutlined />}
          className={styles.button_delete}
        />
      </Tooltip>
    </div>
  </div>
);

export default Book;
```

<br>

```css
/* src/components/Book.module.css */

.book {
  display: table;
  overflow: hidden;
}

.title {
  display: table-cell;
  vertical-align: middle;
  font-size: 14px;
  font-weight: bold;
  padding-left: 10px;
}

.link_detail_title {
  color: #0a222e;
}

.author {
  display: table-cell;
  vertical-align: middle;
  font-size: 14px;
  font-weight: bold;
  padding-left: 10px;
}

.link_detail_author {
  color: #28546a;
}

.created {
  color: #999999;
  display: table-cell;
  vertical-align: middle;
  font-size: 14px;
  padding-left: 10px;
}

.tooltips {
  color: #999999;
  display: table-cell;
  vertical-align: middle;
  font-size: 14px;
  padding-left: 10px;
}

.link_url {
  font-size: 12px;
}

.button_url {
  margin-right: 5px;
}

.button_edit {
  margin-right: 5px;
}
```

<br>

```tsx
// src/components/List.tsx

import { Button, PageHeader, Table } from "antd";
import { useEffect } from "react";
import { BookType } from "../types";
import Layout from "./Layout";
import Book from "./Book";
import styles from "./List.module.css";

interface ListProps {
  books: BookType[] | null;
  loading: boolean;
  error: Error | null;
  getBooks: () => void;
  logout: () => void;
}

const List: React.FC<ListProps> = ({
  books,
  loading,
  getBooks,
  error,
  logout,
}) => {
  useEffect(() => {
    getBooks();
  }, [getBooks]);

  useEffect(() => {
    if (error) {
      logout();
    }
  }, [error, logout]);

  const goAdd = () => {};

  return (
    <Layout>
      <PageHeader
        title={<div>Book List</div>}
        extra={[
          <Button
            key="2"
            type="primary"
            onClick={goAdd}
            className={styles.button}
          >
            Add Book
          </Button>,
          <Button
            key="1"
            type="primary"
            onClick={logout}
            className={styles.button}
          >
            Logout
          </Button>,
        ]}
      />
      <Table
        dataSource={books || []}
        columns={[
          {
            title: "Book",
            dataIndex: "book",
            key: "book",
            render: (text, record) => <Book {...record} />,
          },
        ]}
        loading={books === null || loading}
        showHeader={false}
        rowKey="bookId"
        pagination={false}
        className={styles.table}
      />
    </Layout>
  );
};

export default List;
```

<br>

```css
/* src/components/List.module.css */

.button {
  border-color: #28546a;
  background-color: #28546a;
  text-transform: uppercase;
  border-radius: 1px;
  border-width: 2px;
  color: white;
}

.table {
  margin-top: 30px;
}
```

<br>

```tsx
// src/containers/ListContainer.tsx

import { useCallback } from "react";
import { useDispatch, useSelector } from "react-redux";
import List from "../components/List";
import { BookType, RootState } from "../types";
import { getBooks as getBooksSagaStart } from "../redux/modules/books";
import { logout as logoutSagaStart } from "../redux/modules/auth";

export default function ListContainer() {
  const books = useSelector<RootState, BookType[] | null>(
    (state) => state.books.books
  );

  const loading = useSelector<RootState, boolean>(
    (state) => state.books.loading
  );

  const error = useSelector<RootState, Error | null>(
    (state) => state.books.error
  );

  const dispatch = useDispatch();

  const getBooks = useCallback(() => {
    dispatch(getBooksSagaStart());
  }, [dispatch]);

  const logout = useCallback(() => {
    dispatch(logoutSagaStart());
  }, [dispatch]);

  return (
    <List
      books={books}
      loading={loading}
      getBooks={getBooks}
      error={error}
      logout={logout}
    />
  );
}
```

<br>

![react-book5](https://user-images.githubusercontent.com/62803763/132704143-6ae7bd45-8652-4e3f-94e8-5ee1842ef5d6.PNG){: .align-center .open-new}

<br>

## 4. 책 추가하기

```tsx
// src/containers/ListContainer.tsx

import { useCallback } from "react";
import { useDispatch, useSelector } from "react-redux";
import List from "../components/List";
import { BookType, RootState } from "../types";
import { getBooks as getBooksSagaStart } from "../redux/modules/books";
import { logout as logoutSagaStart } from "../redux/modules/auth";
import { push } from "connected-react-router";

export default function ListContainer() {
  const books = useSelector<RootState, BookType[] | null>(
    (state) => state.books.books
  );

  const loading = useSelector<RootState, boolean>(
    (state) => state.books.loading
  );

  const error = useSelector<RootState, Error | null>(
    (state) => state.books.error
  );

  const dispatch = useDispatch();

  const getBooks = useCallback(() => {
    dispatch(getBooksSagaStart());
  }, [dispatch]);

  const logout = useCallback(() => {
    dispatch(logoutSagaStart());
  }, [dispatch]);

  const goAdd = useCallback(() => {
    dispatch(push("/add"));
  }, [dispatch]);

  return (
    <List
      books={books}
      loading={loading}
      getBooks={getBooks}
      error={error}
      logout={logout}
      goAdd={goAdd}
    />
  );
}
```

<br>

```tsx
// src/components/List.tsx

import { Button, PageHeader, Table } from "antd";
import { useEffect } from "react";
import { BookType } from "../types";
import Layout from "./Layout";
import Book from "./Book";
import styles from "./List.module.css";

interface ListProps {
  books: BookType[] | null;
  loading: boolean;
  error: Error | null;
  getBooks: () => void;
  logout: () => void;
  goAdd: () => void;
}

const List: React.FC<ListProps> = ({
  books,
  loading,
  getBooks,
  error,
  logout,
  goAdd,
}) => {
  useEffect(() => {
    getBooks();
  }, [getBooks]);

  useEffect(() => {
    if (error) {
      logout();
    }
  }, [error, logout]);

  return (
    <Layout>
      <PageHeader
        title={<div>Book List</div>}
        extra={[
          <Button
            key="2"
            type="primary"
            onClick={goAdd}
            className={styles.button}
          >
            Add Book
          </Button>,
          <Button
            key="1"
            type="primary"
            onClick={logout}
            className={styles.button}
          >
            Logout
          </Button>,
        ]}
      />
      <Table
        dataSource={books || []}
        columns={[
          {
            title: "Book",
            dataIndex: "book",
            key: "book",
            render: (text, record) => <Book {...record} />,
          },
        ]}
        loading={books === null || loading}
        showHeader={false}
        rowKey="bookId"
        pagination={false}
        className={styles.table}
      />
    </Layout>
  );
};

export default List;
```

<br>

```tsx
// src/components/Add.tsx

import { ForkOutlined } from "@ant-design/icons";
import { Button, Input, PageHeader, message as messageDialog } from "antd";
import TextArea from "antd/lib/input/TextArea";
import Layout from "./Layout";
import styles from "./Add.module.css";
import { useRef } from "react";
import TextAreaType from "rc-textarea";
import { BookReqType } from "../types";

interface AddProps {
  loading: boolean;
  back: () => void;
  logout: () => void;
  add: (book: BookReqType) => void;
}

const Add: React.FC<AddProps> = ({ loading, back, logout, add }) => {
  const titleRef = useRef<Input>(null);
  const messageRef = useRef<TextAreaType>(null);
  const authorRef = useRef<Input>(null);
  const urlRef = useRef<Input>(null);

  return (
    <Layout>
      <PageHeader
        onBack={back}
        title={
          <div>
            <ForkOutlined /> Add Book
          </div>
        }
        subTitle="Add Your Book"
        extra={[
          <Button
            key="1"
            type="primary"
            onClick={logout}
            className={styles.button_logout}
          >
            Logout
          </Button>,
        ]}
      />

      <div className={styles.add}>
        <div className={styles.input_title}>
          Title
          <span className={styles.required}> *</span>
        </div>
        <div className={styles.input_area}>
          <Input placeholder="Title" className={styles.input} ref={titleRef} />
        </div>
        <div className={styles.input_comment}>
          Comment
          <span className={styles.required}> *</span>
        </div>
        <div className={styles.input_area}>
          <TextArea
            rows={4}
            placeholder="Comment"
            className={styles.input}
            ref={messageRef}
          />
        </div>
        <div className={styles.input_author}>
          Author
          <span className={styles.required}> *</span>
        </div>
        <div className={styles.input_area}>
          <Input
            placeholder="Author"
            className={styles.input}
            ref={authorRef}
          />
        </div>
        <div className={styles.input_url}>
          URL
          <span className={styles.required}> *</span>
        </div>
        <div className={styles.input_area}>
          <Input placeholder="URL" className={styles.input} ref={urlRef} />
        </div>
        <div className={styles.button_area}>
          <Button
            size="large"
            loading={loading}
            onClick={click}
            className={styles.button}
          >
            Add
          </Button>
        </div>
      </div>
    </Layout>
  );

  function click() {
    const title = titleRef.current!.state.value;
    const message = messageRef.current!.resizableTextArea.props.value as string;
    const author = authorRef.current!.state.value;
    const url = urlRef.current!.state.value;

    if (
      title === undefined ||
      message === undefined ||
      author === undefined ||
      url === undefined
    ) {
      messageDialog.error("Please fill out all inputs");
      return;
    }

    add({
      title,
      message,
      author,
      url,
    });
  }
};

export default Add;
```

<br>

```tsx
// src/containers/AddContainer.tsx

import { goBack } from "connected-react-router";
import { useCallback } from "react";
import { useDispatch, useSelector } from "react-redux";
import Add from "../components/Add";
import { BookReqType, RootState } from "../types";
import { logout as logoutSagaStart } from "../redux/modules/auth";
import { addBook as addBookSagaStart } from "../redux/modules/books";

const AddContainer = () => {
  const loading = useSelector<RootState, boolean>(
    (state) => state.books.loading
  );

  const dispatch = useDispatch();

  const back = useCallback(() => {
    dispatch(goBack());
  }, [dispatch]);

  const logout = useCallback(() => {
    dispatch(logoutSagaStart());
  }, [dispatch]);

  const add = useCallback(
    (book: BookReqType) => {
      dispatch(addBookSagaStart(book));
    },
    [dispatch]
  );

  return <Add loading={loading} back={back} logout={logout} add={add} />;
};

export default AddContainer;
```

<br>

```tsx
// src/pages/Add.tsx

import { Redirect } from "react-router";
import AddContainer from "../containers/AddContainer";
import useToken from "../hooks/useToken";

export default function Add() {
  const token = useToken();

  if (token === null) {
    return <Redirect to="/signin" />;
  }

  return <AddContainer />;
}
```

<br>

```ts
// src/hooks/useToken.ts

import { useSelector } from "react-redux";
import { RootState } from "../types";

export default function useToken() {
  const token = useSelector<RootState, string | null>(
    (state) => state.auth.token
  );

  return token;
}
```

<br>

```tsx
// src/pages/Home.tsx

import { Redirect } from "react-router-dom";
import ListContainer from "../containers/ListContainer";
import useToken from "../hooks/useToken";

export default function Home() {
  const token = useToken();

  if (token === null) {
    return <Redirect to="/signin" />;
  }

  return <ListContainer />;
}
```

<br>

```tsx
// src/pages/Signin.tsx

import { Redirect } from "react-router";
import SigninContainer from "../containers/SigninContainer";
import useToken from "../hooks/useToken";

export default function Signin() {
  const token = useToken();

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

export interface BooksState {
  books: BookType[] | null;
  loading: boolean;
  error: Error | null;
}

export interface RootState {
  auth: AuthState;
  books: BooksState;
  router: Reducer<RouterState<unknown>, AnyAction>;
}

export interface BookType {
  bookId: number;
  title: string;
  author: string;
  createdAt: string;
  url: string;
}

export interface BookReqType {
  title: string;
  message: string;
  author: string;
  url: string;
}
```

<br>

```ts
// src/redux/modules/books.ts

import {
  call,
  put,
  select,
  takeEvery,
  takeLatest,
} from "@redux-saga/core/effects";
import { Action, createActions, handleActions } from "redux-actions";
import { BookReqType, BooksState, BookType } from "../../types";
import BookService from "../../services/BookService";
import { push } from "connected-react-router";

const initialState: BooksState = {
  books: null,
  loading: false,
  error: null,
};

const prefix = "my-books/books";

export const { pending, success, fail } = createActions(
  "PENDING",
  "SUCCESS",
  "FAIL",
  { prefix }
);

const reducer = handleActions<BooksState, BookType[]>(
  {
    PENDING: (state) => ({ ...state, loading: true, error: null }),
    SUCCESS: (state, action) => ({
      books: action.payload,
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
export const { getBooks, addBook } = createActions("GET_BOOKS", "ADD_BOOK", {
  prefix,
});

function* getBooksSaga() {
  try {
    yield put(pending());
    const token: string = yield select((state) => state.auth.token);
    const books: BookType[] = yield call(BookService.getBooks, token);
    yield put(success(books));
  } catch (error: any) {
    yield put(fail(new Error(error?.response?.data?.error || "UNKNOWN_ERROR")));
  }
}

function* addBookSaga(action: Action<BookReqType>) {
  try {
    yield put(pending());
    const token: string = yield select((state) => state.auth.token);
    const book: BookType = yield call(
      BookService.addBook,
      token,
      action.payload
    );
    const books: BookType[] = yield select((state) => state.books.books);
    yield put(success([...books, book]));
    yield put(push("/"));
  } catch (error: any) {
    yield put(fail(new Error(error?.response?.data?.error || "UNKNOWN_ERROR")));
  }
}

export function* booksSaga() {
  yield takeLatest(`${prefix}/GET_BOOKS`, getBooksSaga);
  yield takeEvery(`${prefix}/ADD_BOOK`, addBookSaga);
}
```

<br>

```ts
// src/services/BookService.ts

import axios from "axios";
import { BookReqType, BookType } from "../types";

const BOOK_API_URL = "https://api.marktube.tv/v1/book";

export default class BookService {
  public static async getBooks(token: string): Promise<BookType[]> {
    const response = await axios.get(BOOK_API_URL, {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });
    return response.data;
  }

  public static async addBook(
    token: string,
    book: BookReqType
  ): Promise<BookType> {
    const response = await axios.post(BOOK_API_URL, book, {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });
    return response.data;
  }
```

<br>

```css
/* src/components/Add.module.css */

.bg {
  width: 100%;
}

.add {
  width: 800px;
  margin-left: auto;
  margin-right: auto;
}

.input_title {
  font-family: Roboto;
  font-size: 12px;
  font-weight: bold;
  margin-top: 40px;
  text-align: left;
  padding-left: 40px;
}

.input_comment {
  font-family: Roboto;
  font-size: 12px;
  font-weight: bold;
  margin-top: 10px;
  text-align: left;
  padding-left: 40px;
}

.input_author {
  font-family: Roboto;
  font-size: 12px;
  font-weight: bold;
  margin-top: 10px;
  text-align: left;
  padding-left: 40px;
}

.input_url {
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
}

.input {
  width: 720px;
  border-radius: 1px;
  border-width: 1px;
  font-family: Roboto;
  margin-left: 40px;
  margin-right: 40px;
  min-height: 100;
}

.button_area {
  text-align: right;
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
  width: 120px;
}

.button:hover {
  background-color: #28546a;
  color: white;
}

.button_logout {
  border-color: #28546a;
  background-color: #28546a;
  text-transform: uppercase;
  border-radius: 1px;
  border-width: 2px;
  color: white;
}
```

<br>

![react-book6](https://user-images.githubusercontent.com/62803763/132950566-4e0e0d3d-7b37-4889-a95f-5d700ae3fb16.PNG){: .align-center .open-new}

![react-book7](https://user-images.githubusercontent.com/62803763/132950567-4dd18ac2-baf9-4ae4-8d5a-e553c325ad19.PNG){: .align-center .open-new}

![react-book8](https://user-images.githubusercontent.com/62803763/132950568-5cccb7ce-963a-47f2-a57c-6fe06c969220.PNG){: .align-center .open-new}

<br>

## 5. 책 삭제하기

```tsx
// src/components/Book.tsx

import { Link } from "react-router-dom";
import {
  BookOutlined,
  DeleteOutlined,
  EditOutlined,
  HomeOutlined,
} from "@ant-design/icons";
import { BookType } from "../types";
import moment from "moment";
import { Button, Tooltip } from "antd";
import styles from "./Book.module.css";

interface BookProps extends BookType {
  deleteBook: (bookId: number) => void;
}

const Book: React.FC<BookProps> = ({
  bookId,
  title,
  author,
  createdAt,
  url,
  deleteBook,
}) => {
  return (
    <div className={styles.book}>
      <div className={styles.title}>
        <Link to={`/book/${bookId}`} className={styles.link_detail_title}>
          <BookOutlined /> {title}
        </Link>
      </div>
      <div className={styles.author}>
        <Link to={`/book/${bookId}`} className={styles.link_detail_author}>
          {author}
        </Link>
      </div>
      <div className={styles.created}>
        {moment(createdAt).format("MM-DD-YYYY hh:mm a")}
      </div>
      <div className={styles.tooltips}>
        <Tooltip title={url}>
          <a
            href={url}
            target="_BLANK"
            rel="noreferrer"
            className={styles.link_url}
          >
            <Button
              size="small"
              type="primary"
              shape="circle"
              icon={<HomeOutlined />}
              className={styles.button_url}
            />
          </a>
        </Tooltip>
        <Tooltip title="Edit">
          <Button
            size="small"
            shape="circle"
            icon={<EditOutlined />}
            className={styles.button_edit}
          />
        </Tooltip>
        <Tooltip title="Delete">
          <Button
            size="small"
            type="primary"
            shape="circle"
            danger
            icon={<DeleteOutlined />}
            className={styles.button_delete}
            onClick={clickDelete}
          />
        </Tooltip>
      </div>
    </div>
  );

  function clickDelete() {
    deleteBook(bookId);
  }
};

export default Book;
```

<br>

```tsx
// src/components/List.tsx

import { Button, PageHeader, Table } from "antd";
import { useEffect } from "react";
import { BookType } from "../types";
import Layout from "./Layout";
import Book from "./Book";
import styles from "./List.module.css";

interface ListProps {
  books: BookType[] | null;
  loading: boolean;
  error: Error | null;
  getBooks: () => void;
  logout: () => void;
  goAdd: () => void;
  deleteBook: (bookId: number) => void;
}

const List: React.FC<ListProps> = ({
  books,
  loading,
  getBooks,
  error,
  logout,
  goAdd,
  deleteBook,
}) => {
  useEffect(() => {
    getBooks();
  }, [getBooks]);

  useEffect(() => {
    if (error) {
      logout();
    }
  }, [error, logout]);

  return (
    <Layout>
      <PageHeader
        title={<div>Book List</div>}
        extra={[
          <Button
            key="2"
            type="primary"
            onClick={goAdd}
            className={styles.button}
          >
            Add Book
          </Button>,
          <Button
            key="1"
            type="primary"
            onClick={logout}
            className={styles.button}
          >
            Logout
          </Button>,
        ]}
      />
      <Table
        dataSource={books || []}
        columns={[
          {
            title: "Book",
            dataIndex: "book",
            key: "book",
            render: (text, record) => (
              <Book {...record} deleteBook={deleteBook} />
            ),
          },
        ]}
        loading={books === null || loading}
        showHeader={false}
        rowKey="bookId"
        pagination={false}
        className={styles.table}
      />
    </Layout>
  );
};

export default List;
```

<br>

```tsx
// src/containers/ListContainer.tsx

import { useCallback } from "react";
import { useDispatch, useSelector } from "react-redux";
import List from "../components/List";
import { BookType, RootState } from "../types";
import {
  getBooks as getBooksSagaStart,
  deleteBook as deleteBookSagaStart,
} from "../redux/modules/books";
import { logout as logoutSagaStart } from "../redux/modules/auth";
import { push } from "connected-react-router";

export default function ListContainer() {
  const books = useSelector<RootState, BookType[] | null>(
    (state) => state.books.books
  );

  const loading = useSelector<RootState, boolean>(
    (state) => state.books.loading
  );

  const error = useSelector<RootState, Error | null>(
    (state) => state.books.error
  );

  const dispatch = useDispatch();

  const getBooks = useCallback(() => {
    dispatch(getBooksSagaStart());
  }, [dispatch]);

  const logout = useCallback(() => {
    dispatch(logoutSagaStart());
  }, [dispatch]);

  const goAdd = useCallback(() => {
    dispatch(push("/add"));
  }, [dispatch]);

  const deleteBook = useCallback(
    (bookId: number) => {
      dispatch(deleteBookSagaStart(bookId));
    },
    [dispatch]
  );

  return (
    <List
      books={books}
      loading={loading}
      getBooks={getBooks}
      error={error}
      logout={logout}
      goAdd={goAdd}
      deleteBook={deleteBook}
    />
  );
}
```

<br>

```ts
// src/services/BookService.ts

import axios from "axios";
import { BookReqType, BookType } from "../types";

const BOOK_API_URL = "https://api.marktube.tv/v1/book";

export default class BookService {
  public static async getBooks(token: string): Promise<BookType[]> {
    const response = await axios.get(BOOK_API_URL, {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });
    return response.data;
  }

  public static async addBook(
    token: string,
    book: BookReqType
  ): Promise<BookType> {
    const response = await axios.post(BOOK_API_URL, book, {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });
    return response.data;
  }

  public static async deleteBook(token: string, bookId: number) {
    await axios.delete(`${BOOK_API_URL}/${bookId}`, {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });
  }
}
```

<br>

```ts
// src/redux/modules/books.ts

import {
  call,
  put,
  select,
  takeEvery,
  takeLatest,
} from "@redux-saga/core/effects";
import { Action, createActions, handleActions } from "redux-actions";
import { BookReqType, BooksState, BookType } from "../../types";
import BookService from "../../services/BookService";
import { push } from "connected-react-router";

const initialState: BooksState = {
  books: null,
  loading: false,
  error: null,
};

const prefix = "my-books/books";

export const { pending, success, fail } = createActions(
  "PENDING",
  "SUCCESS",
  "FAIL",
  { prefix }
);

const reducer = handleActions<BooksState, BookType[]>(
  {
    PENDING: (state) => ({ ...state, loading: true, error: null }),
    SUCCESS: (state, action) => ({
      books: action.payload,
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
export const { getBooks, addBook, deleteBook } = createActions(
  "GET_BOOKS",
  "ADD_BOOK",
  "DELETE_BOOK",
  {
    prefix,
  }
);

function* getBooksSaga() {
  try {
    yield put(pending());
    const token: string = yield select((state) => state.auth.token);
    const books: BookType[] = yield call(BookService.getBooks, token);
    yield put(success(books));
  } catch (error: any) {
    yield put(fail(new Error(error?.response?.data?.error || "UNKNOWN_ERROR")));
  }
}

function* addBookSaga(action: Action<BookReqType>) {
  try {
    yield put(pending());
    const token: string = yield select((state) => state.auth.token);
    const book: BookType = yield call(
      BookService.addBook,
      token,
      action.payload
    );
    const books: BookType[] = yield select((state) => state.books.books);
    yield put(success([...books, book]));
    yield put(push("/"));
  } catch (error: any) {
    yield put(fail(new Error(error?.response?.data?.error || "UNKNOWN_ERROR")));
  }
}

function* deleteBookSaga(action: Action<number>) {
  try {
    const bookId = action.payload;
    yield put(pending());
    const token: string = yield select((state) => state.auth.token);
    yield call(BookService.deleteBook, token, bookId);
    const books: BookType[] = yield select((state) => state.books.books);
    yield put(success(books.filter((book) => book.bookId !== bookId)));
  } catch (error: any) {
    yield put(fail(new Error(error?.response?.data.error || "UNKNOWN_ERROR")));
  }
}

export function* booksSaga() {
  yield takeLatest(`${prefix}/GET_BOOKS`, getBooksSaga);
  yield takeEvery(`${prefix}/ADD_BOOK`, addBookSaga);
  yield takeEvery(`${prefix}/DELETE_BOOK`, deleteBookSaga);
}
```

<br>

![react-book9](https://user-images.githubusercontent.com/62803763/133085750-1c04a344-d518-4911-a7cb-1f29be72ad39.PNG){: .align-center .open-new}

![react-book10](https://user-images.githubusercontent.com/62803763/133085756-cf227712-8e59-497d-a41a-5404e7615968.PNG){: .align-center .open-new}
