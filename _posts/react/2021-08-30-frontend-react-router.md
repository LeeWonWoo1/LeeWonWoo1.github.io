---
title: "[React] Router"
excerpt: React Router
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
toc: true
toc_sticky: true
popular: true
date: "2021-08-30T23:00:00"
last_modified_at: 2021-08-30T23:00:00
---

## 1. React Routing 이해하기

- Single Page Application
  - 기존에는 서버로부터 해당 url에 대한 데이터를 받아옴
  - 이제는 서버로부터 하나의 전체 App 받아온 후 클라이언트(Browser)에서 url에 따라서 어떤 것을 보여줄지 결정
- SPA 라우팅 과정
  1. 브라우저에서 최초에 '/' 경로로 요청
  2. React Web App을 내려줌
  3. 내려받은 React App에서 '/' 경로에 맞는 Component를 보여줌
  4. React App에서 다른 페이지로 이동하는 동작을 수행하면,
  5. 새로운 경로에 맞는 Component를 보여줌
- cra에 기본 내장된 패키지가 아님
- react-router-dom은 Facebook의 공식 패키지는 아님
- 가장 대표적인 라우팅 패키지

```bash
# terminal

$ npx create-react-app react-router-example
$ cd react-router-example
$ npm i react-router-dom
$ code .
$ npm start
```

<br>

- 특정 경로에서 보여줄 component 준비
  - '/' => Home Component
  - '/profile' => Profile Component
  - '/about' => About Component

```jsx
// src/pages/Home.jsx

export default function Home() {
  return <div>Home 페이지</div>;
}

// src/pages/Profile.jsx
export default function Profile() {
  return <div>Profile 페이지</div>;
}

// src/pages/About.jsx
export default function About() {
  return <div>About 페이지</div>;
}
```

<br>

```js
// src/App.js

// Route Component에 path와 component를 설정하여 나열
import { BrowserRouter, Route } from "react-router-dom";
import About from "./pages/About";
import Home from "./pages/Home";
import Profile from "./pages/Profile";

function App() {
  return (
    // BrowserRouter로 Route를 감싸줌
    // Browser에서 요청한 경로에 Route의 path가 들어있으면 해당 Component를 보여줌
    <BrowserRouter>
      <Route path="/" exact component={Home} />
      <Route path="/profile" component={Profile} />
      <Route path="/about" component={About} />
    </BrowserRouter>
  );
}

export default App;
```

<br>

