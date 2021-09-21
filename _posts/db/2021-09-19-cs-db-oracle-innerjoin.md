---
title: "[Oracle] INNER JOIN"
excerpt: Oracle INNER JOIN
categories:
  - DB
tags:
  - - DB
    - Oracle
    - CS
toc: true
toc_sticky: true
popular: true
date: "2021-09-18T22:00:00"
last_modified_at: 2021-09-18T22:00:00
---

[DB 무료 연습 사이트](http://www.sqlfiddle.com/){:target="\_blank"}
{: .notice--info}

## INNER JOIN

- 같은 값의 행을 조회하는 JOIN

```java
SELECT 컬럼 FROM 테이블1, 테이블2
WHERE 조건
```

<br>

- a의 NAME 컬럼과 b의 NAME 컬럼이 같을 때의 컬럼 조회

![oracle-innerjoin1](https://user-images.githubusercontent.com/62803763/134181162-eb9fe2c7-cda9-4f6f-b332-2b57d2483c2e.PNG){: .align-center .open-new}

![oracle-innerjoin2](https://user-images.githubusercontent.com/62803763/134181169-7eb6c5c1-8788-434b-b206-26cf24dfe49a.PNG){: .align-center .open-new}

<br>

## ANSI INNER JOIN

- 미국 국립 표준 협회에서 모든 SQL에 사용할 수 있도록 만든 문법
- ANSI를 사용하면 어떤 SQL에서도 동일한 문법으로 사용 가능

```java
SELECT 컬럼 FROM 테이블1
INNER JOIN 테이블2
ON 조건
```

<br>

![oracle-innerjoin3](https://user-images.githubusercontent.com/62803763/134181811-bcebbc23-eea0-4768-b248-a09783f30f95.PNG){: .align-center .open-new}

![oracle-innerjoin4](https://user-images.githubusercontent.com/62803763/134181815-d84e4524-6693-4b34-b601-8fb1ca40ec53.PNG){: .align-center .open-new}
