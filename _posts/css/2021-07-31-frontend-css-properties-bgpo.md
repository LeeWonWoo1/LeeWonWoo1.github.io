---
title: "[CSS] CSS 속성 - 배경, 배치"
excerpt: CSS 속성인 배경, 배치 정리
categories:
- CSS
tags:
- - CSS
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-07-31T11:30:00'
last_modified_at: 2021-07-31T11:30:00
---

## 배경


### - background-color

```css
/* 요소의 배경 색상 */
background-color {
  기본값: transparent; 투명함
  색상: 지정 가능한 색상;
}
```


<br>

### - background-image

```css
/* 요소의 배경 이미지 삽입 */
background-image {
  기본값: none; 이미지 없음
  background-image: url("경로"); 이미지 경로
}
```


<br>

### - background-repeat

```css
/* 요소의 배경 이미지 반복 */
background-repeat {
  기본값: repeat; 이미지를 수직, 수평 반복
  background-repeat: repeat-x; 이미지를 수평 반복
  background-repeat: repeat-y; 이미지를 수직 반복
  background-repeat: no-repeat; 반복 없음
}
```


<br>

### - background-position

```css
/* 요소의 배경 이미지 위치 */
background-position {
  기본값: 0% 0%; 0% ~ 100% 사이 값
  방향: top, bottom, left, right, center;
  단위: px, em, rem; 
}
```


<br>

### - background-size

```css
/* 요소의 배경 이미지 크기 */
background-size {
  기본값: auto; 이미지의 실제 크기
  단위: px, em, rem;
  cover: 비율을 유지, 요소의 더 넓은 너비에 맞춤;
  contain: 비율을 유지, 요소의 더 짧은 너비에 맞춤;
}
```


<br>

### - background-attachment

```css
/* 요소의 배경 이미지 스크롤 특성 */
background-attachment {
  기본값: scroll; 이미지가 요소를 따라서 같이 스크롤
  background-attachment: fixed; 이미지가 뷰포트에 고정, 스크롤X
  background-attachment: local; 요소 내 스크롤 시 이미지가 같이 스크롤
}
```


<br>

## 배치


### - position

```css
/* 요소의 위치 지정 기준 */
position {
  기본값: static; 기준 없음
  position: relative; 요소 자신을 기준
  position: absolute; 위치 상 부모 요소를 기준, 부모 꼭 확인해야 함
  position: fixed; 뷰포트를 기준
  position: sticky; 스크롤 영역 기준
  position과 같이 사용하는 CSS속성들은 모두 음수 사용 가능
}
```


<br>

### - 요소 쌓임 순서

- 어떤 요소가 사용자와 더 가깝게 있는지 결정
    1. 요소에 position 속성의 값이 있는 경우 위에 쌓임(static제외)
    2. 1번 조건이 같은 경우, z-index 속성의 숫자 값이 높을 수록 위에 쌓임
    3. 1, 2번 조건이 같은 경우, HTML의 다음 구조일 수록 위에 쌓임


### - z-index

```css
/* 요소 쌓임 정도를 지정 */
z-index {
  기본값: auto; 부모 요소와 동일한 쌓임 정도
  숫자: 숫자가 높을 수록 위에 쌓임;
}
```


### - 요소의 display가 변경

- position 속성의 값으로 absolute, fixed가 지정된 요소는 display 속성이 block로 변경

```css
태그 {
  display: block;
  position: absolute;
  top: 30px;
  left: 30px;
  z-index: 1;
}

/* 위와 아래는 동일 */

태그 {
  position: absolute;
  top: 30px;
  left: 30px;
  z-index: 1;  
}
```