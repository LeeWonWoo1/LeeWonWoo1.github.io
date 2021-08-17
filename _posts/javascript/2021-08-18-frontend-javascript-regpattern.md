---
title: "[Javascript] 정규표현식 패턴"
excerpt: 정규표현식 패턴(표현)
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
date: '2021-08-18T00:00:00'
last_modified_at: 2021-08-18T00:00:00
---

## 정규표현식 패턴(표현)

패턴 | 설명
--|--
^ab | 줄(Line) 시작에 있는 ab와 일치
ab$ | 줄(Line) 끝에 있는 ab와 일치
. | 임의의 한 문자와 일치
a&verbar;b | a 또는 b와 일치
ab? | b가 없거나 b와 일치
{n} | n개 연속 일치
{n,} | n개 이상 연속 일치
{n,m} | n개 이상 m개 이하 연속 일치

```js
const str = `
010-1234-5678
theabc@gmail.com
https://www.omdbapi.com/?apikey=5f6c9466&s=frozen
The quick brown fox jumps over the lazy dog.
abbcccdddd
http://localhost:1234
`

// $ -> 줄(Line) 끝에 있는 ab와 일치
console.log(str.match(/d$/g))  // null
console.log(str.match(/d$/gm))  // ["d"]

// ^ -> 줄(Line) 시작에 있는 ab와 일치
console.log(str.match(/^t/gm))  // ["t"]
console.log(str.match(/^t/gim))  // ["t", "T"]
console.log(str.match(/^T/gm))  // ["T"]

// . -> 임의의 한 문자와 일치
console.log(str.match(/./g))  // (152) ["0", "1", "0", "-", "1", "2", "3", "4", ...]
console.log(str.match(/h..p/g))  // ["http", "http"]

// | -> a 또는 b와 일치
console.log(str.match(/fox|dog/g))  // ["fox", "dog"]

// ? -> b가 없거나 b와 일치
console.log(str.match(/https?/g))  // ["https", "http"]

// {n} -> n개 연속 일치
console.log(str.match(/d{2}/))  // ["dd", index: ...]
console.log(str.match(/d{2}/g))  // ["dd", "dd"]

// {n,} -> n개 이상 연속 일치
console.log(str.match(/d{2,}/g))  // ["dddd"]

// {n,m} -> n개 이상 m개 이하 연속 일치
console.log(str.match(/\w{2,3}/g))  // (36) ["010", "123", "567", "the", "abc", ...]
console.log(str.match(/\b\w{2,3}\b/g))  // (8) ["010", "com", "www", "com", "The", ...]
```
