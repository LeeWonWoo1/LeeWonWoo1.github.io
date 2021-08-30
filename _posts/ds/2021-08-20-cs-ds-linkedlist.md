---
title: "[Data Structure] 링크드 리스트(Linked List)"
excerpt: 자료구조 링크드 리스트
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
date: "2021-08-20T03:00:00"
last_modified_at: 2021-08-20T03:00:00
---

## 1. 링크드 리스트 (Linked List)

### - 링크드 리스트 (Linked List) 구조

- 연결 리스트라고도 함
- 배열은 순차적으로 연결된 공간에 데이터를 나열하는 데이터 구조
- 링크드 리스트는 떨어진 곳에 존재하는 데이터를 화살표로 연결해서 관리하는 데이터 구조
- C언어에서는 주요한 데이터 구조이지만, 파이썬은 리스트 타입이 링크드 리스트의 기능을 모두 지원
- 링크드 리스트 기본 구조와 용어
  - 노드(Node): 데이터 저장 단위 (데이터값, 포인터) 로 구성
  - 포인터(pointer): 각 노드 안에서, 다음이나 이전의 노드와의 연결 정보를 가지고 있는 공간
- 일반적인 링크드 리스트 형태

<br>

<img src="https://www.fun-coding.org/00_Images/linkedlist.png" />

<br>

