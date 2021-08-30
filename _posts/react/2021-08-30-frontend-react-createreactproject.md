---
title: "[React] Create React Project"
excerpt: Create React App, ESLint, Prettier, husky, lint-staged, debugging
categories:
  - React
tags:
  - - React
    - Web
    - Node.js
toc: true
toc_sticky: true
popular: true
date: "2021-08-30T21:00:00"
last_modified_at: 2021-08-30T21:00:00
---

## 1. Create React App

[CRA 링크](https://create-react-app.dev){:target="\_blank"}
{: .notice--info}

```bash
# terminal

$ npx create-react-app tic-tac-toe
$ cd tic-tac-toe
$ code .
```

<br>

```json
// package.json

{
  "name": "tic-tac-toe",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^5.14.1",  // 테스팅
    "@testing-library/react": "^11.2.7",  // 테스팅
    "@testing-library/user-event": "^12.8.3",  // 테스팅
    "react": "^17.0.2",  // 핵심 모듈
    "react-dom": "^17.0.2",  // 핵심 모듈
    "react-scripts": "4.0.3",  // 개발환경, production 모드에서 build를 위한 배포작업, create-react-app의 프로젝트 관리 역할
    "web-vitals": "^1.1.2"  // 구글에서 사이트 경험을 측정하고 개선할 수 있도록 정보를 얻는 라이브러리
  },
  "scripts": {
    "start": "react-scripts start",  // 개발서버를 로컬에서 띄움
    "build": "react-scripts build",  // production 모드로 build. 컴파일, $ npx serve -s build
    "test": "react-scripts test",  // Jest가 실행되면서 test code 실행
    "eject": "react-scripts eject"  // cra 내에서 해결이 안되는 설정을 추가할 때 사용
  },
  ...
}
```

<br>

## 2. ESLint

- 코딩 스타일을 내부적으로 규정

```json
{
  ...
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ],
    "rules": {  // ESLint 규칙 설정
      "semi": ["error", "always"]
    }
  },
  ...
}
```

<br>

## 3. Prettier

- 코드 포매터
- eslint-config-prettier
  - Prettier에서 불필요하거나 Prettier와 충돌할 수 있는 모든 규칙을 끔
  - 규칙을 끄기만 하기 때문에 다른 설정과 함께 사용

```bash
# terminal

$ npm i prettier -D
```

<br>

```json
{
  ...
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest",
      "prettier"
    ],
  },
  ...
}
```

<br>

![react-create-app1](https://user-images.githubusercontent.com/62803763/131349718-078273af-c0ba-4555-ae98-b1cf2950a68e.PNG){: .align-center .open-new}

<br>

## 4. Husky

- Git으로 어떤 액션이 발생할 때, 처리할 것을 처리해 주는 툴
- ex) Commit 전에 코드 테스트

```bash
# terminal

$ npm i husky -D
$ npx husky install
```

<br>

```json
// package.json
{
  ...
  "scripts": {
    "prepare": "husky install",
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  ...
}
```

<br>

```bash
# terminal

$ npx husky add .husky/pre-commit "~~~"
```

<br>

## 5. Lint-staged

- Run linters on git staged files

```bash
# terminal

$ npm i lint-staged -D
$ npx husky add .husky/pre-commit "lint-staged"
```

<br>

```json
// package.json
{
  ...
  "lint-staged": {
    "**/*.js": [
      "eslint --fix",
      "prettier --write",
      "git add"
    ]
  },
  ...
}
```

<br>

## 6. React Component Debugging

- React Developer Tools

[React Developer Tools 설치](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=ko){:target="\_blank"}
{: .notice--info}

```bash
# terminal

$ npm start
```

<br>

![react-debugging](https://user-images.githubusercontent.com/62803763/131353264-e723da49-735e-437f-bf30-a375075047a0.PNG){: .align-center .open-new}
