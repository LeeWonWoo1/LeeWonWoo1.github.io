---
title: "[Oracle] ROWNUM"
excerpt: Oracle 특정 행 추출
categories:
  - DB
tags:
  - - DB
    - Oracle
    - CS
toc: true
toc_sticky: true
popular: true
date: "2021-09-16T21:00:00"
last_modified_at: 2021-09-16T21:00:00
---

[DB 무료 연습 사이트](http://www.sqlfiddle.com/){:target="\_blank"}
{: .notice--info}

## ROWNUM

- Oracle에서 제공하는 가상의 컬럼으로 출력한 행이 몇 번째 행인지 보여줌
- 수 많은 행을 한번에 조회하는 경우 시간이 오래걸릴 수 있음
- 따라서 적은 수의 행을 추출하는 경우에는 ROWNUM을 활용할 수 있음

![oracle-rownum1](https://user-images.githubusercontent.com/62803763/133617804-02fb242f-2e64-4d52-a7ba-5e427eab7fcb.PNG){: .align-center .open-new}

![oracle-rownum2](https://user-images.githubusercontent.com/62803763/133617809-2c2d1912-5de2-4c0c-8109-3df9f0bc6e9f.PNG){: .align-center .open-new}

![oracle-rownum3](https://user-images.githubusercontent.com/62803763/133617811-8cc656f0-1114-4777-b9f3-ac0ead319e7f.PNG){: .align-center .open-new}

<br>

- 1부터 시작해 행에 따라 1씩 증가하는 가상의 컬럼
- SELECT문제 ROWNUM을 넣으면 출력 가능

![oracle-rownum4](https://user-images.githubusercontent.com/62803763/133618177-72dbe22c-2c92-4dad-8dfa-c837b9c6c25e.PNG){: .align-center .open-new}

![oracle-rownum5](https://user-images.githubusercontent.com/62803763/133618183-b791cd2f-92fe-4924-8d19-9335feb65719.PNG){: .align-center .open-new}

<br>

- ORDER BY와 함께 사용하면 활용하기 어려운 숫자로 출력됨

![oracle-rownum6](https://user-images.githubusercontent.com/62803763/133618597-d91714a9-4219-46c7-b1a9-66cac7d34d15.PNG){: .align-center .open-new}

![oracle-rownum7](https://user-images.githubusercontent.com/62803763/133618601-46d861af-0493-4ca7-8b89-7eb2def6a676.PNG){: .align-center .open-new}

<br>

- 따라서 서브쿼리를 사용하여 ORDER BY를 처리하고 ROWNUM을 사용해야 함

![oracle-rownum8](https://user-images.githubusercontent.com/62803763/133619309-c53d34b9-b9f4-4d4e-a127-066d27ff4dd2.PNG){: .align-center .open-new}

![oracle-rownum9](https://user-images.githubusercontent.com/62803763/133619312-6bc5b9cc-6e7e-4bbb-9394-f1e0a03f6d0d.PNG){: .align-center .open-new}
