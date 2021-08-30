---
title: "[Algorithm] 순차 탐색(Sequential Search)"
excerpt: 알고리즘 순차 탐색
categories:
  - Algorithm
tags:
  - - Algorithm
    - CS
    - Programming
    - Python
toc: true
toc_sticky: true
popular: true
date: "2021-08-31T04:00:00"
last_modified_at: 2021-08-31T04:00:00
---

## 1. 순차 탐색 (Sequential Search)

### - 순차 탐색이란?

- 탐색은 여러 데이터 중에서 원하는 데이터를 찾아내는 것
- 데이터가 담겨있는 리스트를 앞에서부터 하나씩 비교해서 원하는 데이터를 찾는 방법

<br>

## 2. 알고리즘 구현 및 테스트

프로그래밍 연습<br>
임의 리스트가 다음과 같이 rand_data_list로 있을 때, 원하는 데이터의 위치를 리턴하는 순차탐색 알고리즘 작성<br>

- 가장 기본적인 방법이므로, 직접 작성
- 원하는 데이터가 리스트에 없을 경우 -1을 리턴

<pre>
# 데이터 준비: data_list 10개 만들기
from random import *
 
rand_data_list = list()
for num in range(10):
    rand_data_list.append(randint(1, 100))
</pre>

<br>

```python
def sequential(data_list, search_data) :
    for index in range(len(data_list)) :
        if data_list[index] == search_data :
            return index
    return -1


# 테스트
from random import *

rand_data_list = list()
for num in range(10) :
    rand_data_list.append(randint(1, 100))

rand_data_list  # [50, 32, 56, 2, 62, 36, 40, 15, 15, 65]

sequential(rand_data_list, 62)  # 4
sequential(rand_data_list, 999)  # -1
```

<br>

## 3. 알고리즘 분석

- 최악의 경우 리스트 길이가 n일 때, n번 비교해야 함
- O(n)
