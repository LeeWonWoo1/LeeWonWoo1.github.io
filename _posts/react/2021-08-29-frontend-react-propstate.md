---
title: "[React] Props, State"
excerpt: React Props와 State
categories:
- React
tags:
- - React
  - Web
  - Node.js
toc: true
toc_sticky: true
popular: true
date: '2021-08-29T04:30:00'
last_modified_at: 2021-08-29T04:30:00
---

## 1. Props와 State

- Props는 Component 외부에서 Component에게 주는 데이터
- State는 Component 내부에서 변경할 수 있는 데이터
- 둘 다 변경이 발생하면, Render가 다시 일어날 수 있음
- Component를 그리는 방법을 기술하는 함수가 Render 함수
- Render 함수는 Props와 State를 바탕으로 Component를 그림
- Props와 State가 변경되면, Component를 다시 그림


<br>

### - Props

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
    // {message: '안녕하세요!!'}
    function Component(props) {
      return (
        <div>
          <h1>{props.message} 이것은 함수로 만든 Component 입니다.</h1>
        </div>
      );
    }

    ReactDOM.render(
      <Component message="안녕하세요!!" />, 
      document.querySelector('#root')
    );
  </script>
</body>
```

<br>

![react-props1](https://user-images.githubusercontent.com/62803763/131228504-9f46ce5d-efc4-44eb-a02e-94c3c7018e19.PNG){: .align-center .open-new}

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
      render() {
        return (
          <div>
            <h1>{this.props.message} 이것은 클래스로 만든 Component 입니다.</h1>
          </div>
        );
      }
    }

    ReactDOM.render(
      <Component message="안녕하세요!!" />, 
      document.querySelector('#root')
    );
  </script>
</body>
```

<br>

![react-props2](https://user-images.githubusercontent.com/62803763/131228550-fb0361cd-7e36-4caa-ab9b-183ffdb6e441.PNG){: .align-center .open-new}


<br>

#### @ defaultProps

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
      render() {
        return (
          <div>
            <h1>{this.props.message} 이것은 클래스로 만든 Component 입니다.</h1>
          </div>
        );
      }
      static defaultProps = {
        message: "기본값1",
      };
    }

    ReactDOM.render(
      <Component />, 
      document.querySelector('#root')
    );
  </script>
</body>
```

<br>

![react-props3](https://user-images.githubusercontent.com/62803763/131228726-a3fd1d8c-baa1-4716-9bce-e95d29f3560d.PNG){: .align-center .open-new}

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
      render() {
        return (
          <div>
            <h1>{this.props.message} 이것은 클래스로 만든 Component 입니다.</h1>
          </div>
        );
      }
    }

    Component.defaultProps = {
      message: "기본값2",
    };

    ReactDOM.render(
      <Component />, 
      document.querySelector('#root')
    );
  </script>
</body>
```

<br>

![react-props4](https://user-images.githubusercontent.com/62803763/131228757-15879a1b-8db9-423e-8a7d-4e6b49347c68.PNG){: .align-center .open-new}

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
    function Component(props) {
      return (
        <div>
          <h1>{props.message} 이것은 함수로 만든 Component 입니다.</h1>
        </div>
      );
    }

    Component.defaultProps = {
      message: "기본값3",
    };

    ReactDOM.render(
      <Component />, 
      document.querySelector('#root')
    );
  </script>
</body>
```

<br>

![react-props5](https://user-images.githubusercontent.com/62803763/131228830-18aaa4ff-e2f7-4241-9ec2-82b757921b70.PNG){: .align-center .open-new}


<br>

### - State

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
      // 그냥 작성
      state = {
        count: 0,
      };

      render() {
        return (
          <div>
            <h1>{this.props.message} 이것은 클래스로 만든 Component 입니다.</h1>
            <p>{this.state.count}</p>
          </div>
        );
      }

      componentDidMount() {
        setTimeout(() => {
          // this.state.count = this.state.count + 1
          this.setState({
            count: this.state.count + 1,
          });
        }, 1000);
      }

      static defaultProps = {
        message: "기본값",
      };
    }

    ReactDOM.render(
      <Component message="안녕하세요!" />, 
      document.querySelector('#root')
    );
  </script>
</body>
```

<br>

![react-state1](https://user-images.githubusercontent.com/62803763/131229107-6e17d9dd-f521-4d91-a6d1-fe7108abe222.PNG){: .align-center .open-new}

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
      // 생성자
      constructor(props) {
        super(props);
        this.state = { count: 0 };
      }

      render() {
        return (
          <div>
            <h1>{this.props.message} 이것은 클래스로 만든 Component 입니다.</h1>
            <p>{this.state.count}</p>
          </div>
        );
      }

      componentDidMount() {
        setTimeout(() => {
          this.setState((previousState) => {
            const newState = { count: previousState.count + 1};
            return newState;
          });
        }, 1000);
      }

      static defaultProps = {
        message: "기본값",
      };
    }

    ReactDOM.render(
      <Component message="안녕하세요!" />, 
      document.querySelector('#root')
    );
  </script>
</body>
```

<br>

![react-state1](https://user-images.githubusercontent.com/62803763/131229107-6e17d9dd-f521-4d91-a6d1-fe7108abe222.PNG){: .align-center .open-new}