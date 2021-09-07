---
title: "[Redux] Redux-actions"
excerpt: Ducks 패턴을 쉽게 구현하게 해주는 라이브러리
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
date: "2021-09-07T22:00:00"
last_modified_at: 2021-09-07T22:00:00
---

## Redux-actions

- Ducks 패턴을 쉽게 구현하게 해주는 라이브러리

```bash
# terminal

$ npm i redux-actions
```

<br>

```js
// src/redux/modules/filter.js

import { createActions, handleActions } from "redux-actions";

export const { showAll, showComplete } = createActions(
  "SHOW_ALL",
  "SHOW_COMPLETE",
  {
    prefix: "redux-start/filter",
  }
);

// 초기값
const initialState = "ALL";

const reducer = handleActions(
  {
    SHOW_ALL: (state, action) => "ALL",
    SHOW_COMPLETE: () => "COMPLETE",
  },
  initialState,
  { prefix: "redux-start/filter" }
);

// 리듀서
export default reducer;
```
