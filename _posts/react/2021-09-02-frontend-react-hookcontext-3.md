---
title: "[React] Hooks & Context - 3"
excerpt: Component 간 통신, Context API
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
toc: true
toc_sticky: true
popular: true
date: "2021-09-02T02:00:00"
last_modified_at: 2021-09-02T02:00:00
---

## 1. Component간 통신

### - 하위 Component를 변경하기

```jsx
// src/components/A.jsx

export default function A() {
  const [value, setValue] = useState("아직 안바뀜");
  return (
    <div>
      <B value={value} />
      <button onClick={click}>E의 값 바꾸기</button>
    </div>
  );

  function click() {
    setValue("E의 값 변경");
  }
}

function B({ value }) {
  return (
    <div>
      <p>여긴 B</p>
      <C value={value} />
    </div>
  );
}

function C({ value }) {
  return (
    <div>
      <p>여긴 C</p>
      <D value={value} />
    </div>
  );
}

function D({ value }) {
  return (
    <div>
      <p>여긴 D</p>
      <E value={value} />
    </div>
  );
}

function E({ value }) {
  return (
    <div>
      <p>여긴 E</p>
      <h3>{value}</h3>
    </div>
  );
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="logo" alt="logo" />
        <A />
      </header>
    </div>
  );
}

export default App;
```

<br>

![react-context1](https://user-images.githubusercontent.com/62803763/131714420-13503712-afc8-4153-8529-cc4a1aa91caf.PNG){: .align-center .open-new}

<br>

### - 상위 Component를 변경하기

```jsx
// src/components/A.jsx

export default function A() {
  const [value, setValue] = useState("아직 안바뀜");
  return (
    <div>
      <p>{value}</p>
      <B setValue={setValue} />
    </div>
  );
}

function B({setValue}) {
  return (
    <div>
      <p>여긴 B</p>
      <C setValue={setValue} />
    </div>
  );
}

function C({setValue}) {
  return (
    <div>
      <p>여긴 C</p>
      <D setValue={setValue} />
    </div>
  );
}

function D({setValue}) {
  return (
    <div>
      <p>여긴 D</p>
      <E setValue={setValue}/>
    </div>
  );
}

function E({setValue}) {
  return (
    <div>
      <p>여긴 E</p>
      <button onClick={click}>클릭</buttin>
    </div>
  );

  function click() {
    setValue('A의 값을 변경');
  }
}
```

<br>

![react-context2](https://user-images.githubusercontent.com/62803763/131715604-4cb86632-99da-4a53-b383-37844265d22c.PNG){: .align-center .open-new}

<br>

## 2. Context API

### 하위 Component 전체에 데이터를 공유하는 법

- 데이터를 Set 하는 것
  - 가장 상위 Component => 프로바이더
- 데이터를 Get 하는 것
  - 모든 하위 Component에서 접근 가능
    - 컨슈머로 하는 방법
    - Class Component의 this.context로 하는 방법
    - Functional Component의 useContext로 하는 방법

<br>

#### @1. 데이터를 Set 하기

1. 일단 컨텍스트를 생성
2. 컨텍스트.프로바이더를 사용
3. value를 사용

```js
// src/contexts/PersonContext.js

import React from "react";

const PersonContext = React.createContext();

export default PersonContext;
```

<br>

```js
// src/index.js

const persons = [
  {id: 0, name: 'Mark', age: 39},
  {id: 1, name: 'Hanna', age: 28}
]

ReactDOM.render(
  <React.StrictMode>
    <PersonContext.Provider value={persons}>
      <App />
    </PersonContext.Provider>
  </React.StrictMode>
  document.getElementById("root")
);
```

<br>

#### @2. 데이터를 Get 하기 - Consumer

1. 컨텍스트를 가져옴
2. 컨텍스트.컨슈머를 사용
3. value를 사용

```jsx
// src/components/Example1.jsx

import PersonContext from "../contexts/PersonContext";

export default function Example1() {
  return (
    <PersonContext.Consumer>
      {(persons) => (
        <ul>
          {persons.map((person) => (
            <li>{person.name}</li>
          ))}
        </ul>
      )}
    </PersonContext.Consumer>;
  );
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example1 from "./components/Example1";

function App({ hasMounted }) {
  const width = useWindowWidth();
  const hasMountedFromHooks = useHasMounted();

  console.log(hasMounted, hasMountedFromHooks);

  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <Example1 />
      </header>
    </div>
  );
}

export default App;
```

<br>

![react-context3](https://user-images.githubusercontent.com/62803763/131717723-2b596edf-ed0d-415b-8339-8e2e16503e2e.PNG){: .align-center .open-new}

<br>

#### @3. 데이터를 Get 하기 - class

1. static contextType에 컨텍스트를 설정
2. this.context => value

```jsx
// src/components/Example2.jsx

import React from "react";
import PersonContext from "../contexts/PersonContext";

export default class Example2 extends React.Component {
  static contextType = PersonContext;

  render() {
    const persons = this.context;
    return (
      <ul>
        {persons.map((person) => (
          <li>{person.name}</li>
        ))}
      </ul>
    );
  }
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example1 from "./components/Example1";
import Example2 from "./components/Example2";

function App({ hasMounted }) {
  const width = useWindowWidth();
  const hasMountedFromHooks = useHasMounted();

  console.log(hasMounted, hasMountedFromHooks);

  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <Example1 />
        <Example2 />
      </header>
    </div>
  );
}

export default App;
```

<br>

![react-context4](https://user-images.githubusercontent.com/62803763/131718461-7ccd3b7c-aef1-44ff-8921-171f61f7f93a.PNG){: .align-center .open-new}

<br>

#### @4. 데이터를 Get 하기 - functional

1. useContext로 컨텍스트를 인자로 호출
2. useContext의 return이 value

```jsx
// src/components/Example3.jsx

import PersonContext from "../contexts/PersonContext";

export default function Example1() {
  const persons = useContext(PersonContext);

  return (
    <ul>
      {persons.map((person) => (
        <li>{person.name}</li>
      ))}
    </ul>
  );
}
```

<br>

```js
// src/App.js

import logo from "./logo.svg";
import "./App.css";
import Example1 from "./components/Example1";
import Example2 from "./components/Example2";
import Example3 from "./components/Example3";

function App({ hasMounted }) {
  const width = useWindowWidth();
  const hasMountedFromHooks = useHasMounted();

  console.log(hasMounted, hasMountedFromHooks);

  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <Example1 />
        <Example2 />
        <Example3 />
      </header>
    </div>
  );
}

export default App;
```

<br>

![react-context5](https://user-images.githubusercontent.com/62803763/131719160-47f27750-121a-40fc-8e85-3f568ffbac64.PNG){: .align-center .open-new}
