---
title: "[CSS] CSS 개요"
excerpt: CSS 기본 문법부터 선택자 우선순위까지
categories:
- CSS
tags:
- - CSS
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-07-30T03:30:00'
last_modified_at: 2021-07-30T03:30:00
---

## CSS 기본 문법

```css
/* 주석 */
선택자 {
  속성 : 값;
  속성 : 값;
}
```


## CSS 선언 방식


### - 내장 방식

style 태그의 내용으로 스타일 작성
{: .notice--info}

```html
<style>
  div {
    color: red;
    margin: 10px;
  }
</style>
```


<br>

### - 인라인 방식

요쇼의 style 속성에 직접 스타일 작성
{: .notice--info}

```html
<div style="color: red; margin: 10px;"></div>
```


<br>

### - 링크 방식

링크 태그로 외부 CSS 파일을 가져와서 연결
{: .notice--info}

```html
<link rel="stylesheet" href="./css/main.css">
```
```css
/* main.css */
div {
  color: red;
  margin: 20px;
}
```


<br>

### - @import 방식

CSS의 @import 규칙으로 CSS문서 안에서 또 다른 CSS문서를 가져와 연결
{: .notice--info}

```html
<link rel="stylesheet" href="./css/main.css">
```
```css
/* main.css */
@import url("./sub.css");

div {
  color: red;
  margin: 20px;
}
```
```css
/* sub.css */
.sub {
  width: 10px;
  height: 20px;
}
```


## CSS 선택자


### - 기본

```css
/* 전체 선택자 : 모든 요소 선택 */
* {
  color: red;
}

/* 태그 선택자 : 태그 이름의 요소 선택 */
div {
  color: red;
}

/* 클래스 선택자 : class 속성 값의 요소 선택  */
.cat {
  color: red;
}

/* 아이디 선택자 : id 속성 값의 요소 선택 */
#cat {
  color: red;
}
```


<br>

### - 복합

```css
/* 일치 선택자 : 선택자를 동시에 만족하는 요소 선택 */
div.cat {
  color: red;
}

/* 자식 선택자 : 자식 요소 선택 */
ul > .cat {
  color: red;
}

/* 하위(후손) 선택자 : 하위 요소 선택. 띄어쓰기가 선택자의 기호 */
div .cat {
  color: red;
}

/* 인접 형제 선택자 : 다음 형제 요소 하나를 선택 */
.cat + li {
  color: red;
}

/* 일반 형제 선택자 : 다음 형제 요소 모두를 선택 */
.cat ~ li {
  color: red;
}
```


<br>

### - 가상 클래스

```css
/* hover : 마우스 커서가 올라가 있는 동안 */
a:hover {
  color: red;
}

/* active : 마우스를 클릭하고 있는 동안 */
a:active {
  color: red;
}

/* focus : 포커스되면 선택 */
/* focus가 될 수 있는 요소는 HTML 대화형 콘텐츠가 해당 */
/* input, a, button, label, select 등 여러 요소 */ 
/* HTML 대화형 콘텐츠 요소가 아니더라도, tabindex 속성을 사용한 요소도 focus가 될 수 있음 */ 
input:focus {
  color: red;
}

/* first-child : 형제 요소중 첫째라면 선택*/
.animals div:first-child {
  color: red;
}

/* last-child : 형제 요소중 막내라면 선택 */
.animals span:last-child {
  color: red;
}

/* nth-child : 형제 요소중 n째라면 선택 */
.animals *:nth-child(2) {
  color: red;
}
.animals *:nth-child(2n) {
  color: red;
}
.animals *:nth-child(2n+1) {
  color: red;
}

/* not : 아닌 요소 선택 */
.animals *:not(div) {
  color: red;
}
```


<br>

### - 가상 요소

```css
/* before : 내부 앞에 내용을 삽입 */
.cat::before {
  content: "앞"
}

/* after 내부 뒤에 내용을 삽입 */
.cat::after {
  content: "뒤"
}
```


<br>

### - 속성

```css
/* 속성 : 해당 속성을 포함한 요소 선택 */
[disabled] {
  color: red;
}
[type] {
  color: red;
}

/* 속성-값 : 해당 속성을 포함하고 값이 x인 요소 선택 */
[type="password"] {
  color: red;
}
```


##  스타일 상속

```css
.animals {
  color: red;
}
```
```html
<div class="ecosystem">생태계
  <div class="animals">동물
    <div class="cat">고양이</div>
    <div class="dog">강아지</div>
    <div class="tiger">호랑이</div>
  </div>
  <div class="plant">식물</div>
</div>
```
<div class="ecosystem">생태계
  <div style="color: red;" class="animals">동물
    <div style="color: red;" class="cat">고양이</div>
    <div style="color: red;" class="dog">강아지</div>
    <div cstyle="color: red;" lass="tiger">호랑이</div>
  </div>
  <div class="plant">식물</div>
</div>


<br>

### - 상속되는 CSS 속성들

**<u>모두 글자/문자 관련 속성들</u>**

- font-style
- font-weight
- font-size
- line-height
- font-family
- color
- text-align
- ...


<br>

### - 강제 상속

- 값에 _inherit_ 넣어서 명시하면 상속됨


## 선택자 우선순위

- 같은 요소가 여러 선언의 대상이 된 경우, 어떤 선언의 CSS속성을 우선 적용할지 결정하는 방법
- 점수가 높은 선언 우선
- 점수가 같으면 마지막에 해석된 선언이 우선

```css
body { color : red; } /* 전체 선택자 : 0점 */
* { color : orange; }

div { color : yellow; } /* 태그 선택자 : 1점 */

.cat { color: green; } /* Class 선택자 : 10점 */

#dog { color: blue; } /* ID 선택자 : 100점 */
```
```html
<div style="color: darkblue;">Hi</div> <!-- 인라인 선언 : 1000점 -->
```
```css
div { color: purple !important; } /* !important : 999999점 */
```