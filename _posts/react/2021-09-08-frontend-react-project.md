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
