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
[abc] | a 또는 b 또는 c
[a-z] | a부터 z 사이의 문자 구간에 일치(소문자)
[A-Z] | A부터 Z 사이의 문자 구간에 일치(대문자)
[0-9] | 0부터 9 사이의 문자 구간에 일치(숫자)
[가-힣] | 가부터 힣 사이의 문자 구간에 일치(한글)
\w | 63개 문자(Word, 대소영문52개 + 숫자10개 + _)에 일치
\b | 63개 문자에 일치하지 않는 문자 경계(Boundary)
\d | 숫자(Digit)에 일치
\s | 공백(Space, Tab 등)에 일치
(?=) | 앞쪽 일치(Lookahead)
(?<=) | 뒤쪽 일치(Lookbehind)

```js
const str = `
010-1234-5678
theabc@gmail.com
https://www.omdbapi.com/?apikey=5f6c9466&s=frozen
The quick brown fox jumps over the lazy dog.
abbcccdddd
http://localhost:1234
동해물과 백두산이 마르고 닳도록
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


// [abc] -> a 또는 b 또는 c
console.log(str.match(/[fox]/g))  // (12) ["o", "o", "o", "f", "f", "o", "o", ..]


// [0-9] -> 0부터 9 사이의 문자 구간에 일치(숫자)
console.log(str.match(/[0-9]/g))  // (21) ["0", "1", "0", "1", "2", "3", "4", ...]
console.log(str.match(/[0-9]{1,}/g))  // (6) ["010", "1234", "5678", ...]


// [가-힣] -> 가부터 힣 사이의 문자 구간에 일치(한글)
console.log(str.match(/[가-힣]{1,}/g))  // (4) ["동해물과", "백두산이", "마르고", "닳도록"]


// \w -> 63개 문자(Word, 대소영문52개 + 숫자10개 + _)에 일치
console.log(str.match(/\w/g))  // ["0", "1", "0", "1", "2", ...]


// \b -> 63개 문자에 일치하지 않는 문자 경계(Boundary)
console.log(str.match(/\bf\w{1,}\b/g))  // ["frozen", "fox"]


// \d -> 숫자(Digit)에 일치
console.log(str.match(/\d/g))  // ["0", "1", "0", "1", "2", ...]
console.log(str.match(/\d{1,}/g))  // ["010", "1234", "5678", ...]


// \s -> 공백(Space, Tab 등)에 일치
console.log(str.match(/\s/g))  // ["\n", "\n", "\n", "\n", " ", " ", ...]

const h = `  the hello  world   !

`
console.log(h.replace(/\s/g, ''))  // thehelloworld!


// (?=) -> 앞쪽 일치(Lookahead)
console.log(h.match(/.{1,}(?=@)/g))  // ["theabc"]


// (?<=) -> 뒤쪽 일치(Lookbehind)
console.log(h.match(/(?<=@).{1,}/g))  // ["gmail.com"]
```