---
title: "[Javascript] 자료형"
excerpt: String, Number, Boolean, Undefined, Null, Object, Array
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-01T15:00:00'
last_modified_at: 2021-08-01T15:00:00
---

## 1. String

```javascript
// 따옴표 사용
let myName = "LWW";
let email = "plmplmdnjsdn@naver.com";
let hello = `Hello ${myName}!`;

console.log(myName);  // LWW
console.log(email);  // plmplmdnjsdn@naver.com
console.log(hello);  // Hello LWW!
```

<br>

### - String 메서드

자세한 내용은 string mdn 검색
{: .notice--info}

- 기호를 통해서 데이터를 손쉽게 선언하는 방식을 **_리터럴 방식_**이라고 함
- 리터럴 방식이 아니면 new라는 키워드를 사용해야 함

```javascript
// String.prototype.indexOf() -> 찾으려는 문자의 첫 번째 등장 index, 없으면 -1
const result1 = 'Hello world!!'.indexOf('world')
const result2 = 'Hello world!!'.indexOf('king')
console.log(result1)  // 6
console.log(result2)  // -1

const str = 'Hello world!!'
console.log(str.indexOf('king') !== -1)  // false


// .length -> 문자열의 길이 반환
const str = '0123'
console.log(str.length)  // 4
console.log('0123'length)  // 4


// .slice(x, y) -> 문자열을 인덱스 x부터 y-1까지 추출
const str = 'Hello world!'
console.log(str.slice(0, 3))  // Hel
console.log(str.slice(6, 11))  // world


// .replace() -> 문자열 치환
const str = 'Hello world!'
console.log(str.replace('world', 'LWW'))  // Hell LWW!

const str = 'Hello world!'
console.log(str.replace(' world!', ''))  // Hello


// .match() -> 정규표현식을 통해 특정한 문자를 match. 배열데이터로 반환
const str = 'emailaddress@gmail.com'
// 정규표현식
console.log(str.match(/.+(?=@)/)[0])  // emailaddress


// .trim() -> 문자데이터의 앞뒤의 모든 공백문자 제거
const str = '      Hello world     '
console.log(str.trim())  // Hello world
```


<br>

## 2. Number

```javascript
// 정수 및 부동소수점 숫자를 나타냄
let number = 123;
let opacity = 1.57;

console.log(number);  // 123
console.log(opacity);  // 1.57
```

<br>

### - 숫자와 수학

자세한 내용은 math mdn 검색
{: .notice--info}

```javascript
const pi = 3.14159265358979
console.log(pi)  // 3.14159265358979

const str = pi.toFixed(2)
console.log(str)  // 3.14
console.log(typeof str)  // string

const integer = parseInt(str)
const float = parseFloat(str)
console.log(integer)  // 3
console.log(float)  // 3.14
console.log(typeof integer, typeof float)  // number number
```


<br>

```javascript
// Math.abs() -> 절대값 반환
console.log('abs: ', Math.abs(-12))  // abs: 12


// Math.min() -> 최소값 반환
console.log('min: ', Math.min(2, 8))  // min: 2


// Math.max() -> 최대값 반환
console.log('max: ', Math.max(2, 8))  // max: 8


// Math.ceil() -> 올림
console.log('ceil: ', Math.ceil(3.14))  // ceil: 4


// Math.floor() -> 내림
console.log('floor: ', Math.floor(3.14))  // floor: 3


// Math.round() -> 반올림
console.log('round: ', Math.round(3.5))  // round: 4


// Math.random() -> 난수
console.log('random: ',Math.random())  // random: 0~1사이의 난수
```


<br>

## 3. Boolean

```javascript
// true, false 두 가지 값밖에 없는 논리 데이터
let checked = true;
let isShow = false;

console.log(checked);  // true
console.log(isShow);  // false
```


<br>

## 4. Undefined

```javascript
// 값이 할당되지 않은 상태를 나타냄
let undef;
let obj = {abc: 123};

console.log(undef);  // undefined
console.log(obj.abc);  // 123
console.log(obj.xyz);  // undefined
```


