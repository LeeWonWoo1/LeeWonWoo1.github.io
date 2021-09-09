---
title: "[Oracle] COMMIT, ROLLBACK"
excerpt: Oracle 적용, 되돌리기
categories:
  - DB
tags:
  - - DB
    - Oracle
    - CS
toc: true
toc_sticky: true
popular: true
date: "2021-09-09T23:00:00"
last_modified_at: 2021-09-09T23:00:00
---

[DB 무료 연습 사이트](http://www.sqlfiddle.com/){:target="\_blank"}
{: .notice--info}

## COMMIT, ROLLBACK

- COMMIT : 변경된 내용을 실제 DB에 적용하는 것
- ROLLBACK : 변경된 내용을 마지막 COMMIT의 상태로 되돌리는 것

```java
COMMIT;
ROLLBACK;
```

<br>

![oracle-cr1](https://user-images.githubusercontent.com/62803763/132707342-53147518-0d2e-4f02-a398-e8184138f766.PNG)

![oracle-cr2](https://user-images.githubusercontent.com/62803763/132707345-33afdbf5-b428-45b0-9ba4-fc0a58dc9750.PNG)

COMMIT 한 시점에서 두 줄만 삽입됐기 때문에<br>
추가로 삽입한 내용은 들어가지 않고,<br>
두 줄만 삽입된 상태로 돌아감
