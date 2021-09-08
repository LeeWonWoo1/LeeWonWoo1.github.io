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
