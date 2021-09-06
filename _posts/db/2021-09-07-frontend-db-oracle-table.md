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

```java
CREATE TABLE 테이블명 (
  COLUMN명 데이터타입(크기) 제약조건,
  COLUMN명 데이터타입(크기) 제약조건
)
```

<br>

```java
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

![oracle-createtable](https://user-images.githubusercontent.com/62803763/132257572-e496a36b-620c-4fb4-b745-063a5f09752d.PNG){: .align-center .open-new}

<br>

## 2. Constraint

- 자신이 얻고자 하는 값만 받을 수 있도록 설정하는 것

<br>

### - NOT NULL

- 해당 컬럼 안에 NULL 값이 들어올 수 없음

![oracle-constraint1](https://user-images.githubusercontent.com/62803763/132259391-35cc01cf-eb76-40f3-85db-46f7d35f31fa.PNG){: .align-center .open-new}

> 에러 발생!

<br>

### - PRIMARY KEY

- 기본키
- 테이블의 각 행들을 식별하는 기능
- NULL과 중복 값을 허용하지 않음

![oracle-constraint2](https://user-images.githubusercontent.com/62803763/132258193-0abaeb40-8c36-49fa-a934-c4f5acae888b.PNG){: .align-center .open-new}

> ERROR!

<br>

### - FOREIGN KEY

- 외래키
- 다른 테이블의 키를 가져와 해당 테이블의 행을 식별
- NULL과 중복 값 허용

```java
CREATE TABLE PK_TABLE (
  key varchar2(10),
  // CONSTRAINT / 명칭 / PRIMARY KEY / 해당 테이블 KEY COLUMN 명
  CONSTRAINT PK_COLUMN PRIMARY KEY (key)
 );  // 다른 테이블에서 FK로 가져다 쓸 수 있음

CREATE TABLE FK_TABLE (
  val varchar2(10),
  key varchar2(10),
  CONSTRAINT FK_COLUMN
    FOREIGN KEY (key)  // FK_TABLE의 key를 FOREIGN KEY로 사용
    REFERENCES PK_TABLE(key)  // PK_TAbLE의 PRIMARY KEY인 key를 가져옴
);

INSERT INTO PK_TABLE(key) VALUES('PK_VAL');  // PRIMARY KEY를 'PK_VAL'로 삽입하면
INSERT INTO FK_TABLE(val,key) VALUES('TEST_VAL','PK_VAL');
INSERT INTO FK_TABLE(val) VALUES('TEST_VAL');  // FK는 'PK_VAL'만 사용 가능

SELECT * FROM FK_TABLE
```

![oracle-constraint3](https://user-images.githubusercontent.com/62803763/132258858-a96ca58e-2cca-4016-b820-b84745ec7af1.PNG){: .align-center .open-new}

<br>

### - UNIQUE

- NULL은 허용, 중복 값은 허용하지 않음

![oracle-constraint4](https://user-images.githubusercontent.com/62803763/132259064-d9442ebe-a12f-43c7-a74d-c22b948c2933.PNG){: .align-center .open-new}

<br>

### - CHECK

- 특정 값만 입력할 수 있도록 범위를 설정하는 것

![oracle-constraint5](https://user-images.githubusercontent.com/62803763/132259230-89774dbd-97fa-43f7-b41c-601bd1fb4926.PNG){: .align-center .open-new}

> 29 > 19 이므로 OK

<br>

![oracle-constraint6](https://user-images.githubusercontent.com/62803763/132259234-0c82e3c5-73c5-4a4d-a800-f8e1ce203d67.PNG){: .align-center .open-new}

> 17 < 19 이므로 ERROR!
