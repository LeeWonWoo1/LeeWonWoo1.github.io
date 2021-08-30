---
title: "[Algorithm] 병합 정렬(Merge Sort)"
excerpt: 알고리즘 병합 정렬
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
date: "2021-08-31T03:00:00"
last_modified_at: 2021-08-31T03:00:00
---

## 1. 병합 정렬 (Merge Sort)

- 재귀용법을 활용한 정렬 알고리즘
  1. 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눔
  2. 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬
  3. 두 부분 리스트를 다시 하나의 정렬된 리스트로 합병
- 직접 눈으로 보기: [https://visualgo.net/en/sorting](https://visualgo.net/en/sorting){:target="\_blank"}

<br>

<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif" width=500/>

출처: [위키피디아](https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC){:target="\_blank"}

<br>

### - 알고리즘 이해

- 데이터가 네 개 일때
  - 예: data_list = [1, 9, 3, 2]
    - 먼저 [1, 9], [3, 2] 로 나누고
    - 다시 앞 부분은 [1], [9] 로 나누고
    - 다시 정렬해서 합친다. [1, 9]
    - 다음 [3, 2] 는 [3], [2] 로 나누고
    - 다시 정렬해서 합친다 [2, 3]
    - 이제 [1, 9] 와 [2, 3]을 합친다.
      - 1 < 2 이니 [1]
      - 9 > 2 이니 [1, 2]
      - 9 > 3 이니 [1, 2, 3]
      - 9 밖에 없으니, [1, 2, 3, 9]

<br>

### - 알고리즘 구현

- mergesplit 함수 만들기

  - 만약 리스트 갯수가 한개이면 해당 값 리턴
  - 그렇지 않으면, 리스트를 앞뒤, 두 개로 나누기
  - left = mergesplit(앞)
  - right = mergesplit(뒤)
  - merge(left, right)

- merge 함수 만들기
  - 리스트 변수 하나 만들기 (sorted)
  - left_index, right_index = 0
  - while left_index < len(left) or right_index < len(right):
    - 만약 left_index 나 right_index 가 이미 left 또는 right 리스트를 다 순회했다면, 그 반대쪽 데이터를 그대로 넣고, 해당 인덱스 1 증가
    - if left[left_index] < right[right_index]:
      - sorted.append(left[left_index])
      - left_index += 1
    - else:
      - sorted.append(right[right_index])
      - right_index += 1

#### @1. 작은 부분부터 작성해서 하나씩 구현

프로그래밍 연습<br>
어떤 데이터리스트가 있을 때 리스트를 앞뒤로 짜르는 코드 작성 (일반화)

```python
def split_func(data) :
    medium = int(len(data) / 2)
    print (medium)
    left = data[:medium]
    right = data[medium:]
    print (left, right)

split_func([1, 5, 3, 2, 4])  # 2
                             # [1, 5] [3, 2, 4]
```

<br>

#### @2. 재귀용법 활용하기

프로그래밍 연습<br>

<pre>
다음 문장을 코드로 작성 (merge함수는 아직은 없는 상태, 있다고만 가정)
* mergesplit 함수 만들기
  - 만약 리스트 갯수가 한개이면 해당 값 리턴
  - 그렇지 않으면, 리스트를 앞뒤, 두 개로 나누기
  - left = mergesplit(앞)
  - right = mergesplit(뒤)
  - merge(left, right)
</pre>

```python
def mergesplit(data) :
    if len(data) <= 1 :
        return data
    medium = int(len(data) / 2)
    left = mergesplit(data[:medium])
    right = mergesplit(data[medium:])
    return merge(left, right)
```

<br>

#### @3. merge 함수 만들기

- 목표 : left 와 right 의 리스트 데이터를 정렬해서 sorted_list 라는 이름으로 return
- left와 right는 이미 정렬된 상태 또는 데이터가 하나

```python
def merge(left, right) :
    merged = list()
    left_point, right_point = 0, 0

    # case 1: left/right 아직 남아있을 때
    while len(left) > left_point and len(right) > right_point :
        if left[left_point] > right[right_point] :
            merged.append(right[right_point])
            right_point += 1
        else :
            merged.append(left[left_point])
            left_point += 1

    # case 2 : left만 남아있을 때
    while len(left) > left_point :
        merged.append(left[left_point])
        left_point += 1

    # case 3 : right만 남아있을 때
    while len(right) > right_point :
        merged.append(right[right_point])
        right_point += 1

    return merged
```

<br>

## 2. 최종 코드 및 테스트

```python
def merge(left, right) :
    merged = list()
    left_point, right_point = 0, 0

    # case 1: left/right 아직 남아있을 때
    while len(left) > left_point and len(right) > right_point :
        if left[left_point] > right[right_point] :
            merged.append(right[right_point])
            right_point += 1
        else :
            merged.append(left[left_point])
            left_point += 1

    # case 2 : left만 남아있을 때
    while len(left) > left_point :
        merged.append(left[left_point])
        left_point += 1

    # case 3 : right만 남아있을 때
    while len(right) > right_point :
        merged.append(right[right_point])
        right_point += 1

    return merged

def mergesplit(data) :
    if len(data) <= 1 :
        return data
    medium = int(len(data) / 2)
    left = mergesplit(data[:medium])
    right = mergesplit(data[medium:])
    return merge(left, right)


# 테스트
import random
data_list = random.sample(range(100), 10)
mergesplit(data_list)  # [7, 12, 20, 36, 38, 45, 59, 71, 78, 86]
```

<br>

## 3. 알고리즘 분석

- 알고리즘 분석은 쉽지 않음. 이 부분은 참고로만 알기
- 다음을 보고 이해
  - 몇 단계 깊이까지 만들어지는지를 depth 라고 하고 i로 놓음. 맨 위 단계는 0으로 놓음
    - 다음 그림에서 n/$2^2$ 는 2단계 깊이라고 해봄
    - 각 단계에 있는 하나의 노드 안의 리스트 길이는 n/$2^2$ 가 됨
    - 각 단계에는 $2^i$ 개의 노드가 있음
  - 따라서, 각 단계는 항상 $2^i * \frac { n }{ 2^i } = O(n)$
  - 단계는 항상 $log_2 n$ 개 만큼 만들어짐, 시간 복잡도는 결국 O(log n), 2는 역시 상수이므로 삭제
  - 따라서, 단계별 시간 복잡도 O(n) \* O(log n) = O(n log n)

<br>

<img src="https://www.fun-coding.org/00_Images/mergesortcomplexity.png" />
