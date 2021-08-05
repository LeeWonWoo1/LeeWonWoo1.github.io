---
title: "[Node.js] NVM, Node.js, NPM"
excerpt: NVM -> Node.js -> NPM
categories:
- Javascript
tags:
- - Javascript
  - Node.js
  - NVM
  - NPM
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-05T20:00:00'
last_modified_at: 2021-08-05T20:00:00
---

## 1. Node.js

- Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임
- JavaScript가 동작할 수 있는 컴퓨터 환경


### - Node.js 사용 이유

1. 웹 페이지에서는 html, css, js만 동작
2. 순수하게 html, css, js만 가지고 개발하면 그 과정이 비효율적
3. 따라서 개발을 도와주는 모듈의 도움을 받아야 함
4. 모듈들은 브라우저에서 직접적으로 동작할 수 없음
5. 따라서 모듈의 도움을 받은 내용들을 html, css, js로 변환해야 함
6. 변환을 위해 컴퓨터에게 변환작업에 대한 명령을 내려주어야 함
7. Node.js가 명령이 돌아가는 환경을 제공
8. Node.js 환경에서 js 프로그래밍 언어로 변환을 만들어 줄 수 있음
9. 변환된 결과는 html, cs, js로 결과를 만들어 브라우저로 동작시킴


<br>

## 2. 단일 버전의 Node.js 설치 방법

아래의 링크를 통해 설치할 수 있음

[https://nodejs.org/ko/]({{"https://nodejs.org/ko/"}}){:target="_blank"} 
{: .notice--info}

- LTS(짝수 Version)
    - 장기적으로 안정되고 신뢰도가 높은 지원이 보장
    - 유지/보수와 보안(서버 운영 등)에 초점을 맞춤
    - 대부분의 사용자에게 추천되는 버전
- 현재 버전(홀수 Version)
    - 가장 최신의 버전
- 다른 Node.js 버전에서도 개발을 진행해야 할 수 있음
- 단일 버전의 Node.js 설치보다 **_NVM 우선 설치 권장!_**


<br>

## 3. NVM 설치

구글에 nvm-window를 검색하고 해당 Github 페이지에 접속한 뒤 nvm-setup.zip 파일을 설치

<br>

혹은 아래의 링크를 통해 설치

[https://github.com/coreybutler/nvm-windows]({{"https://github.com/coreybutler/nvm-windows"}}){:target="_blank"} 
{: .notice--info}


<br>

## 4. 원하는 버전의 Node.js 설치

**VS Code 환경**
{: .notice--warning}

```bash
# nvm을 통해 설치되어 있는 node.js 버전 리스트
$ nvm ls

# 설치하고자 하는 node.js 버전
$ nvm install 14.17.3
$ nvm install 12.22.3

# 사용하고자 하는 node.js 버전
$ nvm use 14.17.3

# 현재 사용되고 있는 node.js 버전
$ node --version

# 삭제하고자 하는 node.js 버전
$ nvm uninstall 12.22.3

# nvm 명령어 모음, 설명
$ nvm --help
```


<br>

## 5. NPM 설치

- NPM은 전 세계의 개발자들이 만든 다양한 패키지와 모듈들을 관리
- 최신의 웹 프론트앤드 개발에서는 기능들을 프로젝트에 직접적으로 설치해서 별도의 가공처리를 거치고, 가공된 결과물을 웹 사이트로 동작시킴
- Node.js를 설치하면 NPM이 자동으로 설치됨

```bash
$ npm --version
```


<br>

## 6. NPM을 통한 Package 설치

```bash
# package.json 파일 생성
$ npm init -y

# parcel-bundler 패키지 설치(-D : 개발 의존성 패키지 설치)
$ npm install -D parcel-bundler
# or
$ npm install parcel-bundler -D

# lodash 패키지 설치(일반 의존성 설치)
$ npm install lodash

# lodash 패키지 정보 확인
$ npm info lodash

# lodash 원하는 버전으로 설치
$ npm install lodash@4.17.20

# lodash 패키지 업데이트
$ npm update lodash

# 패키지를 삭제하더라도 내역에 있는 패키지 설치 가능
$ npm install
# or
$ npm i
```


<br>

### - package.json

- name : 프로젝트 이름
- version : 프로젝트 버전
- description : 프로젝트 설명
- main : npm 생태계에 업로드 할 때 필요한 옵션
- scripts : 프로젝트 내부에서 사용할 수 있는 script 명령들을 명시
- keywords : 프로젝트와 관련된 키워드
- author : 프로젝트 소유주
- license : 프로젝트 라이선스

