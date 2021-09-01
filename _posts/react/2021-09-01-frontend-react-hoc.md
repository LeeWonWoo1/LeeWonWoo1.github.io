---
title: "[React] High Order Component"
excerpt: React High Order Component
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
toc: true
toc_sticky: true
popular: true
date: "2021-09-01T23:00:00"
last_modified_at: 2021-09-01T23:00:00
---

## HOC (Higher-Order Components)

- Component안의 로직을 다시 재활용할 수 있는 기수
- React API와는 관련이 없음
- HOC = function(컴포넌트) { return 새로운 컴포넌트; }
- 즉, HOC는 컴포넌트를 인자로 받아 새로운 컴포넌트를 리턴하는 함수
- 보통 with가 붙은 함수가 HOC인 경우가 많음

![react-hoc](https://user-images.githubusercontent.com/62803763/131686692-4f4a597f-0dfb-4387-8e10-134a8ec23cb5.PNG){: .align-center .open-new}

<br>

```js
// export default withRouter(LoginButton);

import React from "react";
import { withRouter } from "react-router-dom";

const LoginButton = (props) => {
  console.log(props);
  function login() {
    setTimeout(() => {
      props.history.push("/");
    }, 1000);
  }
  return <button onClick={login}>로그인</button>;
};

export default withRouter(LoginButton);
```

<br>

### - 사용법

- Use HOCs For Cross-Cutting Concerns
- Don't Matate the Original Component. Use Composition
- Pass Unrelated Props Through to the Wrapped Component
- Maximizing Composability
- Wrap the Display Name for Easy Debugging

<br>

### - 주의할 점

- Don't Use HOCs Inside the render Method
- Static Methods Must Be Copied Over
- Refs Aren't Passed Through (feat. React.forwardRef)

```js
export default MyComponent;

// export the mothod separately
export { someFunction };

// and in the consuming module, import both
import MyComponent, { someFUnction } from "./MyComponent.js";
```