(출처: wikipedia, https://en.wikipedia.org/wiki/Linked_list)

### - 간단한 링크드 리스트 예시

#### @ Node 구현

- 보통 파이썬에서 링크드 리스트 구현시, 파이썬 클래스를 활용함
  - 파이썬 객체지향 문법 이해 필요
  - 참고: [https://www.fun-coding.org/PL&OOP1-3.html](https://www.fun-coding.org/PL&OOP1-3.html)

```python
# 1
class Node :
  def __init__(self, data) :
    self.data = data
    self.next = None

# 2
class Node :
  def __init__(self, data, next=None) :
    self.data = data
    self.next = next
```

<br>

#### @ Node와 Node 연결하기 (포인터 활용)

```python
node1 = Node(1)
node2 = Node(2)
node1.next = node2
head = node1
```

<br>

#### @ 링크드 리스트로 데이터 추가하기

```python
class Node :
  def __init__(self, data, next=None) :
    self.data = data
    self.next = next

  def add(data) :
    node = head
    while node.next :
      node = node.next
    node.next = Node(data)

node1 = Node(1)
head = node1

for index in range(2, 10) :
  add(index)
```

<br>

#### @ 링크드 리스트 데이터 출력하기(검색하기)

```python
node = head
while node.next :
  print(node.data)
  node = node.next

print(node.data)  # 1
                  # 2
                  # 3
                  # ...
                  # 9
```

<br>

### - 링크드 리스트의 장단점 (전통적인 C언어에서의 배열과 링크드 리스트)

- 장점
  - 미리 데이터 공간을 미리 할당하지 않아도 됨
    - 배열은 **미리 데이터 공간을 할당** 해야 함
- 단점
  - 연결을 위한 별도 데이터 공간이 필요하므로, 저장공간 효율이 높지 않음
  - 연결 정보를 찾는 시간이 필요하므로 접근 속도가 느림
  - 중간 데이터 삭제시, 앞뒤 데이터의 연결을 재구성해야 하는 부가적인 작업 필요

### - 링크드 리스트의 복잡한 기능1 (링크드 리스트 데이터 사이에 데이터를 추가)

- 링크드 리스트는 유지 관리에 부가적인 구현이 필요함

<br>

<img src="https://www.fun-coding.org/00_Images/linkedlistadd.png" />

<br>

(출처: wikipedia, https://en.wikipedia.org/wiki/Linked_list)

```python
node = head
while node.next :
  print(node.data)
  node = node.next

print(node.data)  # 1
                  # 2
                  # 3
                  # ...
                  # 9

node3 = Node(1.5)

node = head
search = True
while search :
  if node.data == 1 :
    search = False
  else :
    node = node.next

node_next = node.next
node.next = node3
node3.next = node_next

node = head
while node.next:
    print(node.data)
    node = node.next

print (node.data)  # 1
                   # 1.5
                   # 2
                   # 3
                   # ...
                   # 9
```

<br>

### - 파이썬 객체지향 프로그래밍으로 링크드 리스트 구현하기

```python
class Node :
  def __init__(self, data, next=None) :
    self.data = data
    self.next = next

class NodeMgmt :
  def __init__(self, data) :
    self.head = Node(data)

  def add(self, data) :
    if self.head == '' :
      self.head = Node(data)
    else :
      node = self.head
      while node.next :
        node = node.next
      node.next = Node(data)

  def desc(self) :
    node = self.head
    while node :
      print(node.data)
      node = node.next

linked_list1 = NodeMgmt(0)
linked_list1.desc()  # 0

for data in range(1, 10) :
  linked_list1.add(data)

linked_list1.desc()  # 0
                     # 1
                     # 2
                     # ...
                     # 9
```

<br>

### - 링크드 리스트의 복잡한 기능2 (특정 노드를 삭제)

- 다음 코드는 위의 코드에서 delete 메서드만 추가한 것이므로 해당 메서드만 확인

```python
class Node :
  def __init__(self, data, next=None) :
    self.data = data
    self.next = next

class NodeMgmt :
  def __init__(self, data) :
    self.head = Node(data)

  def add(self, data) :
    if self.head == '' :
      self.head = Node(data)
    else :
      node = self.head
      while node.next :
        node = node.next
      node.next = Node(data)

  def desc(self) :
    node = self.head
    while node :
      print(node.data)
      node = node.next

  def delete(self, data) :
    if self.head == '' :
      print('해당 값을 가진 노드가 없습니다.')
      return
    # head 삭제
    if self.head.data == data :
      temp = self.head
      self.head = self.head.next
      del temp
    else :
      node = self.head
      while node.next :
        # 중간, 끝 노드 삭제
        if node.next.data == data :
          temp = node.next
          node.next = node.next.next
          del temp
          return
        else :
          node = node.next

# 테스트를 위해 1개 노드를 만들어 봄
linked_list1 = NodeMgmt(0)
linked_list1.desc()  # 0

# head가 살아있음을 확인
linked_list1.head  # <__main__.Node at 0x...>

# head를 지워봄
linked_list1.delete(0)

# linked_list1.head가 삭제됨
linked_list1.head  # 출력 없음

# 다시 하나의 노드를 만들어 봄
linked_list1 = NodeMgmt(0)
linked_list1.desc()  # 0

# 여러 노드를 추가해 봄
for data in range(1, 10) :
  linked_list1.add(data)

linked_list1.desc()  # 0
                     # 1
                     # 2
                     # ...
                     # 9

# 노드 중에 한개를 삭제
linked_list1.delete(4)
linked_list1.desc()  # 0
                     # 1
                     # 2
                     # 3
                     # 5
                     # ...
                     # 9

linked_list1.delete(9)
linked_list1.desc()  # 0
                     # 1
                     # 2
                     # 3
                     # 5
                     # ...
                     # 8
```

<br>

## 2. 프로그래밍 연습

```python
# 연습1: 위 코드에서 노드 데이터가 특정 숫자인 노드를 찾는 함수를 만들고, 테스트해보기
# 테스트: 임의로 1 ~ 9까지 데이터를 링크드 리스트에 넣어보고, 데이터 값이 4인 노드의 데이터 값 출력해보기

class Node :
  def __init__(self, data) :
    self.data = data
    self.next = None

class NodeMgmt :
  def __init__(self, data) :
    self.head = Node(data)

  def add(self, data) :
    if self.head == '' :
      self.head = Node(data)
    else :
      node = self.head
      while node.next :
        node = node.next
      node.next = Node(data)

  def desc(self) :
    node = self.head
    while node :
      print(node.data)
      node = node.next

  def delete(self, data) :
    if self.head == '' :
      print('해당 값을 가진 노드가 없습니다.')
      return
    # self.head를 삭제해야할 경우 - self.head를 바꿔줘야 함
    if self.head.data == data :
      temp = self.head  # self.head 객체를 삭제하기 위해, 임시로 temp에 담아서 객체를 삭제
      self.head = self.head.next  # self.head 객체를 삭제하면, 이 코드가 실행이 안됨
      del temp
    else :
      node = self.head
      while node.next :
        # self.head가 아닌 노드를 삭제해야할 경우
        if node.next.data == data :
          temp = node.next
          node.next = node.next.next
          del temp
          pass
        else :
          node = node.next

  # 노드를 찾는 함수
  def search_node(self, data) :
    node = self.head
    while node :
      if node.data == data :
        return data
      else :
        node = node.next

# 테스트
linked_list2 = NodeMgmt(0)

for data in range(1, 10) :
  linked_list2.add(data)

node = linked_list2.search_node(4)
print(node.data)  # 4
```

<br>

## 3. 다양한 링크드 리스트 구조

- 더블 링크드 리스트(Doubly linked list) 기본 구조
  - 이중 연결 리스트라고도 함
  - 장점: 양방향으로 연결되어 있어서 노드 탐색이 양쪽으로 모두 가능

<br>

<img src="https://www.fun-coding.org/00_Images/doublelinkedlist.png" />

<br>

(출처: wikipedia, https://en.wikipedia.org/wiki/Linked_list)

```python
class Node :
  def __init__(self, data, prev=None, next=None) :
    self.prev = prev
    self.data = data
    self.next = next

class NodeMgmt :
  def __init__(self, data) :
    self.head = Node(data)
    self.tail = self.head

  def insert(self, data) :
    if self.head == None :
      self.head = Node(data)
      self.tail = self.head
    else :
      node = self.head
      while node.next :
        node = node.next
      new = Node(data)
      node.next = new
      new.prev = node
      self.tail = new

  def desc(self) :
    node = self.head
    while node :
      print(node.data)
      node = node.next

# 테스트
double_linked_list = NodeMgmt(0)

for data in range(1, 10) :
  double_linked_list.insert(data)

double_linked_list.desc()  # 0
                           # 1
                           # 2
                           # ...
                           # 9
```

<br>

## 4. 프로그래밍 연습

```python
# 연습2: 위 코드에서 노드 데이터가 특정 숫자인 노드 앞에 데이터를 추가하는 함수를 만들고, 테스트
# 더블 링크드 리스트의 tail 에서부터 뒤로 이동하며, 특정 숫자인 노드를 찾는 방식으로 함수를 구현하기
# 테스트: 임의로 0 ~ 9까지 데이터를 링크드 리스트에 넣어보고, 데이터 값이 2인 노드 앞에 1.5 데이터 값을 가진 노드를 추가해보기

class Node :
  def __init__(self, data, prev=None, next=None) :
    self.prev = prev
    self.data = data
    self.next = next

class NodeMgmt :
  def __init__(self, data) :
    self.head = Node(data)
    self.tail = self.head

  def insert(self, data) :
    if self.head == None :
      self.head = Node(data)
      self.tail = self.head
    else :
      node = self.head
      while node.next :
        node = node.next
      new = Node(data)
      node.next = new
      new.prev = node
      self.tail = new

  def desc(self) :
    node = self.head
    while node :
      print(node.data)
      node = node.next

  def search_from_head(self, data) :
    if self.head == None :
      return False
    node = self.head
    while node :
      if node.data == data :
        return node
      else :
        node = node.next
    return False

  def search_from_tail(self, data) :
    if self.head == None :
      return False
    node = self.tail
    while node :
      if node.data == data :
        return node
      else :
        node = node.prev
    return False

  def insert_before(self, data, before_data) :
    if self.head == None :
      self.head = Node(data)
      return True
    else :
      node = self.tail
      while node.data != before_data :
        node = node.prev
        if node == None :
          return False
      new = Node(data)
      before_new = node.prev
      before_new.next = new
      new.prev = before_new
      new.next = node
      node.prev = new
      return True

# 테스트
double_linked_list = NodeMgmt(0)

for data in range(1, 10):
    double_linked_list.insert(data)

double_linked_list.desc()  # 0
                           # 1
                           # 2
                           # ...
                           # 9

node_3 = double_linked_list.search_from_tail(3)
node_3.data  # 3

double_linked_list.insert_before(1.5, 2)
double_linked_list.desc()  # 0
                           # 1
                           # 1.5
                           # 2
                           # ...
                           # 9

node_3 = double_linked_list.search_from_tail(1.5)
node_3.data  # 1.5
```

<br>

```python
# 연습4: 위 코드에서 노드 데이터가 특정 숫자인 노드 뒤에 데이터를 추가하는 함수를 만들고, 테스트해보기
# 더블 링크드 리스트의 head 에서부터 다음으로 이동하며, 특정 숫자인 노드를 찾는 방식으로 함수를 구현하기
# 테스트: 임의로 0 ~ 9까지 데이터를 링크드 리스트에 넣어보고, 데이터 값이 1인 노드 다음에 1.7 데이터 값을 가진 노드를 추가해보기

class Node :
  def __init__(self, data, prev=None, next=None):
    self.prev = prev
    self.data = data
    self.next = next

class NodeMgmt :
  def __init__(self, data) :
    self.head = Node(data)
    self.tail = self.head

  def insert_before(self, data, before_data) :
    if self.head == None :
      self.head = Node(data)
      return True
    else :
      node = self.tail
      while node.data != before_data :
        node = node.prev
        if node == None :
          return False
      new = Node(data)
      before_new = node.prev
      before_new.next = new
      new.next = node
      return True

  def insert_after(self, data, after_data) :
    if self.head == None :
      self.head = Node(data)
      return True
    else :
      node = self.head
      while node.data != after_data :
        node = node.next
        if node == None :
          return False
      new = Node(data)
      after_new = node.next
      new.next = after_new
      new.prev = node
      node.next = new
      if new.next == None :
        self.tail = new
      return True

  def insert(self, data) :
    if self.head == None :
      self.head = Node(data)
    else :
      node = self.head
      while node.next :
        new = Node(data)
      new = Node(data)
      node.next = new
      new.prev = node
      self.tail = new

  def desc(self) :
    node = self.head
    while node :
      print(node.data)
      node = node.next

# 테스트
double_linked_list = NodeMgmt(0)

for data in range(1, 10) :
  double_linked_list.insert(data)

double_linked_list.desc()  # 0
                           # 1
                           # 2
                           # ...
                           # 9

double_linked_list.insert_after(1.5, 1)

double_linked_list.desc()  # 0
                           # 1
                           # 1.5
                           # 2
                           # ...
                           # 9
```
