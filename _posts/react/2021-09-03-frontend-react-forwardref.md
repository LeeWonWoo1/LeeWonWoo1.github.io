---
title: "[React] forwardRef"
excerpt: 하위 Component의 레퍼런스를 상위 Component에서 이용
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
toc: true
toc_sticky: true
popular: true
date: "2021-09-03T19:00:00"
last_modified_at: 2021-09-03T19:00:00
---

## forwarding Refs

- Component를 통해 ref를 자식 중 하나로 자동으로 전달
- 일부 재사용 가능한 Component 라이브러리에 유용할 수 있음

```jsx
// src/components/MyInput.jsx

import React from "react";

export default React.forwardRef(function MyInput(props, ref) {
  return (
    <div>
      <p>MyInput</p>
      <input ref={ref} />
    </div>
  );
});
```

<br>

```js
// src/App.js

import "./App.css";
import { useRef } from "react";
import MyInput from "./components/MyInput";

function App() {
  const myInputRef = useRef();

  const click = () => {
    console.log(myInputRef.current.value);
  };

  return (
    <div>
      <MyInput ref={myInputRef} />
      <button onClick={click}>send</button>
    </div>
  );
}

export default App;
```

<br>

![react-forwardref](https://user-images.githubusercontent.com/62803763/131990779-4df39533-de09-4dae-bdc7-a7f912ef9563.PNG){: .align-center .open-new}
