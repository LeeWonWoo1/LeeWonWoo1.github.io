---
title: "[Data Structure] 해시 테이블(Hash Table)"
excerpt: 자료구조 해시 테이블
categories:
- DS
tags:
- - DS
  - CS
  - Programming
toc: true
toc_sticky: true
popular: true
date: '2021-08-21T04:00:00'
last_modified_at: 2021-08-21T04:00:00
---

## 1. 해시 테이블 (Hash Table)


### - 해시 구조

* Hash Table: 키(Key)에 데이터(Value)를 저장하는 데이터 구조
    - Key를 통해 바로 데이터를 받아올 수 있으므로, 속도가 획기적으로 빨라짐
    - 파이썬 Dictionary 타입이 해쉬 테이블의 예 : Key를 가지고 바로 데이터(Value)를 꺼냄
    - 보통 배열로 미리 Hash Table 사이즈만큼 생성 후에 사용 (공간과 탐색 시간을 맞바꾸는 기법)
    - 단, 파이썬에서는 해시를 별도 구현할 이유가 없음 - 딕셔너리 타입을 사용하면 됨


### - 알아둘 용어

* 해시(Hash): 임의 값을 고정 길이로 변환하는 것
* 해시 테이블(Hash Table): 키 값의 연산에 의해 직접 접근이 가능한 데이터 구조
* 해싱 함수(Hashing Function): Key에 대해 산술 연산을 이용해 데이터 위치를 찾을 수 있는 함수
* 해시 값(Hash Value) / 해시 주소(Hash Address): Key를 해싱 함수로 연산해서, 해시 값을 알아내고, 이를 기반으로 해시 테이블에서 해당 Key에 대한 데이터 위치를 일관성있게 찾을 수 있음
* 슬롯(Slot): 한 개의 데이터를 저장할 수 있는 공간
* 저장할 데이터에 대해 Key를 추출할 수 있는 별도 함수도 존재할 수 있음

<br>

<img src="https://www.fun-coding.org/00_Images/hash.png" width=400 />

<br>

### - 간단한 해시 예

#### @1. hash table 만들기

- 참고 : 파이썬 list comprehension - https://www.fun-coding.org/PL&OOP5-2.html

```python
hash_table = list(0 for i in range(10))
hash_table  # [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```

<br>

#### @2. 간단한 해시 함수 만들기

- 다양한 해시 함수 고안 기법이 있으며, 가장 간단한 방식이 Division 법 
- Division 법 : 나누기를 통한 나머지 값을 사용하는 기법

```python
def hash_func(key) :
  return key % 5
```

<br>

#### @3. 해시 테이블에 저장

- 데이터에 따라 필요시 key 생성 방법 정의가 필요

```python
data1 = 'Andy'
data2 = 'Dave'
data3 = 'Trump'
data4 = 'Anthor'

# ord() -> 문자의 ASCII(아스키)코드 리턴
print(ord(data1[0]), ord(data2[0]), ord(data3[0]))  # 65 68 84
print(ord(data1[0]), hash_func(ord(data1[0])))  # 65 0
print(ord(data1[0]), ord(data4[0]))  # 65 65
```

<br>

- 해시 테이블에 값 저장 예
    - data:value 와 같이 data 와 value를 넣으면, 해당 data에 대한 key를 찾아서, 해당 key에 대응하는 해시주소에 value를 저장하는 예

```python
def storage_data(data, value) :
  key = ord(data[0])
  hash_address = hash_func(key)
  hash_table[hash_address] = value
```

<br>

#### @4. 해시 테이블에서 특정 주소의 데이터를 가져오는 함수 만들기

```python
storage_data('Andy', '01055553333')
storage_data('Dave', '01044443333')
storage_data('Trump', '01022223333')
```

<br>

#### @5. 실제 데이터를 저장하고, 읽기

```python
def get_data(data) :
  key = ord(data[0])
  hash_address = hash_func(key)
  return hash_table[hash_address]

get_data('Andy')  # 01055553333
```


<br>

### - 해시 테이블의 장단점과 주요 용도

- 장점
    - 데이터 저장/읽기 속도가 빠름 (검색 속도 빠름)
    - 해시는 키에 대한 데이터가 있는지(중복) 확인이 쉬움
