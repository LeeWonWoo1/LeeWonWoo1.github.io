---
title: "[Redux] React-router-dom과 함께 쓰기"
excerpt: Redux with React-router-dom
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
date: "2021-09-07T14:00:00"
last_modified_at: 2021-09-07T14:00:00
---

## connected-react-router

```bash
# terminal

$ npm i react-router-dom
```

<br>

```js
// src/App.js

import "./App.css";
import { Router, Route } from "react-router-dom";
import Home from "./pages/Home";
import Todos from "./pages/Todos";
import Users from "./pages/Users";
import history from "./history";

function App() {
  return (
    <Router history={history}>
      <Route path="/" exact component={Home} />
      <Route path="/todos" exact component={Todos} />
      <Route path="/users" exact component={Users} />
    </Router>
  );
}

export default App;
```

<br>

```jsx
// src/pages/Home.jsx

import { Link } from "react-router-dom";

export default function Home() {
  return (
    <div>
      <h1>Home</h1>
      <ul>
        <li>
          <Link to="/todos">Todos</Link>
        </li>
        <li>
          <Link to="/users">Users</Link>
        </li>
      </ul>
    </div>
  );
}
```

<br>

```jsx
// src/pages/Todos.jsx

import TodoFormContainer from "../containers/TodoFormContainer";
import TodoListContainer from "../containers/TodoListContainer";

export default function Todos() {
  return (
    <div>
      <TodoListContainer />
      <TodoFormContainer />
    </div>
  );
}
```

<br>

```jsx
// src/pages/Users.jsx

import UserListContainer from "../containers/UserListContainer";

export default function Users() {
  return (
    <div>
      <UserListContainer />
    </div>
  );
}
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

const store = createStore(
  todoApp,
  composeWithDevTools(
    applyMiddleware(thunk.withExtraArgument({ history }), promise)
  )
);

export default store;
```

<br>

```js
// src/history.js

import { createBrowserHistory } from "history";

const history = createBrowserHistory();

export default history;
```

<br>

```jsx
// src/containers/UserListContainer.jsx

import { useCallback } from "react";
import { useDispatch, useSelector } from "react-redux";
import UserList from "../components/UserList";
import { getUsersThunk } from "../redux/modules/users";

export default function UserListContainer() {
  const users = useSelector((state) => state.users.data);
  const dispatch = useDispatch();

  const getUsers = useCallback(() => {
    dispatch(getUsersThunk());
  }, [dispatch]);

  return <UserList users={users} getUsers={getUsers} />;
}
```

<br>

```js
// src/redux/modules/users.js

import axios from "axios";

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
```

![redux-router1](https://user-images.githubusercontent.com/62803763/132340931-f949b0c7-c290-4b1a-ac75-7c210e59e258.PNG){: .align-center .open-new}

![redux-router2](https://user-images.githubusercontent.com/62803763/132340936-b9dbf783-c8da-4e4b-982f-a110a063989a.PNG){: .align-center .open-new}

![redux-router3](https://user-images.githubusercontent.com/62803763/132340938-ff3ecf7b-61ce-4c79-8406-9e032992ea59.PNG){: .align-center .open-new}

<br>

```bash
# terminal

$ npm i connected-react-router
```

<br>

```js
// src/redux/modules/reducer.js

import { combineReducers } from "redux";
import todos from "./todos";
import filter from "./filter";
import users from "./users";
import { connectRouter } from "connected-react-router";
import history from "../../history";

const reducer = combineReducers({
  todos,
  filter,
  users,
  router: connectRouter(history),
});

export default reducer;
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

const store = createStore(
  todoApp,
  composeWithDevTools(
    applyMiddleware(
      thunk.withExtraArgument({ history }),
      promise,
      routerMiddleware(history)
    )
  )
);

export default store;
```

<br>

```js
// src/App.js

import "./App.css";
import { Router, Route } from "react-router-dom";
import Home from "./pages/Home";
import Todos from "./pages/Todos";
import Users from "./pages/Users";
import history from "./history";
import { ConnectedRouter } from "connected-react-router";

function App() {
  return (
    <ConnectedRouter history={history}>
      <Route path="/" exact component={Home} />
      <Route path="/todos" exact component={Todos} />
      <Route path="/users" exact component={Users} />
    </ConnectedRouter>
  );
}

export default App;
```

<br>

```jsx
// src/pages/Home.jsx

import { push } from "connected-react-router";
import { useDispatch } from "react-redux";
import { Link } from "react-router-dom";

export default function Home() {
  const dispatch = useDispatch();

  return (
    <div>
      <h1>Home</h1>
      <ul>
        <li>
          <Link to="/todos">Todos</Link>
        </li>
        <li>
          <Link to="/users">Users</Link>
        </li>
      </ul>
      <button onClick={click}>todos로 이동</button>
    </div>
  );

  function click() {
    dispatch(push("/todos"));
  }
}
```

![redux-router4](https://user-images.githubusercontent.com/62803763/132342679-165c1a47-0a18-4c02-a3a0-a66154e636ec.PNG){: .align-center .open-new}

![redux-router5](https://user-images.githubusercontent.com/62803763/132342686-658ffae0-d50e-4eeb-94c7-5be34291707a.PNG){: .align-center .open-new}
