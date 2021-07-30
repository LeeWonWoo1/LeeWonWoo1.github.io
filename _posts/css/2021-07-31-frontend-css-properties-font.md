---
title: "[CSS] CSS 속성 - 글꼴, 문자"
excerpt: CSS 속성인 글꼴, 문자 정리
categories:
- CSS
tags:
- - CSS
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-07-31T03:00:00'
last_modified_at: 2021-07-31T03:00:00
---

## 글꼴


### - font-style

```css
/* 글자의 기울기 */
font-style {
  기본값: normal; 기울기 없음
  font-style: italic; 이텔릭체
  font-style: oblique; 기울어진 글자
}
```


<br>

### - font-weight

```css
/* 글자의 두께 */
font-weight {
  기본값: normal or 400; 기본 두께
  font-weight: bold or 700; 두껍게
  font-weight: bolder; 부모 요소보다 두껍게
  font-weight: lighter; 부모 요소보다 얇게
  font-weight: 100 ~ 900; 100단위의 숫자 9개
}
```


<br>

### - font-size

```css
/* 글자의 크기 */
font-size {
  기본값: 16px; 기본 크기
  단위: px, em, rem;
  %: 부모 요소의 폰트 크기에 대한 비율
  font-size: larger; 부모 요소보다 크게
  font-size: smaller; 부모 요소보다 작게
  font-size: xx-small ~ xx-large; 가장 작은 크기 ~ 가장 큰 크기까지 7단계 크기
}
```


<br>

### - line-height

```css
/* 한 줄의 높이, 행간과 유사 */
line-height {
  기본값: normal; 브라우저의 기본 정의
  line-height: 숫자; 요소의 글꼴 크기의 배수로 지정
  단위: px, em, rem;
  %: 요소의 글꼴 크기의 비율로 지정
}
```


<br>

### - font-family

```css
font-family {
  font-family: serif; 바탕체 계열
  font-family: sans-serif; 고딕체 계열
  font-family: monospace; 고정너비 글꼴 계열
  font-family: cursive; 필기체 계열
  font-family: fantasy; 장식 글꼴 계열
}
```

<div style="font-family: serif">Hello World!</div>
<div style="font-family: sans-serif">Hello World!</div>
<div style="font-family: monospace">Hello World!</div>
<div style="font-family: cursive">Hello World!</div>
<div style="font-family: fantasy">Hello World!</div>



## 문자


### - color

```css
/* 글자의 색상 */
color {
  기본값: rgb(0, 0, 0); 검정색
  color: 색상; 기타 지정 가능한 색상
}
```


<br>

### - text-align

```css
/* 문자의 정렬 방식 */
text-align {
  기본값: left; 왼쪽 정렬
  text-align: right; 오른쪽 정렬
  text-align: center; 가운데 정렬
  text-align: justify; 양쪽 정렬
}
```


<br>

### - text-decoration

```css
/* 문자의 장식(선) */
text-decoration {
  기본값: none; 장식 없음
  text-decoration: underline; 밑줄
  text-decoration: overline; 윗줄
  text-decoration: line-through; 중앙 선
}
```

<div>Hello World!</div>
<div style="text-decoration: underline">Hello World!</div>
<div style="text-decoration: overline">Hello World!</div>
<div style="text-decoration: line-through">Hello World!</div>


<br>

### - text-indent

```css
/* 문자 첫 줄의 들여쓰기 */
text-indent {
  기본값: 0; 들여쓰기 없음
  단위: px, em, rem;
  %: 요소의 가로 너비에 대한 비율
  음수 사용 가능
  반대는 내어쓰기 outdent
}
```