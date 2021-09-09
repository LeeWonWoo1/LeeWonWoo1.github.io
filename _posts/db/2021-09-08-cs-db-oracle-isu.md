---
title: "[Oracle] INSERT, SELECT, UPDATE"
excerpt: Oracle 삽입, 조회, 수정
categories:
  - DB
tags:
  - - DB
    - Oracle
    - CS
toc: true
toc_sticky: true
popular: true
date: "2021-09-08T03:00:00"
last_modified_at: 2021-09-08T03:00:00
---

[DB 무료 연습 사이트](http://www.sqlfiddle.com/){:target="\_blank"}
{: .notice--info}

## 1. INSERT

```java
INSERT INTO 테이블(컬럼) VALUES(값);
//              or
INSERT INTO 데이블 VALUES(타입 순서대로 넣은 값);
```

<br>

![oracle-insert1](https://user-images.githubusercontent.com/62803763/132394020-90abbb9f-ea9b-42a7-add5-32dbe3deafca.PNG){: .align-center .open-new}

![oracle-insert2](https://user-images.githubusercontent.com/62803763/132394022-3f5bec18-c0a6-489f-8b07-2a746d7da403.PNG){: .align-center .open-new}

<br>

## 2. SELECT

```java
SELECT * FROM 테이블  // 테이블의 모든 컬럼 조회
SELECT 컬럼, 컬럼 ... FROM 테이블  // 테이블에서 원하는 컬럼만 조회
```

<br>

![oracle-select1](https://user-images.githubusercontent.com/62803763/132394657-15e3efc4-1e72-451f-83bc-9a1355dcc1ef.PNG){: .align-center .open-new}

![oracle-select2](https://user-images.githubusercontent.com/62803763/132394660-2a565a60-53e9-43e7-9182-689b797d9bb8.PNG){: .align-center .open-new}

<br>

## 3. UPDATE

```java
UPDATE 테이블 SET 컬럼 = 바꿀 값
WHERE 컬럼 = 변경 조건
```

<br>

![oracle-update1](https://user-images.githubusercontent.com/62803763/132395358-8c843db2-4f45-4ad7-8114-214c3454b934.PNG){: .align-center .open-new}

![oracle-update2](https://user-images.githubusercontent.com/62803763/132395356-edc4d514-8712-45ab-9675-a610f70e2e27.PNG){: .align-center .open-new}

<br>

### - 조건 설정

- 문제 인식 : 동명이인의 'LWW'가 의도와 상관없이 모두 수정됨

![oracle-update3](https://user-images.githubusercontent.com/62803763/132395606-93f2d59b-5e9b-4dea-857f-9c06d9fcb644.PNG){: .align-center .open-new}

![oracle-update4](https://user-images.githubusercontent.com/62803763/132395611-ecbb5e24-4eb0-4e17-9c0f-a89a64264445.PNG){: .align-center .open-new}

<br>

- 해결책 : 조건을 설정해 원하는 컬럼의 데이터만 수정

![oracle-update5](https://user-images.githubusercontent.com/62803763/132396056-252c4275-a706-46aa-bfee-775b28065410.PNG){: .align-center .open-new}

![oracle-update6](https://user-images.githubusercontent.com/62803763/132396060-1a8ce89d-02c4-40e4-9b20-0fc18eba588f.PNG){: .align-center .open-new}
