---
title: "[Javascript] 정규표현식 메서드, 플래그"
excerpt: 정규표현식 메서드, 플래그
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


<br>

## 2. 정규표현식 플래그(옵션)

플래그 | 설명
--|--
g | 모든 문자 일치(global)
i | 영어 대소문자를 구분 않고 일치(ignore case)
m | 여러 줄 일치(multi line)

```js
const str = `
010-1234-5678
theabc@gmail.com
https://www.omdbapi.com/?apikey=5f6c9466&s=frozen
The quick brown fox jumps over the lazy dog.
abbcccdddd
`
// 플래그 없음
const regexp = /the/
console.log(str.match(regexp))  // ["the", index: 15, input: "\n010-1234-5678\ntheabc@...]

// g
const regexp = /the/g
console.log(str.match(regexp))  // (2) ["the", "the"]

// gi
const regexp = /the/gi
console.log(str.match(regexp))  // (3) ["the", "The", "the"]

console.log(str.match(/the/gi))  // (3) ["the", "The", "the"]

// Escape Character
console.log(str.match(/\./gi))  // (4) [".", ".", ".", "."]

// 끝나는 부분 찾아서 일치시킴
console.log(str.match(/\.$/gi))  // null

// m
console.log(str.match(/\.$/gim))  // ["."]
```