![react-router1](https://user-images.githubusercontent.com/62803763/131361573-8ad896f6-9731-4b58-bef6-b0b7d9194d2f.PNG){: .align-center .open-new}

![react-router2](https://user-images.githubusercontent.com/62803763/131361609-419931cd-78de-4fb9-8610-41f52c109d0a.PNG){: .align-center .open-new}

![react-router3](https://user-images.githubusercontent.com/62803763/131361633-ff0bb00b-eed1-4c63-8023-441fd8981cc8.PNG){: .align-center .open-new}

<br>

## 2. Dynamic Routing

```js
// src/App.js

import { BrowserRouter, Route } from "react-router-dom";
import About from "./pages/About";
import Home from "./pages/Home";
import Profile from "./pages/Profile";

function App() {
  return (
    <BrowserRouter>
      <Route path="/" exact component={Home} />
      <Route path="/profile" exact component={Profile} />
      <Route path="/profile/:id" component={Profile} />
      <Route path="/about" component={About} />
    </BrowserRouter>
  );
}

export default App;
```

<br>

```jsx
// src/pages/Profile.jsx

export default function Profile(props) {
  const id = props.match.params.id;
  console.log(id, typeof id);
  return (
    <div>
      <h2>Profile 페이지</h2>
      {id && <p>id는 {id}입니다.</p>}
    </div>
  );
}
```

<br>

![react-router4](https://user-images.githubusercontent.com/62803763/131369788-ef1f4ec7-e55a-4f40-917d-b815b3dcbed2.PNG){: .align-center .open-new}

<br>

```jsx
// src/pages/About.jsx

export default function About(props) {
  const searchParams = props.location.search;
  console.log(searchParams);
  const obj = new URLSearchParams(searchParams);
  console.log(obj.get("name"));
  return <div>About 페이지</div>;
}

// ---------------------------------------------------

import queryString from "query-string";

export default function About(props) {
  const searchParams = props.location.search;
  console.log(searchParams);
  const query = queryString.parse(searchParams);
  console.log(query);
  return (
    <div>
      <h2>About 페이지</h2>
      {query.name && <p>name은 {query.name} 입니다.</p>}
    </div>
  );
}
```

<br>

![react-router5](https://user-images.githubusercontent.com/62803763/131373124-07a59b60-9c15-454e-8e2a-62f91bef13d0.PNG){: .align-center .open-new}

<br>

![react-router6](https://user-images.githubusercontent.com/62803763/131373358-fe56abcc-6e84-4311-9247-a644e6473216.PNG){: .align-center .open-new}

<br>

## 3. Switch와 NotFound

- 여러 Route 중 순서대로 먼저 맞는 하나만 보여줌
- exact를 뺄 수 있는 로직을 만들 수 있음
- 가장 마지막에 어디 path에도 맞지 않으면 보여지는 Component를 설정해서, "Not Found" 페이지를 만들 수 있음

```js
// src/App.js

import { BrowserRouter, Route, Switch } from "react-router-dom";
import About from "./pages/About";
import Home from "./pages/Home";
import Profile from "./pages/Profile";
import NotFound from "./pages/NotFound";

function App() {
  return (
    <BrowserRouter>
      <Switch>
        <Route path="/profile/:id" component={Profile} />
        <Route path="/profile" component={Profile} />
        <Route path="/about" component={About} />
        <Route path="/" exact component={Home} />
        <Route component={NotFound} />
      </Switch>
    </BrowserRouter>
  );
}

export default App;
```

<br>

```jsx
// src/pages/NotFound.jsx

export default function NotFound() {
  return <div>페이지를 찾을 수 없습니다.</div>;
}
```

<br>

![react-router4](https://user-images.githubusercontent.com/62803763/131369788-ef1f4ec7-e55a-4f40-917d-b815b3dcbed2.PNG){: .align-center .open-new}

![react-router2](https://user-images.githubusercontent.com/62803763/131361609-419931cd-78de-4fb9-8610-41f52c109d0a.PNG){: .align-center .open-new}

![react-router7](https://user-images.githubusercontent.com/62803763/131375570-be98e5b3-0cc6-4775-9e51-28932fb74b3d.PNG){: .align-center .open-new}

![react-router1](https://user-images.githubusercontent.com/62803763/131361573-8ad896f6-9731-4b58-bef6-b0b7d9194d2f.PNG){: .align-center .open-new}

![react-router8](https://user-images.githubusercontent.com/62803763/131375597-361ba213-9625-481a-9828-40e712edb930.PNG){: .align-center .open-new}

<br>

## 4. JSX 링크로 Routing 이동하기

```js
// src/App.js

import { BrowserRouter, Route, Switch } from "react-router-dom";
import About from "./pages/About";
import Home from "./pages/Home";
import Profile from "./pages/Profile";
import NotFound from "./pages/NotFound";
import Links from "./components/Links";

function App() {
  return (
    <BrowserRouter>
      <Links />
      <Switch>
        <Route path="/profile/:id" component={Profile} />
        <Route path="/profile" component={Profile} />
        <Route path="/about" component={About} />
        <Route path="/" exact component={Home} />
        <Route component={NotFound} />
      </Switch>
    </BrowserRouter>
  );
}

export default App;
```

<br>

```jsx
// src/components/Links.jsx

import { Link } from "react-router-dom";

export default function Links() {
  return (
    <ul>
      <li>
        <Link to="/">Home</Link>
      </li>
      <li>
        <Link to="/profile">Profile</Link>
      </li>
      <li>
        <Link to="/profile/LWW">Profile/LWW</Link>
      </li>
      <li>
        <Link to="/about">About</Link>
      </li>
      <li>
        <Link to="/about?name=LWW">About?name=LWW</Link>
      </li>
    </ul>
  );
}
```

<br>

![react-router9](https://user-images.githubusercontent.com/62803763/131377349-8b6f6eab-847a-4220-ba07-6144956b7f18.PNG){: .align-center .open-new}

<br>

- import { NavLink } from 'react-router-dom';
- activeClassName, activeStyle처럼 active 상태에 대한 스타일 지정 가능
- Route의 path처럼 동작하기 때문에 exact가 있음

```js
// src/App.js

import { BrowserRouter, Route, Switch } from "react-router-dom";
import About from "./pages/About";
import Home from "./pages/Home";
import Profile from "./pages/Profile";
import NotFound from "./pages/NotFound";
import Links from "./components/Links";
import NavLinks from "./components/NavLinks";

function App() {
  return (
    <BrowserRouter>
      <Links />
      <NavLinks />
      <Switch>
        <Route path="/profile/:id" component={Profile} />
        <Route path="/profile" component={Profile} />
        <Route path="/about" component={About} />
        <Route path="/" exact component={Home} />
        <Route component={NotFound} />
      </Switch>
    </BrowserRouter>
  );
}

export default App;
```

<br>

```jsx
// src/components/NavLinks.jsx

import { NavLink } from "react-router-dom";

const activeStyle = { color: "royalblue" };

export default function NavLinks() {
  return (
    <ul>
      <li>
        <NavLink to="/" exact activeStyle={activeStyle}>
          Home
        </NavLink>
      </li>
      <li>
        <NavLink to="/profile" exact activeStyle={activeStyle}>
          Profile
        </NavLink>
      </li>
      <li>
        <NavLink to="/profile/LWW" activeStyle={activeStyle}>
          Profile/LWW
        </NavLink>
      </li>
      <li>
        <NavLink
          to="/about"
          activeStyle={activeStyle}
          isActive={(match, location) => {
            console.log(match, location);
            return match !== null && location.search === "";
          }}
        >
          About
        </NavLink>
      </li>
      <li>
        <NavLink
          to="/about?name=LWW"
          activeStyle={activeStyle}
          isActive={(match, location) => {
            return match !== null && location.search === "?name=LWW";
          }}
        >
          About?name=LWW
        </NavLink>
      </li>
    </ul>
  );
}
```

<br>

![react-router10](https://user-images.githubusercontent.com/62803763/131379030-267ecaec-e468-4263-a740-7e6219ec12cb.PNG){: .align-center .open-new}

<br>

## 5. JS로 Routing 이동하기

```js
// src/App.js

import { BrowserRouter, Route, Switch } from "react-router-dom";
import About from "./pages/About";
import Home from "./pages/Home";
import Profile from "./pages/Profile";
import NotFound from "./pages/NotFound";
import Login from "./pages/Login";
import Links from "./components/Links";
import NavLinks from "./components/NavLinks";

function App() {
  return (
    <BrowserRouter>
      <Links />
      <NavLinks />
      <Switch>
        <Route path="/login" component={Login} />
        <Route path="/profile/:id" component={Profile} />
        <Route path="/profile" component={Profile} />
        <Route path="/about" component={About} />
        <Route path="/" exact component={Home} />
        <Route component={NotFound} />
      </Switch>
    </BrowserRouter>
  );
}

export default App;
```

<br>

```jsx
// src/pages/Login.jsx

import LoginButton from "../components/LoginButton";

export default function Login() {
  return (
    <div>
      <h2>Login 페이지</h2>
      <LoginButton />
    </div>
  );
}
```

<br>

```jsx
// src/components/LoginButton.jsx

import { withRouter } from "react-router-dom";

export default withRouter(function LoginButton(props) {
  console.log(props);

  function login() {
    setTimeout(() => {
      props.history.push("/");
    }, 1000);
  }

  return <button onClick={login}>로그인하기</button>;
});
```

<br>

![react-router11](https://user-images.githubusercontent.com/62803763/131381551-73430641-c3a7-40a6-b7d4-1420dd9ab241.PNG){: .align-center .open-new}

![react-router12](https://user-images.githubusercontent.com/62803763/131381838-d753c963-ea27-4b3c-ae5a-791efc1510c5.PNG){: .align-center .open-new}

<br>

## 6. Redirect

```js
// src/App.js

import { BrowserRouter, Redirect, Route, Switch } from "react-router-dom";
import About from "./pages/About";
import Home from "./pages/Home";
import Profile from "./pages/Profile";
import NotFound from "./pages/NotFound";
import Login from "./pages/Login";
import Links from "./components/Links";
import NavLinks from "./components/NavLinks";

const isLogin = false;

function App() {
  return (
    <BrowserRouter>
      <Links />
      <NavLinks />
      <Switch>
        <Route
          path="/login"
          render={() => (isLogin ? <Redirect to="/" /> : <Login />)}
        />
        <Route path="/profile/:id" component={Profile} />
        <Route path="/profile" component={Profile} />
        <Route path="/about" component={About} />
        <Route path="/" exact component={Home} />
        <Route component={NotFound} />
      </Switch>
    </BrowserRouter>
  );
}

export default App;
```

<br>

![react-router11](https://user-images.githubusercontent.com/62803763/131382362-3b625b08-5827-4beb-9dd7-3c71b7c768c0.PNG){: .align-center .open-new}
