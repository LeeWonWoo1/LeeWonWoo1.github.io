---
title: "[Typescript] Typescript란?"
excerpt: Typescript 정보, 설치
categories:
- Typescript
tags:
- - Typescript
  - Programming
  - Web
  - NPM
toc: true
toc_sticky: true
popular: true
date: '2021-08-18T19:00:00'
last_modified_at: 2021-08-18T19:00:00
---

## 1. Typescript란?

- Programming Language
- Compiled Language
    - 전통적인 Compiled Language와는 다른 점이 많음
    - Transpile
    - Javascript는 Interpreted Language
- Typescript -> (Typescript Compiler) -> Javascript
- 타입을 명시적으로 지정할 수 있음
- 타입을 지정하지 않으면, Typescript 컴파일러가 자동으로 타입을 추론

Compiled | Interpreted
--|--
컴파일 필요 | 컴파일 필요 X
컴파일러 필요 | 컴파일러 필요 X
컴파일하는 시점 O | 컴파일하는 시점 X
컴파일된 결과물을 실행 | 코드를 실행하는 시점 O = 런타임
컴파일된 결과물을 실행하는 시점 | -


<br>

## 2. Typescript 설치

### - 글로벌 설치

```bash
# 글로벌 설치
$ npm i typescript -g


# 프로젝트 폴더 생성
$ mkdir ts-test


# 프로젝트 폴더로 이동
$ cd ts-test


# 테스트 파일 생성
$ nano test.ts  # console.log('hello')


# 컴파일(test.js 파일 생성)
$ tsc test.ts


# 파일 확인
$ cat test.js
$ cat test.ts


# 설정파일 디폴트 생성
$ tsc --init


# 파일 수정 시 새로 컴파일 
$ tsc -w


# 파일 내용 변경
$ nano test.ts  # console.log('hello typescript')


# 파일 내용 확인
$ cat test.js


# 글로벌 설치 삭제
$ npm uninstall typescript -g


# 프로젝트 폴더 삭제
$ rm -rf ts-test
```

<br>

### - 프로젝트에 설치

```bash
# 프로젝트 폴더 생성
$ mkdir ts-test


# 프로젝트 폴더로 이동
$ cd ts-test


# npm 프로젝트 시작
$ npm init -y


# typescript 설치
$ npm i typescript -D


# typescript 설치 확인
$ cat package.json  # dependencies 항목에서 typescript 설치 확인


# typescript 컴파일러 설치 확인
$ ls node_modules  # typescript


# tsc 실행 방법1
$ node_modules/.bin/tsc


# tsc 실행 방법2
$ node_modules/typescript/bin/tsc


# tsc 실행 방법3
$ npx tsc


# 설정파일 디폴트 생성
$ npx tsc --init


# 테스트 파일 생성
$ nano test.ts


# 컴파일(test.js 파일 생성)
$ npx tsc


# watch 모드 실행
$ npx tsc -w


# script 명시
$ nano package.json  # scripts: {"build": "tsc", "build:watch": "tsc -w"}


# tsc 실행
$ npm run build
$ npm run build:watch
```

<br>

### - VS Code에서 설치

```bash
$ npm init -y
$ npm i typescript -D
```