---
title: "[Redux] 개요, Action, Reducers"
excerpt: Redux Basic - 1
categories:
  - Redux
tags:
  - - Redux
    - Web
    - Node.js
    - Jest
toc: true
toc_sticky: true
popular: true
date: "2021-09-05T02:00:00"
last_modified_at: 2021-09-05T02:00:00
---

## 1. Redux 개요

- Context에 주어지는 전역 데이터를 효과적으로 관리하기 위한 라이브러리
- 단일 스토어
- (만들기) 단일 스토어 사용 준비하기
  - import redux
  - 액션을 정의
  - 액션을 사용하는 리듀서를 만듦
  - 리듀서들을 합침
  - 최종 합쳐진 리듀서를 인자로, 단일 스토어를 만듦
- (사용하기) 준비한 스토어를 React Component에서 사용하기
  - import react-redux
  - connect 함수를 이용해 컴포넌트에 연결

[Component - Communication](https://cloud.protopie.io/p/irg8jMXuGov?ui=false&mockup=false&scaleToFit=true){:target="\_blank"}

[Component - Communication - Redux](https://cloud.protopie.io/p/Ycc3KrJvjgA?ui=false&mockup=false&scaleToFit=true){:target="\_blank"}

<br>

![redux-start1](https://user-images.githubusercontent.com/62803763/132103458-9154ad7f-1e27-4d11-bbc2-4324ac2b6e92.png){: .align-center .open-new}

<br>

- 프로젝트 시작

```bash
# terminal

$ npx create-react-app redux-start
$ cd redux-start
$ npm i redux
$ code .
```

<br>

## 2. Action

- Action은 사실 그냥 객체
- 두 가지 형태의 Action이 있음
  - { type: 'TEST' } -> payload 없는 액션
  - { type: 'TEST', params: 'hello' } -> payload 있는 액션
- type만이 필수 프로퍼티이며, type은 문자열
- 스토어의 상태를 변경하는 용도로 사용됨

<br>

### - Redux의 Action 생성자란?

- 액션을 생성하는 함수를 액션 생성자라고 함
- 함수를 통해 액션을 생성해서, 액션 객체를 리턴
- createTest('hello'); -> {type: 'TEST', params: 'hello'} 리턴

```js
function 액션생성자(...args) {
  return 액션;
}
```

<br>

### - Redux의 Action이 하는 일

- 액션 생성자를 통해 액션을 만들어 냄
- 만들어낸 액션 객체를 Redux 스토어에 보냄
- Redux 스토어가 액션 객체를 받으면 스토어의 상태 값이 변경 됨
- 변경된 상태 값에 의해 상태를 이용하고 있는 Component가 변경됨
- 액션은 스토어에 보내는 일종의 input

<br>

### - Action 준비

- 액션의 타입을 정의하여 변수로 빼는 단계
  - 강제는 아님
  - 그냥 타입을 문자열로 넣기에는 실수를 유발할 가능성이 큼
  - 미리 정의한 변수를 사용하면, 스펠링에 주의를 덜 기울여도 됨
- 액션 객체를 만들어 내는 함수를 만드는 단계
  - 하나의 액션 객체를 만들기 위해 하나의 함수를 만들어 냄
  - 액션의 타입은 미리 정의한 타입 변수로부터 가져와서 사용

```js
// src/redux/actions.js
// 액션의 타입을 정의하고 액션 생성자 하나 만들기

export const ADD_TODO = "ADD_TODO";

function addTodo(todo) {
  return {
    type: ADD_TODO,
    todo,
  };
}
```

<br>

## 3. Reducers

- 액션을 주면, 그 액션이 적용되어 달라진 결과를 만들어 줌
- 함수
  - Pure Function
  - Immutable : 리듀서를 통해 state가 달라졌음을 Redux가 인지하는 방식
    식
- 액션을 받아서 state를 리턴하는 구조
- 인자로 들어오는 previousState와 리턴되는 newState는 다른 참조를 가지도록 해야함

```js
function 리듀서(previousState, action) {
  return newState;
}
```

<br>

```js
// src/redux/reducers.js

import { ADD_TODO } from "./actions";

const initialState = [];

function todoApp(previousState = initialState, action) {
  // 초기값을 설정해주는 부분
  // if (previousState === undefined) {
  //   return [];
  // }

  if (action.type === ADD_TODO) {
    return [...previousState, action.todo];
  }

  return previousState;
}
```
