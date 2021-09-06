---
title: "[Oracle] CREATE TABLE, Constraint"
excerpt: 테이블 생성, 테이블 제약조건
categories:
  - DB
tags:
  - - DB
    - Oracle
    - CS
toc: true
toc_sticky: true
popular: true
date: "2021-09-07T04:00:00"
last_modified_at: 2021-09-07T04:00:00
---

[DB 무료 연습 사이트](http://www.sqlfiddle.com/){:target="\_blank"}
{: .notice--info}

## 1. CREATE TABLE

- 테이블 생성

```oracle
CREATE TABLE 테이블명 (
  COLUMN명 데이터타입(크기) 제약조건,
  COLUMN명 데이터타입(크기) 제약조건
)
```

<br>

```oracle
CREATE TABLE PERSON_TABLE (
  NAME VARCHAR2(8),
  GENDER CHAR(2),
  AGE NUMBER(5),
  PHONE CHAR(13)
)
```

<br>

- 자주 쓰는 데이터 타입
  - CHAR : 주로 고정 크기일 때 사용
  - VARCHAR2 : 주로 가벼 크기일 때 사용
  - NUMBER : 숫자
  - DATE : 날짜
