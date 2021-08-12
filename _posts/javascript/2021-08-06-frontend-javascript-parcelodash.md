---
title: "[Node.js] Parcel-Bundler, lodash"
excerpt: Parcel-Bundler와 lodash
categories:
- Javascript
tags:
- - Javascript
  - Node.js
  - NPM
  - Parcel
  - Lodash
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-06T18:00:00'
last_modified_at: 2021-08-06T18:00:00
---

## 1. Parcel-Bundler

- open with live server는 원시적인 방법으로 동작
- 최신의 웹 frontend 개발에서는 잘 쓰이지 않음
- dependencies : 사용하는 여러가지 패키지들이 명시
- devDependencies : 우리가 설치한 패키지들이 명시
- 개발, 관리, 제품화 목적


### - parcel 명령어 등록

- 터미널에서 parcel 명령어가 동작하지 않음
- package.json 파일의 scripts 부분에서 "dev": "parcel index.html" 작성
- 터미널에서 parcel이라는 명령어가 현재 프로젝트에서만 동작할 수 있음
- 로컬 환경에서 개발용으로 서버를 열기 위함

```bash
$ parcel index.html
```


<br>

### - 개발서버 열기

```bash
$ npm run dev
```

- npm 명령어를 통해 scripts 부분을 실행
- dev는 development의 약어로, 로컬 환경에서 개발서버를 열겠다는 뜻


### - build 명령어 등록

- package.json 파일의 scripts 부분에서 "build": "parcel build index.html" 작성
- 실제로 사용자들이 보는 용도의 결과물이 출력


### - 빌드서버 열기

```bash
$ npm run build
```

- 프로젝트 구조에서 dist 폴더 생성
- 들여쓰기 같은 띄어쓰기도 다 용량이기 때문에, 전부 제거해서 압축된 형식으로 만들어 줌
- 코드 난독화
    - 작성된 코드를 읽기 어렵게 만드는 작업
    - 빌드된 결과(제품)는 브라우저에서 해석되는 용도로, 용량을 축소하기 읽기 어렵게 만드는 등의 최적화를 거치는 것이 좋음
- Bundle : 프로젝트 개발에 사용한 여러 모듈(패키지)을 하나로 묶어내는 작업


<br>

## 2. lodash


### - lodash 패키기 가져오기

```javascript
import _ from 'lodash'
```

- lodash를 node_modules 디렉토리에서 import
- 즉 lodash라는 패키지의 package.json 파일에 main 옵션에 명시되어있는 lodash.js 파일을 실제로 가져와서 프로젝트의 js 파일에서 활용됨
- "_" 라는 변수에 할당해서 사용


### - lodash 메서드

```javascript
import _ from 'lodash'

// _.camelCase() -> 문자열을 CamelCase 방식으로 출력
console.log(_.camelCase('hello world'));  // helloWorld


// _.uniqBy(배열, 속성) -> 합쳐진 배열의 중복값을 제거한 배열 반환
const usersA = {
  { userId: '1', name: 'LWW' },
  { userId: '2', name: 'Kim' }
}

const userB = {
  { userId: '1', name: 'LWW'},
  { userId: '3', name: 'Park'},
}

// .concat()은 중복 발생!
const usersC = usersA.concat(usersB)
console.log('concat', usersC) // concat
                              // 0: {userId: "1", name: "LWW"}
                              // 1: {userId: "2", name: "Kim"}
                              // 2: {userId: "1", name: "LWW"}
                              // 3: {userId: "3", name: "Park"}
console.log('uniqBy', _.uniqBy(usersC, 'userId')) // uniqBy
                                                  // 0: {userId: "1", name: "LWW"}
                                                  // 1: {userId: "2", name: "Kim"}
                                                  // 2: {userId: "3", name: "Park"}


// _.unionBy(배열1, 배열2, 속성) -> 합치기 전 배열을 합쳐 중복값을 제거한 배열 반환
const usersD = _.unionBy(usersA, usersB, 'userId')
console.log('unionBy', usersD)  // unionBy
                                // 0: {userId: "1", name: "LWW"}
                                // 1: {userId: "2", name: "Kim"}
                                // 2: {userId: "3", name: "Park"}


// _.find() -> 해당 객체를 찾음
const users = {
  { userId: '1', name: 'LWW' },
  { userId: '2', name: 'Kim' },
  { userId: '3', name: 'Park' },
  { userId: '4', name: 'Choi' },
  { userId: '5', name: 'Jang' }
}

const foundUser = _.find(users, { name: 'Park' })
console.log(foundUser)  // {userId: "3", name: "Park"}


// _.findIndex() -> 해당 객체의 index 번호 반환
const foundUserIndex = _.findIndex(users, { name: 'Park' })
console.log(foundUserIndex)  // 2


// _.remove() -> 해당 객체를 삭제
_.remove(users, { name: 'LWW' })
console.log(users)  // 0: { userId: "2", name: "Kim" }
                    // 1: { userId: "3", name: "Park" }
                    // 2: { userId: "4", name: "Choi" }
                    // 3: { userId: "5", name: "Jang" }
```