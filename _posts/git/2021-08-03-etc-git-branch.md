---
title: "[Git & Github] Branch"
excerpt: 독립적인 Working Directory, Branch
categories:
- Git
tags:
- - Github
  - Git
toc: true
toc_sticky: true
popular: true
date: '2021-08-03T03:00:00'
last_modified_at: 2021-08-03T03:00:00
---

## 1. Branch란?

- 독립적인 Working Directory
- 새로운 작업공간으로 서로 다른 작업과 테스트가 가능


<br>

## 2. Branch Model

- master branch
    - 프로젝트의 기본 branch
    - git init으로 자동 생성
    - 배포용 branch
- develop branch
    - 메인 branch
    - 통합 branch
- feature branch
    - topic branch 역할
    - 버그의 수정과 새로운 기능 개발
    - 원격으로 관리하지 않음
    - 개발이 완료되면, develop branch로 merge
- release branch
    - 버그 수정 작업 후 정상적으로 동작해 배포 가능하면 master branch로 merge
    - 'release-'를 branch 이름 앞에 붙임
- hotfix branch
    - 배포한 버전에 수정이 필요할 경우
    - 'hotfix-'를 branch 이름 앞에 붙임
    - 변경 사항을 develop branch에 merge


<br>

## 3. 명령어

```bash
# 원하는 이름의 branch 생성
$ git branch 이름

# 로컬 저장소 branch list 확인
$ git branch

# 원격 저장소 branch list 확인
$ git branch -r

# 로컬, 원격 저장소 branch list 확인
$ git branch -a

# 생성된 branch로 이동
$ git checkout 이름

# 생성과 동시에 branch로 이동
$ git checkout -b 이름

# 원격 저장소에 있는 branch를 가져와서 해당 branch로 이동
$ git checkout -t 이름

# 로컬 저장소에서 branch 삭제
$ git branch -d 이름
```


<br>

## 4. Branch Working Flow

```bash
$ git branch login
$ git checkout -b login
개발
$ git add .
$ git commit -m 'Add login in new branch'
$ git push origin login
$ git checkout master
$ git pull origin login
$ git push origin master
$ git branch -d login
```