- 단점 
    - 일반적으로 저장공간이 좀더 많이 필요
    - **여러 키에 해당하는 주소가 동일할 경우 충돌을 해결하기 위한 별도 자료구조가 필요**
- 주요 용도
    - 검색이 많이 필요한 경우
    - 저장, 삭제, 읽기가 빈번한 경우
    - 캐시 구현시 (중복 확인이 쉽기 때문)


<br>

## 2. 프로그래밍 연습

연습1 : 리스트 변수를 활용해서 해시 테이블 구현<br>
1. 해시 함수 : key % 8
2. 해시 키 생성 : hash(data)

```python
hash_table = list([0 for i in range(8)])

def get_key(data) :
  return hash(data)

def hash_function(key) :
  return key % 8

def save_data(data, value) :
  hash_address = hash_function(get_key(data))
  hash_table[hash_address] = value
    
def read_data(data) :
  hash_address = hash_function(get_key(data))
  return hash_table[hash_address]


# 테스트
save_data('Dave', '0102030200')
save_data('Andy', '01033232200')
read_data('Dave')  # 0102030200

hash_table  # [0, 0, 0, 0, 0, '0102030200', 0, '01033232200']
```


<br>

## 3. 충돌(Collision) 해결 알고리즘

- 좋은 해시 함수 사용
- 해시 테이블의 가장 큰 문제는 충돌(Collision)
- 이 문제를 충돌(Collision) 또는 해시 충돌(Hash Collision)이라고 부름


### - Chaining 기법

- **개방 해싱 또는 Open Hashing 기법** 중 하나 : 해시 테이블 저장공간 외의 공간을 활용
- 충돌이 일어나면 링크드 리스트를 사용해서 데이터를 추가로 뒤에 연결시켜 저장

연습2 : 연습1의 해쉬 테이블 코드에 Chaining 기법으로 충돌해결 코드를 추가<br>
1. 해쉬 함수: key % 8
2. 해쉬 키 생성: hash(data)

```python
hash_table = list([0 for i in range(8)])

def get_key(data) :
  return hash(data)

def hash_function(key) :
  return key % 8

def save_data(data, value) :
  index_key = get_key(data)
  hash_address = hash_function(index_key)
  if hash_table[hash_address] != 0 :
    for index in range(len(hash_table[hash_address])) :
      if hash_table[hash_address][index][0] == index_key :
        hash_table[hash_address][index][1] = value
        return
    hash_table[hash_address].append([index_key, value])
  else :
    hash_table[hash_address] = [[index_key, value]]
    
def read_data(data) :
  index_key = get_key(data)
  hash_address = hash_function(index_key)
  if hash_table[hash_address] != 0 :
    for index in range(len(hash_table[hash_address])):
      if hash_table[hash_address][index][0] == index_key :
        return hash_table[hash_address][index][1]
    return None
  else :
    return None


# 테스트(매번 다름)
print(hash('Dave') % 8)  # 5
print(hash('Df') % 8)  # 0
print(hash('Data') % 8)  # 0

save_data('Df', '1201023010')
save_data('Data', '3301023010')
read_data('Df')  # '1201023010'

hash_table  # [[[6824493835692342864, '1201023010'], [1504471460684481160, '3301023010']],
            # 0,
            # 0,
            # 0,
            # 0,
            # 0,
            # 0,
            # 0]
```


<br>

### - Linear Probing 기법

- **폐쇄 해싱 또는 Close Hashing 기법** 중 하나: 해시 테이블 저장공간 안에서 충돌 문제를 해결
- 충돌이 일어나면, 해당 hash address의 다음 address부터 맨 처음 나오는 빈공간에 저장
- 저장공간 활용도를 높이기 위한 기법

연습3 : 연습1의 해시 테이블 코드에 Linear Probling 기법으로 충돌해결 코드를 추가<br>
1. 해시 함수: key % 8
2. 해시 키 생성: hash(data)

