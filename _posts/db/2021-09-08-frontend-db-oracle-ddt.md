---
title: "[Oracle] DELETE, DROP, TRUNCATE"
excerpt: Oracle 행 삭제, 테이블 삭제
categories:
  - DB
tags:
  - - DB
    - Oracle
    - CS
toc: true
toc_sticky: true
popular: true
date: "2021-09-08T04:00:00"
last_modified_at: 2021-09-08T04:00:00
---

[DB 무료 연습 사이트](http://www.sqlfiddle.com/){:target="\_blank"}
{: .notice--info}

## 1. DELETE

- 테이블의 행 삭제

```java
DELETE FROM 테이블
  WHERE 컬럼 = '값'
  AND 컬럼 = '값';
```

<br>

![oracle-delete1](https://user-images.githubusercontent.com/62803763/132397103-86627a4d-fb65-4d4c-a7c9-2d79734d86a4.PNG){: .align-center .open-new}

![oracle-delete2](https://user-images.githubusercontent.com/62803763/132397105-c86ee74c-f7ab-458d-8946-6847f70c3022.PNG){: .align-center .open-new}

<br>

## 2. DROP

- 테이블 자체를 삭제

```java
DROP TABLE 테이블;
```

<br>

![oracle-drop1](https://user-images.githubusercontent.com/62803763/132397833-23153358-aa60-41a5-88c4-bbebd6c133b4.PNG){: .align-center .open-new}

<br>

## 3. TRUNCATE

- 테이블 내의 데이터를 삭제

```java
TRUNCATE TABLE 테이블;
```

<br>

![oracle-truncate1](https://user-images.githubusercontent.com/62803763/132397837-eee578d2-ec31-4ed0-94ec-8f9aad936629.PNG){: .align-center .open-new}
