---
title: "[React] Component Styling - 1"
excerpt: Style Loaders, CSS, SASS, Module
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
    - CSS
    - SCSS
toc: true
toc_sticky: true
popular: true
date: "2021-09-01T20:00:00"
last_modified_at: 2021-09-01T20:00:00
---

## 1. Style Loaders

```js
// webpack.config.js

// CSS
// import './App.css';
{
  test: cssRegex,
  exclude: cssModuleRegex,
  use: getStyleLoaders({
    importLoaders: 1,
    sourceMap: isEnvProduction && shouldUseSourceMap,
  }),
  sideEffects: true,
},

// -----------------------------------------------------
// CSS Module
// import styles from './App.module.css';

{
  test: cssModuleRegex,
  use: getStyleLoaders({
    importLoaders: 1,
    sourceMap: isEnvProduction && shouldUseSourceMap,
    modules: true,
    getLocalIdent: getCSSModuleLocalIdent,
  }),
},

// -----------------------------------------------------
// SASS
// import './App.scss';
// import './App.sass';

{
  test:sassRegex,
  exclude: sassModuleRegex,
  use: getStyleLoaders(
    {
      importLoaders: 2,
      sourceMap: isEnvProduction && shouldUseSourceMap,
    },
    'sass-loader'
  ),
  sideEffects: true,
},

// -----------------------------------------------------
// SASS Module
// import styles from './App.module.scss';
// import styles from './App.module.sass';

{
  test: sassModuleRegex,
  use: getStyleLoaders(
    {
      importLoaders: 2,
      sourceMap: isEnvProduction && shouldUseSourceMap,
      modules: true,
      getLocalIdent: getCSSModuleLocalIdent,
    },
    'sass-loader'
  ),
},
```

<br>

## 2. CSS to SCSS

```js
// src/App.js

import logo from "./logo.svg";
import "./App.scss";

function App() {
  return (
    <div className="App">
      <header className="header">
        <img src={logo} className="logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}
```

<br>

```bash
# terminal

$ npm i sass
```

<br>

```scss
// src/App.scss

.App {
  text-align: center;

  .logo {
    height: 40vmin;
    pointer-events: none;
  }

  @media ... ...;
}
```

<br>

## 3. CSS Module, SASS Module

- 두 모듈의 사용법은 같음

```js
// src/App.js

import logo from "./logo.svg";
import styles from "./App.module.css";
import Button from "./components/Button";

console.log(styles);

function App() {
  return (
    <div className={styles["App"]}>
      <header className={styles["header"]}>
        <img src={logo} className={styles["logo"]} alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <Button>Button</Button>
      </header>
    </div>
  );
}
```

<br>

```bash
# terminal

$ npm i classnames
```

<br>

```jsx
// src/components/Button.jsx

import styles from "./Button.module.css";
import classNames from "classnames/bind";

const cx = classNames.bind(styles)

class Button extends React.Component {
  state = {
    loading: false
  }

  render() {
    console.log(classNames('foo', 'bar'));  // foo bar
    console.log(classNames({ foo: true }, { bar: false }));  // foo
    console.log(classNames(null, false, 'bar', undefined, 0, 1, {baz: null}, ""));  // bar 1

    const {loading} = this.state;
    return (
      <button
        onClick={this.startLoading}
        className={classNames(cx("button", { loading })}
        {...this.props}
      />
    );
  }

  startLoading = () => {
    this.setState({
      loading: true,
    });
    setTimeout(() => {
      this.setState({
        loading: false,
      });
    }, 1000);
  };
}

export default Button;
```

<br>

```css
/* src/components/Button.module.css */

.button {
  background: transparent;
  border-radius: 3px;
  border: 2px solid palevioletred;
  color: palevioletred;
  margin: 0 1em;
  padding: 0.25em 1em;
  font-size: 20px;
}
. loading {
  border: 2px solid grey;
  color: grey;
}
```

<br>

![react-styling1](https://user-images.githubusercontent.com/62803763/131664437-4bf3e235-2f08-49c3-a389-159ead7621d3.PNG){: .align-center .open-new}

![react-styling2](https://user-images.githubusercontent.com/62803763/131669789-9bababea-5e5f-4303-9a43-70df10d074ef.PNG){: .align-center .open-new}
