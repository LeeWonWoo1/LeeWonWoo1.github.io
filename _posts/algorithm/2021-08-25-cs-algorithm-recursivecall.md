---
title: "[Algorithm] 재귀 용법(Recursive Call)"
excerpt: 알고리즘 재귀 호출
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
date: "2021-08-25T02:30:00"
last_modified_at: 2021-08-25T02:30:00
---

## 1. 재귀 용법 (recursive call, 재귀 호출)

- 함수 안에서 동일한 함수를 호출하는 형태
- 여러 알고리즘 작성시 사용

### - 재귀 용법 예제

- 팩토리얼을 구하는 알고리즘을 Recursive Call을 활용해서 알고리즘 작성
- 간단한 경우부터 생각
  - 2! = 1 X 2
  - 3! = 1 X 2 X 3
  - 4! = 1 X 2 X 3 X 4 = 4 X 3!
- 규칙 : n! = n X (n - 1)!
  1. 함수를 만들어 봄
  2. 함수(n) 은 n > 1 이면 return n X 함수(n - 1)
  3. 함수(n) 은 n = 1 이면 return n
- 검증 (코드로 검증하지 않고, 직접 간단한 경우부터 대입해서 검증)
  1. 먼저 2! 부터
     - 함수(2) 이면, 2 > 1 이므로 2 X 함수(1)
     - 함수(1) 은 1 이므로, return 2 X 1 = 2
  2. 먼저 3! 부터
     - 함수(3) 이면, 3 > 1 이므로 3 X 함수(2)
     - 함수(2) 는 결국 1번에 의해 2! 이므로, return 2 X 1 = 2
     - 3 X 함수(2) = 3 X 2 = 3 X 2 X 1 = 6
  3. 먼저 4! 부터
     - 함수(4) 이면, 4 > 1 이므로 4 X 함수(3)
     - 함수(3) 은 결국 2번에 의해 3 X 2 X 1 = 6
     - 4 X 함수(3) = 4 X 6 = 24
- 코드 레벨로 적어보기

```python
def factorial(num) :
    if num > 1 :
        return num * factorial(num - 1)
    else :
        return num


for num in range(10) :
  print(factorial(num))  # 0
                         # 1
                         # 2
                         # 6
                         # ...
                         # 362880
```

<br>

- 시간 복잡도와 공간 복잡도
  - factorial(n) 은 n - 1 번의 factorial() 함수를 호출해서, 곱셈을 함
    - n-1번 반복문을 호출한 것과 동일
    - factorial() 함수를 호출할 때마다, 지역변수 n 이 생성
  - 시간 복잡도/공간 복잡도는 O(n-1) 이므로 결국, 둘 다 O(n)

<br>

### - 재귀 호출의 일반적인 형태

```python
# 일반적인 형태1

def function(입력) :
    if 입력 > 일정값 :  # 입력이 일정 값 이상이면
        return function(입력 - 1)  # 입력보다 작은 값
    else :
        return 일정값, 입력값, 또는 특정값  # 재귀 호출 종료


# ------------------------------------------------------------
# 일반적인 형태2

def function(입력) :
    if 입력 <= 일정값 :  # 입력이 일정 값보다 작으면
        return 일정값, 입력값, 또는 특정값  # 재귀 호출 종료
    function(입력보다 작은 값)
    return 결과값
```

<br>

```python
def factorial(num) :
    if num <= 1 :
        return num
    return_value = num * factorial(num - 1)
    return return_value


for num in range(10) :
    print(factorial(num))  # 0
                           # 1
                           # 2
                           # 6
                           # ...
                           # 362880
```

<br>

- 재귀 호출은 스택의 전형적인 예
  - 함수는 내부적으로 스택처럼 관리

<br>

<img src="https://www.fun-coding.org/00_Images/recursivecall.png" />

