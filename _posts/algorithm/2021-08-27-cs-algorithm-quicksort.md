---
title: "[Algorithm] 퀵 정렬(Quick Sort)"
excerpt: 알고리즘 퀵 정렬
categories:
- Algorithm
tags:
- - Algorithm
  - CS
  - Programming
toc: true
toc_sticky: true
popular: true
date: '2021-08-27T05:20:00'
last_modified_at: 2021-08-27T05:20:00
---

## 1. 퀵 정렬(Quick Sort)

* 정렬 알고리즘의 꽃
* 기준점(pivot)을 정해서, pivot보다 작은 데이터는 왼쪽, 큰 데이터는 오른쪽으로 모으는 함수를 작성
* 각 왼쪽, 오른쪽은 재귀용법을 사용해서 다시 동일 함수를 호출하여 위 작업을 반복
* 함수는 왼쪽 + pivot + 오른쪽을 리턴


### - 어떻게 코드로 만들까?

프로그래밍 연습<br>
다음 리스트를 리스트 슬라이싱을 이용해서 세 개로 짤라서 각 리스트 변수에 넣고 출력해보기<br>

<pre>
data_list = [1, 2, 3, 4, 5]
출력:
print (data1)
print (data2)
print (data3)
[1, 2]
3
[4, 5]
</pre>

```python
data_list = [1, 2, 3, 4, 5]
data1 = data_list[:2]
data2 = data_list[2]
data3 = data_list[3:]

print(data1)  # [1, 2]
print(data2)  # 3
print(data3)  # [4, 5]
```

<br>

프로그래밍 연습<br>
다음 리스트를 맨 앞에 데이터를 기준으로 작은 데이터는 left 변수에, 그렇지 않은 데이터는 right 변수에 넣기<br>

<pre>
data_list = [4, 1, 2, 5, 7]
</pre>

```python
data_list = [4, 1, 2, 5, 7]
pivot = data_list[0]
left, right = list(), list()

for i in range(1, len(data_list)) :
    if pivot > data_list[i] :
        left.append(data_list[i])
    else :
        right.append(data_list[i])

print(left)  # [1, 2]
print(pivot)  # 4
print(right)  # [5, 7]
```

<br>

프로그래밍 연습<br>
data_list 가 임의 길이일 때 리스트를 맨 앞에 데이터를 기준으로 작은 데이터는 left 변수에, 그렇지 않은 데이터는 right 변수에 넣기<br>

<pre>
import random 
data_list = random.sample(range(100), 10)

left = list()
right = list()
pivot = data_list[0]

for index in range(1, -----------------):
    if data_list[index] < pivot:
        left.append(data_list[index])
    else:
        right.append(data_list[index])
</pre>

```python
import random
data_list = random.sample(range(100), 10)

left, right = list(), list()
pivot = data_list[0]

for i in range(1, len(data_list)) :
    if pivot > data_list[i] :
        left.append(data_list[i])
    else :
        right.append(data_list[i])
        
print(left)  # [2, 21]
print(pivot)  # 22
print(right)  # [31, 24, 55, 40, 26, 97, 78]
```


<br>

### 2. 알고리즘 구현

* quicksort 함수 만들기
    - 만약 리스트 갯수가 한개이면 해당 리스트 리턴
    - 그렇지 않으면, 리스트 맨 앞의 데이터를 pivot으로 놓기
    - left, right 리스트 변수를 만들고,
    - 맨 앞의 데이터를 뺀 나머지 데이터를 pivot과 비교
        - pivot보다 작으면 left.append(해당 데이터)
        - pivot보다 크면 right.append(해당 데이터)
    - return quicksort(left) + pivot + quicksort(right) 로 재귀 호출
  
> 리스트로 만들어서 리턴 : return quick_sort(left) + [pivot] + quick_sort(right)

```python
def qsort(data) :
    if len(data) <= 1 :
        return data
    left, right = list(), list()
    pivot = data[0]
    for index in range(1, len(data)) :
        if pivot > data[index] :
            left.append(data[index])
        else :
            right.append(data[index])
    return qsort(left) + [pivot] + qsort(right)


# 테스트
import random

data_list = random.sample(range(100), 10)
qsort(data_list)  # [8, 15, 34, 38, 39, 42, 69, 70, 77, 82]
```

<br>

프로그래밍 연습<br>
위 퀵정렬 코드를 파이썬 list comprehension을 사용해서 더 깔끔하게 작성해보기<br>

```python
def qsort(data) :
    if len(data) <= 1 :
        return data
    pivot = data[0]
    left = [item for item in data[1:] if pivot > item]
    right = [item for item in data[1:] if pivot <= item]
    return qsort(left) + [pivot] + qsort(right)


# 테스트
import random

data_list = random.sample(range(100), 10)
qsort(data_list)  # [6, 53, 57, 61, 65, 81, 90, 92, 93, 94]
```


<br>

## 3. 알고리즘 분석

* 병합정렬과 유사, 시간복잡도는 O(nlogn)
* 단, 최악의 경우 
    - 맨 처음 pivot이 가장 크거나, 가장 작으면
    - 모든 데이터를 비교하는 상황이 나옴
    - O($n^2$)

<br>

<img src="https://www.fun-coding.org/00_Images/quicksortworks.jpg" />