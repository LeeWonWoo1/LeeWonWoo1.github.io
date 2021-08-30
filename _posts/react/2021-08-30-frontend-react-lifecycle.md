---
title: "[React] Component Lifecycle"
excerpt: React Component Lifecycle
categories:
- React
tags:
- - React
  - Web
  - Node.js
toc: true
toc_sticky: true
popular: true
date: '2021-08-30T19:00:00'
last_modified_at: 2021-08-30T19:00:00
---

## Component Lifecycle

- React Component는 탄생부터 죽음까지 여러 지점에서 개발자가 작업이 가능하도록 메서드를 오버라이딩 할 수 있게 해줌
- Declarative 성질 : Component의 탄생부터 죽음까지 순간순간을 선언적으로 표현하면, React Component가 선언적으로 표현된 함수들을 실행해서 사용할 수 있게 해주기 때문에, 효과적으로 처리할 수 있음
* Initialization
    - setup props and state
* Mounting
    - componentWillMount
    - render
    - componentDidMount
* Updation
    - props
    - states
* Unmounting
    - componentWillUnmount


<br>

### - Component 생성 및 마운트

- React 16.3 version 이전
* constructor
* componentWillMount
* render (최초 랜더)
* componentDidMount

```html
<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    console.log(React);
    console.log(ReactDOM);

    class App extends React.Component {
      state = {
        age: 29,
      };
      constructor(props) {
        super(props);
        console.log('consturctor', props);
      }
      render() {
        console.log('render')
        return (
          <div>
            <h2>Hello {this.props.name} - {this.state.age}</h2>
          </div>
        );
      }
      componentWillMount() {
        console.log('componentWillMount');
      }
      componentDidMount() {
        console.log('componentDidMount');

        // 타이머 설정
        setInterval(() => {
          this.setState(state => ({ ...state, age: state.age + 1}));
        }, 1000);
      }
    }

    ReactDOM.render(<App name="LWW" />, document.querySelector("#root"));
  </script>
</body>
</html>
```

<br>

![react-lifecycle1](https://user-images.githubusercontent.com/62803763/131327384-4d4a49ea-5fc4-4aa7-8c7a-d10a524d95ff.PNG){: .align-center .open-new}

<br>

### - Component props, state 변경

- React 16.3 version 이전
* componentWillReceiveProps
    - props를 새로 지정했을 때 바로 호출됨
    - state의 변경에 반응하지 않음
    - props의 값에 따라 state를 변경해야 한다면,
        - setState를 이용해 state를 변경
        - 각각 다음 이벤트로 가는것이 아니라 한번에 변경됨
* shouldComponentUpdate
    - props만, state만, props와 state 둘다 변경되어도 실행
    - new Props와 new State를 인자로 해서 호출
    - return type이 boolean
        - true면 render
        - false면 render가 호출되지 않음
        - 이 함수를 구현하지 않으면, default는 true
* componentWillUpdate
    - Component가 재 rendering되기 직전에 호출
    - setState 같은 것을 쓰면 안됨
* render
* componentDidUpdate
    - Component가 재 rendering을 마치면 호출

```html
<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    console.log(React);
    console.log(ReactDOM);

    class App extends React.Component {
      state = {
        age: 29,
      };
      constructor(props) {
        super(props);
        console.log('consturctor', props);
      }
      render() {
        console.log('render')
        return (
          <div>
            <h2>Hello {this.props.name} - {this.state.age}</h2>
          </div>
        );
      }
      componentWillMount() {
        console.log('componentWillMount');
      }
      componentDidMount() {
        console.log('componentDidMount');

        // 타이머 설정
        setInterval(() => {
          this.setState(state => ({ ...state, age: state.age + 1}));
        }, 1000);
      }

      componentWillReceiveProps(nextProps) {
        console.log('componentWillReceivePorps', nextProps);
      }
      shouldComponentUpdate(nextProps, nextState) {
        console.log('shouldComponentUpdate', nextProps, nextState);
        return true;  // 바로 render할 준비
        // return false;  // props나 state가 변경되어도 다시 render하지 않음
      }
      componentWillUpdate(nextProps, nextState) {
        console.log('componentWillUpdate', nextProps, nextState)
      }
      componentDidUpdate(prevProps, prevState) {
        console.log('componentDidUpdate', prevProps, prevState)
      }
    }

    ReactDOM.render(<App name="LWW" />, document.querySelector("#root"));
  </script>
</body>
</html>
```

<br>

- ShouldComponentUpdate가 false일 경우

![react-lifecycle2](https://user-images.githubusercontent.com/62803763/131328537-2e7fa504-4e50-46b6-a8ea-a1849e768a80.PNG){: .align-center .open-new}

<br>

- ShouldComponentUpdate가 true 경우

![react-lifecycle3](https://user-images.githubusercontent.com/62803763/131328594-1fe995fd-0654-491d-b317-4bace7f2dfbe.PNG){: .align-center .open-new}


<br>

### - Component 언마운트

- React 16.3 version 이전
* componentWillUnmount
    - 언마운트되기 직전
    - Component가 사용하고 있던 메모리 중에 정리할 것이 있으면 정리
    - API 응답을 받기 전에 언마운트 된다면 API를 더 이상 받을 준비를 하지 않는 처리 등

```html

<body>
  <div id="root"></div>
  <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    console.log(React);
    console.log(ReactDOM);

    class App extends React.Component {
      state = {
        age: 29,
      };
      // 변수 정의
      interval = null;
      constructor(props) {
        super(props);
        console.log('consturctor', props);
      }
      render() {
        console.log('render')
        return (
          <div>
            <h2>Hello {this.props.name} - {this.state.age}</h2>
          </div>
        );
      }
      componentWillMount() {
        console.log('componentWillMount');
      }
      componentDidMount() {
        console.log('componentDidMount');
        
        // 멤버 변수로 할당
        this.interval = setInterval(() => {
          this.setState(state => ({ ...state, age: state.age + 1}));
        }, 1000);
      }

      componentWillReceiveProps(nextProps) {
        console.log('componentWillReceivePorps', nextProps);
      }
      shouldComponentUpdate(nextProps, nextState) {
        console.log('shouldComponentUpdate', nextProps, nextState);
        return true;
      }
      componentWillUpdate(nextProps, nextState) {
        console.log('componentWillUpdate', nextProps, nextState)
      }
      componentDidUpdate(prevProps, prevState) {
        console.log('componentDidUpdate', prevProps, prevState)
      }
      // Interval 함수 종료
      componentWillUnmount() {
        clearInterval(this.interval);
      }
    }

    ReactDOM.render(<App name="LWW" />, document.querySelector("#root"));
  </script>
</body>
</html>
```