<br>

## 5. Null

```javascript
// 어떤 값이 의도적으로 비어있음을 의미
let empty = null;

console.log(empty);  // null
```


<br>

## 6. Object

```javascript
// 여러 데이터를 Key:Value 형태로 저장 { }
let user = {
  name: 'LWW',
  age: 50,
  isValid: true
};

console.log(user.name);  // LWW
console.log(user.age);  // 50
console.log(user.isValid);  // true
```

<br>

### - Object 메서드

자세한 내용은 object mdn 검색
{: .notice--info}

```javascript
// .assign(x, y) -> x 객체 데이터에 y 객체 데이터를 합침
// static 메서드
const userAge = {
  // key: value
  name: 'LWW',
  age: 45
}
const userEmail = {
  name: 'LWW',
  email: 'abcdefg@gmail.com'
}

// 프로토타입으로 만들어진 메서드가 아니기 때문에 객체 데이터 자체에는 사용 불가
// ex) userAge.assign와 같은 식으로 사용불가
const target = Object.assign(userAge, userEmail)
console.log(target)  // {name: "LWW", age: 45, email: "abcdefg@gmail.com"}
console.log(userAge)  // {name: "LWW", age: 45, email: "abcdefg@gmail.com"}
console.log(target === userAge)  // true

// 서로 다른 메모리 주소를 가리키고 있음
const a = {k: 123}
const b = {k: 123}
console.log(a === b)  // false

// 원본 데이터 손상 안주는 방법
const target = Object.assign({}, userAge, userEmail)
console.log(target)  // {name: "LWW", age: 45, email: "abcdefg@gmail.com"}
console.log(userAge)  // {name: "LWW", age: 45}
console.log(target === userAge)  // false

// 복사본 만들기
const target = Object.assign({}, userAge)
console.log(target)  // {name: "LWW", age: 45}
console.log(userAge)  // {name: "LWW", age: 45}
console.log(target === userAge)  // false
```


<br>

## 7. Array

```javascript
// 여러 데이터를 순차적으로 저장 [ ]
let animals = ['Cat', 'Dog', 'Tiger'];

console.log(animals[0]);  // 'Cat'
console.log(animals[1]);  // 'Dog'
console.log(animals[2]);  // 'Tiger'
```

<br>

### - Array indexing

자세한 내용은 array mdn 검색
{: .notice--info}

```javascript
// 각각의 요소는 element(요소), item이라고 부름
const numbers = [1, 2, 3, 4]
const animals = ['Cat', 'Dog', 'Tiger']

console.log(numbers[1])  // 2
console.log(fruits[2])  // 'Tiger'
```

<br>

### - Array 메서드