```python
hash_table = list([0 for i in range(8)])

def get_key(data) :
  return hash(data)

def hash_function(key) :
  return key % 8

def save_data(data, value) :
  index_key = get_key(data)
  hash_address = hash_function(index_key)
  if hash_table[hash_address] != 0 :
    for index in range(hash_address, len(hash_table)) :
      if hash_table[index] == 0 :
        hash_table[index] = [index_key, value]
        return
      elif hash_table[index][0] == index_key :
        hash_table[index][1] = value
        return
  else :
    hash_table[hash_address] = [index_key, value]

def read_data(data) :
  index_key = get_key(data)
  hash_address = hash_function(index_key)
  if hash_table[hash_address] != 0 :
    for index in range(hash_address, len(hash_table)) :
      if hash_table[index] == 0 :
        return None
      elif hash_table[index][0] == index_key :
        return hash_table[index][1]
  else :
    return None


# 테스트(매번 다름)
print(hash('ds') % 8)  # 3
print(hash('db') % 8)  # 3
print(hash('dg') % 8)  # 3

save_data('ds', '01200123123')
save_data('db', '3333333333')
read_data('ds')  # '01200123123'
```


<br>

### - 빈번한 충돌을 개선하는 기법

- 해시 함수을 재정의 및 해시 테이블 저장공간을 확대

```python
hash_table = list([None for i in range(16)])

def hash_function(key):
  return key % 16
```


<br>

## 4. 해시 함수와 키 생성 함수

- 파이썬의 hash() 함수는 실행할 때마다, 값이 달라질 수 있음
- 유명한 해시 함수 : SHA(Secure Hash Algorithm, 안전한 해시 알고리즘)
    - 어떤 데이터도 유일한 고정된 크기의 고정값을 리턴, 해쉬 함수로 유용하게 활용 가능


### - SHA-1

```python
import hashlib

data = 'test'.encode()
hash_object = hashlib.sha1()
hash_object.update(data)
hex_dig = hash_object.hexdigest()

print(hex_dig)  # a94a8fe5ccb19ba61c4c0873d391e987982fbbd3
```


<br>

### - SHA-256

```python
import hashlib

data = 'test'.encode()
hash_object = hashlib.sha256()
hash_object.update(data)
hex_dig = hash_object.hexdigest()

print(hex_dig)  # 9f86d081884c7d659a2feaa0c55ad015a3bf4f1b2b0b822cd15d6c15b0f00a08
```


<br>

## 5. 프로그래밍 연습

연습4 : 연습2의 Chaining 기법을 적용한 해시 테이블 코드에 키 생성 함수를 sha256를 사용하도록 변경<br>
1. 해시 함수 : key % 8
2. 해시 키 생성 : hash(data)

```python
import hashlib

hash_table = list([0 for i in range(8)])

def get_key(data) :
  hash_object = hashlib.sha256()
  hash_object.update(data.encode())
  hex_dig = hash_object.hexdigest()
  return int(hex_dig, 16)

def hash_function(key) :
  return key % 8

def save_data(data, value) :
  index_key = get_key(data)
  hash_address = hash_function(index_key)
  if hash_table[hash_address] != 0 :
    for index in range(hash_address, len(hash_table)) :
      if hash_table[index] == 0 :
        hash_table[index] = [index_key, value]
        return
      elif hash_table[index][0] == index_key :
        hash_table[index][1] = value
        return
  else :
    hash_table[hash_address] = [index_key, value]

def read_data(data) :
  index_key = get_key(data)
  hash_address = hash_function(index_key)
  if hash_table[hash_address] != 0 :
    for index in range(hash_address, len(hash_table)) :
      if hash_table[index] == 0 :
        return None
      elif hash_table[index][0] == index_key :
        return hash_table[index][1]
  else :
    return None


# 테스트
print(get_key('db') % 8)  # 1
print(get_key('da') % 8)  # 2
print(get_key('dh') % 8)  # 2

save_data('da', '01200123123')
save_data('dh', '3333333333')
read_data('dh')  # '3333333333'
```


<br>

## 6. 시간 복잡도

- 일반적인 경우(Collision이 없는 경우)는 **O(1)**
- 최악의 경우(Collision이 모두 발생하는 경우)는 **O(n)**

> 해시 테이블의 경우, 일반적인 경우를 기대하고 만들기 때문에, O(1)라고 말할 수 있음


### 검색에서 해시 테이블의 사용 예

- 16개의 배열에 데이터를 저장하고, 검색할 때 **O(n)**
- 16개의 데이터 저장공간을 가진 위의 해시 테이블에 데이터를 저장하고, 검색할 때 **O(1)**