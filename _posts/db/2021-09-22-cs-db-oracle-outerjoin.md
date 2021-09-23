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

## 1. OUTER JOIN

- 값이 없어도 행이 출력되게 해주는 것
- 값이 없는 쪽에 (+)를 붙임

![oracle-outerjoin1](https://user-images.githubusercontent.com/62803763/134348170-18423a77-b11b-4932-8094-30d4cf2c54d8.PNG){: .align-center .open-new}

![oracle-outerjoin2](https://user-images.githubusercontent.com/62803763/134348173-4037e82a-2041-4c02-9038-e021ba266b73.PNG){: .align-center .open-new}

<br>

## 2. ANSI LEFT OUTER JOIN

```java
SELECT 컬럼 FROM 값이 있는 테이블
LEFT JOIN 값이 없는 테이블
ON 조건
```

<br>

![oracle-outerjoin3](https://user-images.githubusercontent.com/62803763/134522195-bbb0e821-e78b-4165-a43c-d2a50105c5a2.PNG){: .align-center .open-new}

![oracle-outerjoin4](https://user-images.githubusercontent.com/62803763/134522199-ca45a271-84cd-4098-94dc-42d1107d4c51.PNG){: .align-center .open-new}

<br>

## 3. ANSI RIGHT OUTER JOIN

```java
SELECT 컬럼 FROM 값이 없는 테이블
RIGHT JOIN 값이 있는 테이블
ON 조건
```

<br>

![oracle-outerjoin5](https://user-images.githubusercontent.com/62803763/134522200-d6014e11-2163-4fb0-b582-bc85cddd29dc.PNG){: .align-center .open-new}

![oracle-outerjoin6](https://user-images.githubusercontent.com/62803763/134522202-b86e15c6-87ef-46a8-a643-dae71f338837.PNG){: .align-center .open-new}

<br>

## 4. ANSI FULL OUTER JOIN

- 양 테이블에 값이 없는 경우에도 모두 출력

```java
SELECT 컬럼 FROM 테이블
FULL OUTER JOIN 테이블
ON 조건
```

<br>

![oracle-outerjoin7](https://user-images.githubusercontent.com/62803763/134522205-1aef7d29-9869-41f0-9423-3b9b5a4b58b0.PNG){: .align-center .open-new}

![oracle-outerjoin8](https://user-images.githubusercontent.com/62803763/134522206-8b6db464-5ac9-4dd6-a77a-7e8fbc289e6d.PNG){: .align-center .open-new}
