---
title: "[React] Event Handling"
excerpt: React Event Handling
categories:
- React
tags:
- - React
  - Web
  - Node.js
toc: true
toc_sticky: true
popular: true
date: '2021-08-29T05:00:00'
last_modified_at: 2021-08-29T05:00:00
---

## Event Handling

- HTML DOM에 클릭하면 이벤트가 발생하고, 그에 맞는 변경이 일어나도록 해야함
- JSX에 이벤트를 설정할 수 있음
- camelCase로만 사용할 수 있음
    - onClick, onMouseEnter
- 이벤트에 연결된 JavaScript 코드는 함수
    - 이벤트 = {함수}와 같이 씀
- 실제 DOM 요소들에만 사용 가능
    - React Component에 사용하면, 그냥 props로 전달

```js
class Comp extends React.Component {
  render() {
    return (
      <div>
        <button onClick={() => {
          console.log('cilcked');
        }}>클릭</button>
      </div>
    );
  }
}
```

<br>

```html
<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    console.log(React);
    console.log(ReactDOM);

    // Function Component
    function Component() {
      return (
        <div>
          <button 
            onClick={() => { 
              console.log('clicked');
             }}
          >
            클릭
          </button>
        </div>
      );
    }

    ReactDOM.render(<Component />, document.querySelector('#root'))
  </script>
</body>
```

<br>

![react-eventhandling1](https://user-images.githubusercontent.com/62803763/131229671-0dff6d58-9b05-4704-b55f-5a98243aeacb.PNG){: .align-center .open-new}

<br>

```html
<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    console.log(React);
    console.log(ReactDOM);

    // Class Component
    class Component extends React.Component {
      state = {
        count: 0,
      };
      render() {
        return (
          <div>
            <p>{this.state.count}</p>
            <button 
              onClick={() => { 
                console.log('clicked');
                this.setState((state) => ({
                  ...state,
                  count: state.count + 1,
                }));
              }}
            >
              클릭
            </button>
          </div>
        );
      }
    }

    ReactDOM.render(<Component />, document.querySelector('#root'))
  </script>
</body>
```

<br>

![react-eventhandling2](https://user-images.githubusercontent.com/62803763/131229715-6cd9c2d1-5fc3-48b9-9c39-2f20d6e159a0.PNG){: .align-center .open-new}

<br>

- 메서드 분리

```html
<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    console.log(React);
    console.log(ReactDOM);

    // Class Component
    class Component extends React.Component {
      state = {
        count: 0,
      };
      // bind 방법 1
      constructor(props) {
        super(props);
        this.click = this.click.bind(this);
      }
      render() {
        return (
          <div>
            <p>{this.state.count}</p>
            <button onClick={this.click}>클릭</button>
          </div>
        );
      }
      click() {
        console.log('clicked');
        this.setState((state) => ({
          ...state,
          count: state.count + 1,
        }));
      }
    }

    ReactDOM.render(<Component />, document.querySelector('#root'))
  </script>
</body>
```

<br>

```html
<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    console.log(React);
    console.log(ReactDOM);

    // Class Component
    class Component extends React.Component {
      state = {
        count: 0,
      };
      render() {
        return (
          <div>
            <p>{this.state.count}</p>
            <button onClick={this.click}>클릭</button>
          </div>
        );
      }
      click = () => {  // bind 방법 2
        console.log('clicked');
        this.setState((state) => ({
          ...state,
          count: state.count + 1,
        }));
      }
    }

    ReactDOM.render(<Component />, document.querySelector('#root'))
  </script>
</body>
```

<br>

![react-eventhandling2](https://user-images.githubusercontent.com/62803763/131229715-6cd9c2d1-5fc3-48b9-9c39-2f20d6e159a0.PNG){: .align-center .open-new}