- [코드분석](http://pythontutor.com/live.html#code=%23%20factorial%20%ED%95%A8%EC%88%98%20%EC%95%88%EC%97%90%EC%84%9C%20factorial%20%ED%95%A8%EC%88%98%EB%A5%BC%20%ED%98%B8%EC%B6%9C%0Adef%20factorial%28num%29%3A%0A%20%20%20%20if%20num%20%3E%201%3A%0A%20%20%20%20%20%20%20%20return%20num%20*%20factorial%28num%20-%201%29%0A%20%20%20%20else%3A%0A%20%20%20%20%20%20%20%20return%20num%0A%0Afactorial%285%29&cumulative=false&curInstr=22&heapPrimitives=false&mode=display&origin=opt-live.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false){:target="\_blank"}

> 참고: 파이썬에서 재귀 함수는 깊이가(한번에 호출되는) 1000회 이하

<br>

## 2. 재귀 용법을 활용한 프로그래밍 연습

프로그래밍 연습<br>
다음 함수를 재귀 함수를 활용해서 1부터 num까지의 곱이 출력되게 만들기

<pre>
def muliple(data):
    if data <= 1:
        return data
    
    return -------------------------
    
multiple(10)
</pre>

```python
# 단순 반복문
def multiple(num) :
    return_value = 1
    for index in range(1, num+1) :
        return_value = return_value * index
    return return_value


# ------------------------------------------------------------
# 재귀 용법
def multiple(num) :
    if num <= 1 :
        return num
    return num * multiple(num - 1)



multiple(10)  # 3628800
```

<br>

프로그래밍 연습<br>
숫자가 들어 있는 리스트가 주어졌을 때, 리스트의 합을 리턴하는 함수를 만들기 (재귀함수 사용)

<pre>
참고 : 임의 값으로 리스트 만들기 random.sample(0 ~ 99까지 중에서, 임의로 10개를 만들어서 10개 값을 가지는 리스트 변수 만들기
import random 
data = random.sample(range(100), 10)
</pre>

<pre>
def sum_list(data):
    if len(data) == 1:
        return data[0]
    
    return --------------------------------

import random 
data = random.sample(range(100), 10)
print (sum_list(data))
</pre>

```python
import random

data = random.sample(range(100), 10)
print(data)  # [63, 1, 47, 6, 81, 74, 59, 75, 84, 51]

def sum_list(data) :
    if len(data) <= 1 :
        return data[0]
    return data[0] + sum_list(data[1:])


sum_list(data)  # 541
```

<br>

프로그래밍 연습<br>
회문(palindrome)은 순서를 거꾸로 읽어도 제대로 읽은 것과 같은 단어와 문장을 의미<br>
회문을 판별할 수 있는 함수를 재귀함수를 활용해서 만들기
<br>
<img src="https://www.fun-coding.org/00_Images/palindrome.png" width=200/>

<pre>
참고 - 리스트 슬라이싱
string = 'Dave' 
string[-1] --> e
string[0] --> D
string[1:-1] --> av
string[:-1] --> Dav
</pre>

```python
def palindrome(string) :
    if len(string) <= 1 :
        return True
    if string[0] == string[-1] :
        return palindrome(string[1:-1])
    else :
        return False


palindrome('level')  # True
palindrome('love')  # False
```

<br>

프로그래밍 연습<br>

1. 정수 n에 대해<br>
2. n이 홀수이면 3 X n + 1 을 하고,<br>
3. n이 짝수이면 n 을 2로 나눔<br>
4. 이렇게 계속 진행해서 n 이 결국 1이 될 때까지 2와 3의 과정을 반복<br>
   <br>
   예를 들어 n에 3을 넣으면,
   <pre>
   3
   10
   5
   16
   8
   4
   2
   1
   </pre>
   이 됨

이렇게 정수 n을 입력받아, 위 알고리즘에 의해 1이 되는 과정을 모두 출력하는 함수를 작성

```python
def func(n) :
    print(n)
    if n == 1 :
        return n
    if n % 2 == 1 :
        return func((3 * n) + 1)
    else :
        return func(int(n / 2))


func(3)  # 3
         # 10
         # 5
         # 16
         # 8
         # 4
         # 2
         # 1

         # 1
```

<br>

프로그래밍 연습<br>

<pre>
문제: 정수 4를 1, 2, 3의 조합으로 나타내는 방법은 다음과 같이 총 7가지가 있음
1+1+1+1
1+1+2
1+2+1
2+1+1
2+2
1+3
3+1
정수 n이 입력으로 주어졌을 때, n을 1, 2, 3의 합으로 나타낼 수 있는 방법의 수를 구하시오
</pre>

힌트: 정수 n을 만들 수 있는 경우의 수를 리턴하는 함수를 f(n) 이라고 하면,<br>
f(n)은 f(n-1) + f(n-2) + f(n-3) 과 동일하다는 패턴 찾기<br>
출처: ACM-ICPC > Regionals > Asia > Korea > Asia Regional - Taejon 2001<br>

- 문제 분석을 연습장에 작성

<br>

<img src="https://www.fun-coding.org/00_Images/algopractice.jpg" />

```python
def func(data) :
    if data == 1 :
        return 1
    elif data == 2 :
        return 2
    elif data == 3 :
        return 4
    return func(data - 1) + func(data - 2) + func(data - 3)


func(5)  # 13
```
