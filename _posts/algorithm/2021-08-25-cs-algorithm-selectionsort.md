---
title: "[Algorithm] 선택 정렬(Selection Sort)"
excerpt: 알고리즘 선택 정렬
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
date: "2021-08-25T00:30:00"
last_modified_at: 2021-08-25T00:30:00
---

## 1. 선택 정렬 (Selection Sort)

### - 선택 정렬이란?

- 다음과 같은 순서를 반복하며 정렬하는 알고리즘
  1. 주어진 데이터 중, 최소값을 찾음
  2. 해당 최소값을 데이터 맨 앞에 위치한 값과 교체
  3. 맨 앞의 위치를 뺀 나머지 데이터를 동일한 방법으로 반복
- 직접 눈으로 보기 [https://visualgo.net/en/sorting](https://visualgo.net/en/sorting){:target="\_blank"}

<br>

<img src="https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif" width=100>

> 출처: https://en.wikipedia.org/wiki/Selection_sort

### - 어떻게 코드로 만들까?

- 데이터가 두 개 일때 : data_list = [9, 1]
  - data*list[0] > data_list[1] 이므로 data_list[0] 값과 data* list[1] 값을 교환
- 데이터가 세 개 일때 : data_list = [9, 1, 7]
  - 처음 한번 실행하면, 1, 9, 7 이 됨
  - 두 번째 실행하면, 1, 7, 9 가 됨
- 데이터가 네 개 일때 : data_list = [9, 3, 2, 1]
  - 처음 한번 실행하면, 1, 3, 2, 9 가 됨
  - 두 번째 실행하면, 1, 2, 3, 9 가 됨
  - 세 번째 실행하면, 변화 없음

<br>

## 2. 알고리즘 구현

1. for stand in range(len(data_list) - 1) 로 반복
2. lowest = stand 로 놓고,
3. for num in range(stand, len(data_list)) stand 이후부터 반복
   - 내부 반복문 안에서 data_list[lowest] > data_list[num] 이면,
     - lowest = num
4. data_list[num], data_list[lowest] = data_list[lowest], data_list[num]

```python
def selection_sort(data) :
  for stand in range(len(data) - 1) :
    lowest = stand
    for i in range(stand + 1, len(data)) :
      if data[lowest] > data[i] :
        lowest = i
    data[lowest], data[stand] = data[stand], data[lowest]
  return data


# 테스트
import random

data_list = random.sample(range(100), 10)
selection_sort(data_list)  # [1, 5, 36, 41, 55, 67, 68, 91, 95, 98]
```

<br>

## 3. 알고리즘 분석

- 반복문이 두 개 O($n^2$)
- 실제로 상세하게 계산하면, $\frac { n * (n - 1)}{ 2 }$
