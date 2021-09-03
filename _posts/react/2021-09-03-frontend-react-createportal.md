---
title: "[React] createPortal"
excerpt: Portals
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
toc: true
toc_sticky: true
popular: true
date: "2021-09-03T18:00:00"
last_modified_at: 2021-09-03T18:00:00
---

## createPortal

- 부모의 영향을 받지 않게 부모와 독립된 랜더링

```html
<!-- public/index.html -->

<div id="root"></div>
<div id="modal"></div>
```

<br>

```css
/* src/index.css */

#modal {
  position: absolute;
  top: 0;
  left: 0;
}
```

<br>

```jsx
// src/components/Modal.jsx

import ReactDOM from "react-dom";

const Modal = ({ children }) =>
  ReactDOM.createProtal(children, document.querySelector("#modal"));

export default Modal;
```

<br>

```js
// src/App.js

import "./App.css";
import React from "react";

function App() {
  const [visible, setVisible] = useState(false);
  const open = () => {
    setVisible(true);
  };
  const close = () => {
    setVisible(false);
  };

  return (
    <div>
      <button onClick={open}>open</button>
      {visible && (
        <Modal>
          <div
            style={{
              width: "100vw",
              height: "100vh",
              background: "rgba(0,0,0,.5)",
            }}
            onClick={close}
          >
            Hello
          </div>
        </Modal>
      )}
    </div>
  );
}

export default App;
```

<br>

![react-createportal1](https://user-images.githubusercontent.com/62803763/131989175-dfba9f85-e7da-4869-af48-9c6dd3735682.PNG){: .align-center .open-new}

![react-createportal2](https://user-images.githubusercontent.com/62803763/131989205-2716ccde-9fcd-4b69-bc77-275c9c4bab87.PNG){: .align-center .open-new}
