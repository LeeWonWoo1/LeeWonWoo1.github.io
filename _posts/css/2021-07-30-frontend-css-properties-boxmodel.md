---
title: "[CSS] CSS 속성 - 박스모델"
excerpt: CSS 속성인 박스모델 정리
categories:
- CSS
tags:
- - CSS
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-07-30T04:00:00'
last_modified_at: 2021-07-30T04:00:00
---

## 박스 모델


### - 단위

```
px 픽셀
% 상대적 백분율
em 요소의 글꼴 크기
rem 루트 요소(html)의 글꼴 크기
vw 뷰포트 가로 너비의 백분율
vh 뷰포트 세로 너비의 백분율
```


<br>

### - 색상 표현

```
이름 : red, royalblue, tomato // 브라우저에서 제공하는 색 이름
Hex 색상코드 : #000, #FFFFFF // 16진수 색상
RGB : rgb(255, 255, 255) // 빛의 삼원색
RGBA : rgba(0, 0, 0, 0.5) // 빛의 삼원색 + 투명도
HSL : hsl(120, 100%, 50%) // 색상, 채도, 명도
HSLA : hsla(120, 100%, 50%, 0.5) // 색상, 채도, 명도 + 투명도
```


<br>

### - width, height

```css
/* 요소의 가로/세로 너비 */
width, height {
  기본값: auto; 브라우저가 너비를 계산
  단위: px, em, vw;
}
```


<br>

### - max-width, max-height

```css
/* 요소가 커질 수 있는 최대 가로/세로 너비 */
max-width, max-height {
  기본값: none; 최대 너비 제한 없음
  단위: px, em, vw;
}
```


<br>

### - min-width, min-height

```css
/* 요소가 작아질 수 있는 최소 가로/세로 너비 */
min-width, min-height {
  기본값: 0; 최소 너비 제한 없음
  단위: px, em, vw;
}
```


<br>

### - margin

```css
/* 요소의 외부 여백을 지정하는 단축 속성 */
margin {
  기본값: 0; 외부 여백 없음
  auto 브라우저가 여백을 계산. 가운데 정렬에 활용
  단위: px, em, vw;
  음수 사용 가능
}

적용 {
  margin: 10px;  /* top, right, bottom, left*/
  margin: 10px 20px;  /* top, bottom / left, right */
  margin: 10px 20px 30px;  /* top / left, right / bottom */
  margin: 10px 20px 30px 40px;  /* top / right / bottom / left */
}

개별 속성 {
  margin-top: 10px;
  margin-bottom: 10px;
  margin-left: 10px;
  margin-right: 10px;
}
```


<br>

### - padding

```css
/* 요소의 내부 여백을 지정하는 단축 속성 */
padding {
  기본값: 0; 내부 여백 없음
  단위: px, em, vw;
  %: 부모 요소의 가로 너비에 대한 비율로 지정
  요소의 크기가 커짐
}

적용 {
  padding: 10px;  /* top, right, bottom, left*/
  padding: 10px 20px;  /* top, bottom / left, right */
  padding: 10px 20px 30px;  /* top / left, right / bottom */
  padding: 10px 20px 30px 40px;  /* top / right / bottom / left */
}

개별 속성 {
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 10px;
  padding-right: 10px;
}
```


<br>

### - border

```css
/* 요소의 테두리 선을 지정하는 단축 속성 */
border {
  border: 두께 종류 색상;
  요소의 크기가 커짐
}

적용 {
  border: 4px solid black;
}

두께 {
  border-width: px, em, %;
}

종류 {
  기본값: none; 선 없음
  border-style: solid; 실선
  border-style: dashed; 파선
  border-style: dotted; 점선
  border-style: double; 두줄선
  border-style: groove; 홈이 파여있는 모양
  border-style: ridge; 솟은 모양(groove 반대)
  border-style: inset; 요소 전체가 들어간 모양
  border-style: outset; 요소 전체가 나온 모양
}

색상 {
  기본값: black;
  투명: transparent;
}

모서리 {
  /* 둥글게 깎기 */
  기본값: 0;
  border-radius: px, em, vw;
}
```


<br>

### - box-sizing

```css
/* 요소의 크기 계산 기준을 지정 */
box-sizing {
  기본값: content-box; 요소의 내용으로 크기 계산
  box-sizing: border-box; 요소의 내용 + padding + border로 크기 계산
}
```


<br>

### - overflow

```css
/* 내용이 넘쳤을 때, 보여짐을 제어 */
overflow {
  기본값: visible; 넘친 내용을 그대로 보여줌
  overflow: hidden; 넘친 내용을 잘라냄
  overflow: scroll; 넘친 내용을 잘라내고 스크롤바 생성
  overflow: auto; 넘친 내용이 있는 경우에만 잘라내고 스크롤바 생성
}

개별속성 {
  overflow-x
  overflow-y
}
```


<br>

### - display

```css
/* 화면 출력 특성 */
display {
  기본값: block;
  기본값: inline;
  기본값: inline-block; 각 요소에 이미 지정되어 있는 값
  display: flex; 플렉스 박스 (1차원 레이아웃)
  display: grid; 그리드 (2차원 레이아웃)
  display: none; 보여짐 특성 없음, 화면에서 사라짐
  기타: table, table-row, table-cell 등;
}
```


<br>

### - opacity

```css
/* 요소 투명도 */
opacity {
  기본값: 1; 불투명
  opacity: 0~1; 0부터 1사이의 소수점 숫자
}
```