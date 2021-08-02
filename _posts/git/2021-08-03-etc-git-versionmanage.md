---
title: "[Git & Github] 버전 관리"
excerpt: Git과 Github을 사용한 프로젝트 버전 관리 방법
categories:
- Git
tags:
- - Github
  - Git
toc: true
toc_sticky: true
popular: true
date: '2021-08-03T02:00:00'
last_modified_at: 2021-08-03T02:00:00
---

## 1. Git이란?

- 컴퓨터 파일의 변경사항을 추적
- 여러 사용자들 간에 해당 파일 작업을 조율
- 대표적인 버전 관리 시스템(VCS)


<br>

## 2. Git 사용 준비

```bash
# 개행 문자(Newline) 설정
# macOS, Linux
$ git config --global core.autocrlf input
# Windows
$ git config --global core.autocrlf true

# 사용자 정보
# commit(버전 생성)을 위한 정보 등록
$ git config --global user.name 'Github 계정 이름'
$ git config --global user.email 'Github 이메일'

# 구성 확인
# Q키를 눌러서 종료
$ git config --global --list
```


<br>

## 3. Git 명령어

```bash
# 현재 프로젝트에서 변경사항 추적(버전관리) 시작
$ git init

# 원격 저장소를 로컬 저장소로 복사
$ git clone 원격 저장소 url

# 변경사항을 추적할 특정 파일을 지정
$ git add 파일 이름

# 모든 파일의 변경사항을 추적하도록 지정
$ git add .

# 버전관리 상태 확인
$ git status

# 메시지(-m)와 함께 버전을 생성
$ git commit -m '메시지'

# commit list 확인
$ git log

# 한 버전 뒤로 되돌리기
$ git reset --hard HEAD~1

# N 버전 뒤로 되돌리기
$ git reset --hard HEAD~N

# 되돌린 버전 원상복귀
$ git reset --hard ORIG_HEAD

# origin이라는 별칭으로 원격 저장소를 연결
$ git remote add origin 원격 저장소 url

# origin이란 별칭의 원격 저장소로 버전 내역 전송
$ git push origin master

# 원격 저장소의 master 브랜치 내역 당겨오기
$ git pull origin master

# 병합 없이 원격 저장소의 최신 내용으로 업데이트
$ git fetch

# 파일이 삭제 됐거나 원격 서버에 반영하지 않음
$ git rm 삭제할 파일

# Stage Area에서만 제거하고 Working Directory 상태는 유지
$ git rm --cached

# 아직 add 되지 않은 Working Directory 파일을 스택에 임시 저장
$ git stash

# git stash 목록 확인
$ git stash list

# 가장 최근의 stash 적용
$ git stash apply
```