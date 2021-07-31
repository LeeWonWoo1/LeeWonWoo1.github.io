---
title: "[CSS] CSS 속성 - 정렬, 전환, 변환"
excerpt: CSS 속성인 정렬, 전환, 변환 정리
categories:
- CSS
tags:
- - CSS
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-08-01T00:00:00'
last_modified_at: 2021-08-01T00:00:00
---

## 정렬


### - display

```css
/* Flex Container의 화면 출력 특성 */
display {
  display: flex; 블록 요소와 같이 Flex Container 정의
  display: inline-flex; 인라인 요소와 같이 Flex Container 정의
}
```


<br>

### - flex-direction

```css
/* 주 축을 설정 */
flex-direction {
  기본값: row; 행 축 (좌 -> 우)
  flex-direction: row-reverse; 행 축 (우 -> 좌)
  flex-direction: column; 열 축 (위 -> 아래)
  flex-direction: column-reverse; 열 축 (아래 -> 위)
}
```


<br>

### - flex-wrap

```css
/* Flex Items 묶음(줄 바꿈) 여부 */
flex-wrap {
  기본값: nowrap; 묶음(줄 바꿈) 없음
  flex-wrap: wrap; 여러 줄로 묶음
  flex-wrap: wrap-reverse; wrap의 반대 방향으로 묶음
}
```


<br>

### - justify-content

```css
/* 주 축의 정렬 방법 */
justify-content {
  기본값: flex-start; Flex Items를 시작점으로 정렬
  justify-content: flex-end; Flex Items를 끝점으로 정렬
  justify-content: center; Flex Items를 가운데 정렬
  justify-content: space-between; 각 Flex Item 사이를 균등하게 정렬
  justify-content: space-around; 각 Flex Item의 외부 여백을 균등하게 정렬
}
```


<br>

### - align-content

```css
/* 교차 축의 여러 줄 정렬 방법 */
align-content {
  기본값: stretch; Flex Items를 시작점으로 정렬
  align-content: flex-start; Flex Items를 시작점으로 정렬
  align-content: flex-end; Flex Items를 끝점으로 정렬
  align-content: center; Flex Items를 가운데 정렬
  align-content: space-between; 각 Flex Item 사이를 균등하게 정렬
  align-content: space-around; 각 Flex Item의 외부 여백을 균등하게 정렬
}
```


<br>

### - align-items

```css
/* 교차 축의 한 줄 정렬 방법 */
align-items {
  기본값: stretch; Flex Items를 교차 축으로 늘림
  align-items: flex-start; Flex Items를 각 줄의 시작점으로 정렬
  align-items: flex-end; Flex Items를 각 줄의 끝점으로 정렬
  align-items: center; Flex Items를 각 줄의 가운데 정렬
  align-items: baseline; Flex Items를 각 줄의 문자 기준선에 정렬
}
```


<br>

### - order

```css
/* Flex Item의 순서 */
order {
  기본값: 0; 순서 없음
  숫자: 숫자가 작을 수록 먼저;
}
```


<br>

### - flex-grow

```css
/* Flex Item의 증가 너비 비율 */
flex-grow {
  기본값: 0; 증가 비율 없음
  숫자: 증가 비율;
}
```


<br>

### - flex-shrink

```css
/* Flex Item의 감소 너비 비율 */
flex-shrink {
  기본값: 1; Flex Container 너비에 따라 감소 비율 적용
  숫자: 감소 비율;
}
```


<br>

### - flex-basis

```css
/* Flex Item의 공간 배분 전 기본 너비 */
flex-basis {
  기본값: auto; 요소의 Content 너비
  단위: px, em, rem;
}
```


<br>

## 전환


### - transition

```css
/* 요소의 전환(시작과 끝) 효과를 지정하는 단축 속성 */
태그 {
  transition: 속성명 지속시간 타이밍함수 대기시간;
  지속시간은 단축형으로 작성할 때, 필수 포함 속성
}
```


<br>

### - transition-property

```css
/* 전환 효과를 사용할 속성 이름을 지정 */
transition-property {
  기본값: all; 모든 속성에 적용
  속성이름: 전환 효과를 사용할 속성 이름 명시;
}
```


<br>

### - transition-duration

```css
/* 전환 효과의 지속시간을 지정 */
transition-duration {
  기본값: 0s; 전환 효과 없음
  시간: 지속시간(s)을 지정;
}
```


<br>

### - transition-timing-function

```css
/* 전환 효과의 타이밍(Easing) 함수를 지정 */
transition-timing-function {
  기본값: ease; 느리게-빠르게-느리게
  transition-timing-function: linear; 일정하게
  transition-timing-function: ease-in; 느리게-빠르게
  transition-timing-function: ease-out; 빠르게-느리게
  transition-timing-function: ease-in-out; 느리게-빠르게-느리게
  transition-timing-function: cubic-bezier(n, n, n, n); 자신만의 값을 정의(0~1)
  transition-timing-function: step(n); n번 분할된 애니메이션
}
```


<br>

### - transition-delay

```css
/* 전환 효과가 몇 초 뒤에 시작할지 대기시간을 지정 */
transition-delay {
  기본값: 0s; 대기시간 없음
  시간: 대기시간(s)을 지정;
}
```


<br>

## 변환

- 요소의 변환 효과
- transform: 변환함수1 변환함수2 변환함수3 ...

```css
태그 {
 transform: 원근법 이동 크기 회전 기울임;
}
```


### - 2D 변환 함수

```css
태그 {
  transform: translate(x, y); 이동(x축, y축)
  transform: translateX(x); 이동(x축)
  transform: translateY(y); 이동(y축)
  transform: scale(x, y); 크기(x축, y축)
  transform: scaleX(x); 크기(x축)
  transform: scaleY(y); 크기(x축)
  transform: rotate(degree); 회전(각도)
  transform: skew(x, y); 기울임(x축, y축)
  transform: skewX(x); 기울임(x축)
  transform: skewY(y); 기울임(y축)
  transform: matrix(n, n, n, n, n, n); 2차원 변환 효과
}
```


<br>

### - 3D 변환 함수

```css
태그 {
  transform: translateZ(z); 이동(z축)
  transform: translate3d(x, y, z); 이동(x축, y축, z축)
  transform: scaleZ(z); 크기(z축)
  transform: scale3d(x, y, z); 크기(x축, y축, z축)
  transform: perspective(n); 원근법(거리)
  transform: matrix3d(n, ..... , n); 3차원 변환 효과
  transform: rotateX(x); 회전(x축)
  transform: rotateY(y); 회전(y축)
  transform: rotateZ(z); 회전(z축)
  transform: rotate3d(x, y, z, a); 회전(x축, y축, z축, 각도)
}
```


<br>

### - perspective

```css
/* 하위 요소를 관찰하는 원근 거리를 지정 */
perspective {
  단위: px;
}
```


<br>

### - backface-visibility

```css
/* 3D 변환으로 회전된 요소의 뒷면 숨김 여부 */
backface-visibility {
  기본값: visible; 뒷면 보임
  backface-visibility: hidden; 뒷면 숨김
}
```