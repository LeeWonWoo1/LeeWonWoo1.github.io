---
title: "[Oracle] NVL, NVL2"
excerpt: Oracle NVL, NVL2
categories:
  - DB
tags:
  - - DB
    - Oracle
    - CS
toc: true
toc_sticky: true
popular: true
date: "2021-09-24T23:00:00"
last_modified_at: 2021-09-24T23:00:00
---

[DB 무료 연습 사이트](http://www.sqlfiddle.com/){:target="\_blank"}
{: .notice--info}

## 1. NVL

- NULL 값을 다른 값으로 채워서 보여주는 것

```java
NVL(컬럼, NULL일 때의 값)
```

<br>

![oracle-nvl1](https://user-images.githubusercontent.com/62803763/134692608-da86f178-e812-4242-9422-c137b3a82c8c.PNG){: .align-center .open-new}

![oracle-nvl2](https://user-images.githubusercontent.com/62803763/134692612-e9a646c0-eda4-4db2-993d-7dcb0c677bfc.PNG){: .align-center .open-new}

![oracle-nvl3](https://user-images.githubusercontent.com/62803763/134692614-844f7668-9af1-427b-9152-0d7ec2ae3e8f.PNG){: .align-center .open-new}

<br>

## 2. NVL2

- NULL 값과 NULL이 아닐 때의 값 모두 정해서 보여줌

```java
NVL2(컬럼, NULL 아닐 때의 값, NUL일 때의 값)
```

<br>

![oracle-nvl4](https://user-images.githubusercontent.com/62803763/134693344-14df3aab-998b-48c5-907f-a4d2dcbdb4eb.PNG){: .align-center .open-new}

![oracle-nvl5](https://user-images.githubusercontent.com/62803763/134693348-455b0744-3c8d-49d3-8b58-aba0d2398724.PNG){: .align-center .open-new}