```javascript
// .length -> 배열의 길이 반환
const numbers = [1, 2, 3, 4]
const animals = ['Cat', 'Dog', 'Tiger']

console.log(numbers.length)  // 4
console.log(animals.length)  // 3
console.log([1, 2].length)  // 2
console.log([].length)  // 0


// .concat() -> 두 개의 배열 데이터를 병합해서 새로운 배열 데이터 반환
// 원본 데이터는 변하지 않음
const numbers = [1, 2, 3, 4]
const animals = ['Cat', 'Dog', 'Tiger']

console.log(numbers.concat(animals))  // 0: 1
                                      // 1: 2
                                      // 2: 3
                                      // ....
                                      // 5: "Dog"
                                      // 6: "Tiger"
console.log(numbers)  // (4) [1, 2, 3, 4]
console.log(animals)  // (3) ["Cat", "Dog", "Tiger"]


// .forEach() -> 배열의 item 개수만큼 인수로 사용된 콜백함수가 반복적으로 실행
const numbers = [1, 2, 3, 4]
const animals = ['Cat', 'Dog', 'Tiger']

animals.forEach(function (animal, i) {
  console.log(animal, i)  // Cat 0 (3) ["Cat", "Dog", "Tiger"]
})                        // Dog 1 (3) ["Cat", "Dog", "Tiger"]
                          // Tiger 2 (3) ["Cat", "Dog", "Tiger"]


// .map() -> 콜백에서 반환된 특정한 데이터를 기준으로 해서 새로운 배열 반환
const numbers = [1, 2, 3, 4]
const animals = ['Cat', 'Dog', 'Tiger']

const a = animals.forEach(function (animal, index) {
  console.log(`${animal}-${i}`) // Cat-0
})                              // Dog-1
                                // Tiger-2
console.log(a)  // Undefined, 반환값 없음

const b = animals.map(function (animal, index) {
  return `${animal}-${i}`
})
console.log(b) // (3) ["Cat-0", "Dog-1", "Tiger-2"]

const c = animals.map(function (animal, index) {
  return {
    id: index,
    name: animal
  }
})
console.log(c)  // (3) [{...}, {...}, {...}]

const d = animals.map((animal, index) => ({
  id: index,
  name: animal
}))
console.log(d)  // (3) [{...}, {...}, {...}]


// .filter() -> 콜백 함수에서 반환된 값이 true인 경우에만 새로운 배열로 반환
const numbers = [1, 2, 3, 4]

const a = numbers.map(number => number < 3)
console.log(a)  // (4) [true, true, false, false]

const b = numbers.filter(number => number < 3)
console.log(b)  // (2) [1, 2]
console.log(numbers)  // (4) [1, 2, 3, 4]


// .find() -> 내가 원하는 특정한 데이터를 찾음
// 아이템을 찾으면 반복 종료
const animals = ['Cat', 'Dog', 'Tiger']

const a = animals.find(animal => /^D/.test(animal))
const b = animals.find(animal => /^T/.test(animal))
console.log(a)  // Dog
console.log(b)  // Tiger


// .findIndex() -> 내가 원하는 특정한 데이터의 인덱스를 찾음
const animals = ['Cat', 'Dog', 'Tiger']

const a = animals.findIndex(animal => /^D/.test(animal))
console.log(a)  // 1


// .includes() -> 배열의 인수로 사용된 특정한 데이터가 포함되어 있는지 확인
const numbers = [1, 2, 3, 4]
const animals = ['Cat', 'Dog', 'Tiger']

const a = numbers.includes(3)
console.log(a)  // true

const b = animals.includes('LWW')
console.log(b)  // false


// .push() -> 배열의 가장 뒤쪽에 새로운 데이터 삽입
// .unshift() -> 배열의 가장 앞쪽에 새로운 데이터 삽입
// 원본 수정됨 주의!
const numbers = [1, 2, 3, 4]

numbers.push(5)
console.log(numbers)  // (5) [1, 2, 3, 4, 5]
numbers.unshift(0)
console.log(numbers)  // (6) [0, 1, 2, 3, 4, 5]


// .reverse() -> 배열의 요소 순서를 뒤집음
// 원본 수정됨 주의!
const numbers = [1, 2, 3, 4]
const animals = ['Cat', 'Dog', 'Tiger']

numbers.reverse()
animals.reverse()

console.log(numbers)  // (4) [4, 3, 2, 1]
console.log(animals)  // (3) ["tiger", "Dog", "Cat"]


// .splice(x, y) -> 인덱스 x에서 y개의 배열 요소를 삭제
// 원본 수정됨 주의!
// 어떤 자리에 새로운 요소를 끼워 넣는 용도로도 사용
const numbers = [1, 2, 3, 4]

numbers.splice(2, 2)
console.log(numbers)  // (3) [1, 2]

const numbers = [1, 2, 3, 4]

numbers.splice(2, 0, 999)
console.log(numbers)  // (5) [1, 2, 999, 3, 4]

const animals = ['Cat', 'Dog', 'Tiger']

animals.splice(2, 1, 'Lion')
console.log(animals)  // (3) ["Cat", "Lion", "Tiger"]
```