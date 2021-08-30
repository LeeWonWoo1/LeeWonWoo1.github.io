---
title: "[Data Structure] 배열(Array)"
excerpt: 자료구조 배열
categories:
  - DS
tags:
  - - DS
    - CS
    - Programming
    - Python
toc: true
toc_sticky: true
popular: true
date: "2021-08-19T20:00:00"
last_modified_at: 2021-08-19T20:00:00
---

## 1. 배열 (Array)

- 데이터를 나열하고, 각 데이터를 index에 대응하도록 구성한 데이터 구조
- Python에서는 리스트 타입이 배열 기능을 제공함

### - 배열은 왜 필요할까?

- 같은 종류의 데이터를 효율적으로 관리하기 위해 사용
- 같은 종류의 데이터를 순차적으로 저장
- 장점: 빠른 접근 가능
  - 첫 데이터의 위치에서 상대적인 위치로 데이터 접근(index 번호로 접근)
- 단점: 데이터 추가/삭제의 어려움
  - 미리 최대 길이를 지정해야 함

### - 파이썬과 C 언어의 배열 예제

```c
// C
// include <stdio.h>

int main(int argc, char * argv[])
{
    char country[3] = "US";
    printf ("%c%c\n", country[0], country[1]);
    printf ("%s\n", country);
    return 0;
}
```

<br>

```python
# Python

country = 'US'
print(country)  # US

country = country + 'A'
print(country)  # USA
```

<br>

### - 파이썬과 배열

- 파이썬에서는 리스트로 배열 구현 가능

```python
# 1차원 배열 : 리스트로 구현시
data_list = [1, 2, 3, 4, 5]
data_list  # [1, 2, 3, 4, 5]


# 2차원 배열 : 리스트로 구현시
data_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
data_list  # [[1, 2, 3], [4, 5, 6], [7, 8, 9]]


print(data_list[0])  # [1, 2, 3]
print(data_list[0][0])  # 1
print(data_list[0][1])  # 2
print(data_list[0][2])  # 3
print(data_list[1][0])  # 4
print(data_list[1][1])  # 5
```

<br>

## 2. 프로그래밍 연습

```python
# 연습1 : 위의 2차원 배열에서 9, 8, 7 순서대로 출력

print(data_list[2][2], data_list[2][1], data_list[2][0])
```

<br>

```python
# 연습2 : 아래 dataset에서 전체 M 의 빈도수 출력하기

# dataset
dataset = ['Braund, Mr. Owen Harris',
'Cumings, Mrs. John Bradley (Florence Briggs Thayer)',
'Heikkinen, Miss. Laina',
'Futrelle, Mrs. Jacques Heath (Lily May Peel)',
'Allen, Mr. William Henry',
'Moran, Mr. James',
'McCarthy, Mr. Timothy J',
'Palsson, Master. Gosta Leonard',
'Johnson, Mrs. Oscar W (Elisabeth Vilhelmina Berg)',
'Nasser, Mrs. Nicholas (Adele Achem)',
'Sandstrom, Miss. Marguerite Rut',
'Bonnell, Miss. Elizabeth',
'Saundercock, Mr. William Henry',
'Andersson, Mr. Anders Johan',
'Vestrom, Miss. Hulda Amanda Adolfina',
'Hewlett, Mrs. (Mary D Kingcome) ',
'Rice, Master. Eugene',
'Williams, Mr. Charles Eugene',
'Vander Planke, Mrs. Julius (Emelia Maria Vandemoortele)',
'Masselmani, Mrs. Fatima',
'Fynney, Mr. Joseph J',
'Beesley, Mr. Lawrence',
'McGowan, Miss. Anna "Annie"',
'Sloper, Mr. William Thompson',
'Palsson, Miss. Torborg Danira',
'Asplund, Mrs. Carl Oscar (Selma Augusta Emilia Johansson)',
'Emir, Mr. Farred Chehab',
'Fortune, Mr. Charles Alexander',
'Dwyer, Miss. Ellen "Nellie"',
'Todoroff, Mr. Lalio']


# 구현부
m_count = 0

for data in dataset :
  for index in range(len(data)) :
    if data[index] == 'M' :
      m_count += 1

print(m_count)  # 38
```
