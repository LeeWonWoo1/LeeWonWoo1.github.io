---
title: "[Javascript] 정규표현식 메서드"
excerpt: 정규표현식 메서드
categories:
- Javascript
tags:
- - Javascript
  - Programming
  - Web
  - Reg
toc: true
toc_sticky: true
popular: true
date: '2021-08-17T19:00:00'
last_modified_at: 2021-08-17T19:00:00
---

## 1. 정규표현식 메서드

메서드 | 문법 | 설명
--|--|--
exec | `정규식.exec(문자열)` | 일치하는 하나의 정보(Array) 반환
test | `정규식.test(문자열)` | 일치 여부(Boolean) 반환
match | `문자열.match(정규식)` | 일치하는 문자열의 배열(Array) 반환
search | `문자열.search(정규식)` | 일치하는 문자열의 인덱스(Number) 반환
replace | `문자열.replace(정규식, 대체문자)` | 일치하는 문자열을 대체하고 문자열(String) 반환
split | `문자열.split(정규식)` | 일치하는 문자열을 분할하여 배열(Array)로 반환
toString | `생성자_정규식.toString()` | 생성자 함수 방식의 정규식을 리터럴 방식의 문자열(String)로 반환

<br>

```js
const str = `
010-1234-5678
theabc@gmail.com
https://www.omdbapi.com/?apikey=5f6c9466&s=frozen
The quick brown fox jumps over the lazy dog.
abbcccdddd
`

// test
const regexp = /fox/gi
console.log(regexp.test(str))  // true

const regexp = /LWW/gi
console.log(regexp.test(str))  // false

// replace
const regexp = /fox/gi
console.log(str.replace(regexp, 'AAA'))  // The quick bronw AAA ...
console.log(str)  // The quick brown fox ...

let str = `
The quick brown fox jumps over the lazy dog.
`
const regexp = /fox/gi
str = str.replace(regexp, 'AAA')
console.log(str)  // The quick brown AAA ...
```