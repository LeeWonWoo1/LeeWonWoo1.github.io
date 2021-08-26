---
title: "[Bundler] NPX, Degit"
excerpt: Parcel, Webpack 템플릿을 쉽게 다운로드 하는법
categories:
- Bundler
tags:
- - Bundler
  - Web
  - Git
  - Github
toc: true
toc_sticky: true
popular: true
date: '2021-08-27T04:00:00'
last_modified_at: 2021-08-27T04:00:00
---

## NPX, Degit

- npx는 Node.js에서 쓸 수 있는 명령으로, degit을 설치하지 않고 동작시킬 수 있음
- degit은 Github에 있는 원격 저장소를 현재 경로에 다운로드
- 버전관리가 되어있지 않은 상태이기 때문에 처음부터 다시 버전관리가 가능
    - npx degit : 버전관리가 없는 새로운 프로젝트 다운로드
    - git clone : 해당하는 저장소가 가지고 있는 버전의 내역까지 가지고 옴

```bash
# terminal

# $ npx degit Github계정이름/저장소이름 폴더이름
$ npx degit LeeWonWoo1/webpack-template-basic webpack-template-test

$ cd webpack-template-test
$ code . -r
```