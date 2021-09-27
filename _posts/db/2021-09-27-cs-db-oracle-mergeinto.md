---
title: "[Oracle] MERGE INTO"
excerpt: Oracle MERGE INTO
categories:
  - DB
tags:
  - - DB
    - Oracle
    - CS
toc: true
toc_sticky: true
popular: true
date: "2021-09-27T21:00:00"
last_modified_at: 2021-09-27T21:00:00
---

[DB 무료 연습 사이트](http://www.sqlfiddle.com/){:target="\_blank"}
{: .notice--info}

## MERGE INTO

- IF~ ELSE~문과 유사
- 조건을 만족하면 INSERT나 UPDATE 등을 수행

```java
MERGE INTO 테이블
  USING 비교 테이블  // 없으면 DUAL
    ON (조건)  // 테이블 KEY 사용
WHEN MATCHED THEN  // 조건 만족
  UPDATE ~~
WHEN NOT MATCHED THEN  // 조건 비만족
  INSERT ~~
```

<br>

### - 조건 만족시

![oracle-mergeinto1](https://user-images.githubusercontent.com/62803763/134906970-631d6d2d-c195-4bf8-bbfd-639b4f0eb58d.PNG){: .align-center .open-new}

![oracle-mergeinto2](https://user-images.githubusercontent.com/62803763/134906976-e28b1732-3df9-460f-8b79-e2d4d153ff7f.PNG){: .align-center .open-new}

<br>

### - 조건 비만족시

![oracle-mergeinto3](https://user-images.githubusercontent.com/62803763/134906978-b5e74422-f73a-4b81-9056-6c23fe5c13d7.PNG){: .align-center .open-new}

![oracle-mergeinto4](https://user-images.githubusercontent.com/62803763/134906980-c8367fe6-5b57-400f-9dd1-da7db29abae2.PNG){: .align-center .open-new}
