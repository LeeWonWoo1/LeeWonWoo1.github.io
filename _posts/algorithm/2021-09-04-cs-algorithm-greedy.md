---
title: "[Algorithm] 탐욕 알고리즘(Greedy)"
excerpt: 탐욕 알고리즘
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
date: "2021-09-04T00:10:00"
last_modified_at: 2021-09-04T00:10:00
---

## 1. 탐욕 알고리즘이란?

- Greedy Algorithm 또는 탐욕 알고리즘
- 최적의 해에 가까운 값을 구하기 위해 사용
- 여러 경우 중 하나를 결정해야할 때마다, **매순간 최적이라고 생각되는 경우를 선택**하는 방식으로 진행해서, 최종적인 값을 구하는 방식

<br>

## 2. 탐욕 알고리즘 예

### - 문제 1 : 동전 문제

- 지불해야 하는 값이 4720원 일 때 1원 50원 100원, 500원 동전으로 동전의 수가 가장 적게 지불
- 가장 큰 동전부터 최대한 지불해야 하는 값을 채우는 방식으로 구현
- 탐욕 알고리즘으로 매순간 최적이라고 생각되는 경우를 선택

```python
coin_list = [500, 100, 50, 1]

def min_coin_count(value, coin_list) :
  total_coin_count = 0
  details = list()
  coin_list.sort(reverse=True)

  for coin in coin_list :
    coin_num = value // coin
    total_coin_count += coin_num
    value -= coin_num * coin
    details.append([coin, coin_num])

  return total_coin_count, details


# 테스트
min_coin_count(4720, coin_list)  # (31, [[500, 9], [100, 2], [50, 0], [1, 20]])
```

<br>

### - 문제 2 : 부분 배낭 문제

- 무게 제한이 k인 배낭에 최대 가치를 가지도록 물건을 넣는 문제
  - 각 물건은 무게(w)와 가치(v)로 표현
  - 물건은 쪼갤 수 있으므로 물건의 일부분이 배낭에 넣어질 수 있음, Fractional Knapsack Problem
    - Fractional Knapsack Problem 의 반대로 물건을 쪼개서 넣을 수 없는 배낭 문제도 존재 (0/1 Knapsack Problem)

<br>

<img src="https://www.fun-coding.org/00_Images/knapsack.png">

```python
data_list = [(10, 10), (15, 12), (20, 10), (25, 8), (30, 5)]

def get_max_value(data_list, capacity) :
  data_list = sorted(data_list, key = lambda x : x[1] / x[0], reverse = True)
  total_value = 0
  details = list()

  for data in data_list :
    if capacity - data[0] >= 0 :
      capacity -= data[0]
      total_value += data[1]
      details.append([data[0], data[1], 1])
    else :
      fraction = capacity / data[0]
      total_value += data[1] * fraction
      details.append([data[0], data[1], fraction])
      break
  return total_value, details


# 테스트
get_max_value(data_list, 30)  # (24.5, [[10, 10, 1], [15, 12, 1], [20, 10, 0.25]])
```

<br>

## 3. 탐욕 알고리즘의 한계

- 탐욕 알고리즘은 근사치 추정에 활용
- 반드시 최적의 해를 구할 수 있는 것은 아님
- 최적의 해에 가까운 값을 구하는 방법 중의 하나

<br>

<img src="https://www.fun-coding.org/00_Images/greedy.png" width=300>

<br>

- '시작' 노드에서 시작해서 가장 작은 값을 찾아 leaf node 까지 가는 경로
- Greedy 알고리즘 적용시 시작 -> 7 -> 12 를 선택하게 되므로 7 + 12 = 19
- 하지만 실제 가장 작은 값은 시작 -> 10 -> 5 이며, 10 + 5 = 15
