---
title: "[HTML] HTML 구조 및 태그"
excerpt: HTML 요소의 구조 및 태그를 학습
categories:
- HTML
tags:
- - HTML
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-07-30T01:30:00'
last_modified_at: 2021-07-30T01:30:00
---

## HTML 구조

```html
<!DOCTYPE html>  <!-- 문서의 HTML 버전을 지정 -->

<html>       <!-- 문서의 전체 범위 -->

  <head>     <!-- 문서의 정보를 나타내는 범위 -->
             <!-- 웹 페이지의 보이지 않는 정보를 작성하는 범위 -->
  </head>

  <body>     <!-- 문서의 구조를 나타내는 범위 -->
             <!-- 웹 페이지의 보여지는 구조를 작성하는 범위 -->
  </body>
</html>
```


## Head 태그 내부


### - meta 태그

```html
<meta charset="UTF-8" />   <!-- 문자 인코딩 방식 -->
<meta name="viewport" content="width=xxxx..." />
<!-- 정보의 종류     정보의 값 -->
```
```
<meta />는 HTML 문서의 제작자, 내용, 키워드 등의 정보를 검색엔진이나 브라우저에 제공
```


<br>

### - title 태그

```html
<title>Google</title> <!-- HTML 문서의 제목을 정의. 웹 브라우저 탭에 표시됨-->
```


<br>

### - link 태그

```html
<!-- 관계              경로 -->
<link rel="stylesheet" href="./main.css" />
<link rel="icon" htrf="./favicon.png" />
```
```
<link />는 외부 문서를 가져와 연결할 때 사용. 대부분 CSS 파일
```


<br>

### - style 태그

```html
<!-- CSS를 HTML 문서 안에서 작성하는 경우에 사용 -->
<style>
  div {
    color : red;
  }
</style>
```


<br>

### - script 태그

```html
<script src="./main.js"></script>  <!-- JS파일 가져오는 경우-->

<!-- JS를 HTML 문서 안에서 작성하는 경우 -->
<script>
  console.log('Hello World!!')
</script>
```


## Body 태그 내부


### - div 태그

```html
<div></div>  <!-- Block, 특별한 의미가 없는 구분을 위한 요소 -->
```


<br>

### - h 태그

```html
<h1>제목1</h1>    <!-- Block, 제목을 의미하는 요소 -->
<h2>제목2</h2>    <!-- 숫자가 작을수록 더 중요한 제목-->
<h6>제목6</h6>
```


<br>

### - p 태그

```html
<p>가나 다라마</p>  <!-- Block, 문장을 의미하는 요소 -->
```


<br>

### - img 태그

```html
<!-- 경로              대체 텍스트 -->
<img src="img/xxx.png" alt="xxx" /> <!-- Inline, 이미지 삽입 요소-->
```


<br>

### - ul, li 태그

```html
<ul>  <!-- Block, 순서가 필요 없는 목록의 집합-->
  <li>강아지</li> 
  <li>고양이</li>  <!-- 목록 내 각 항목 -->
  <li>돼지</li>
</ul>
```


<br>

### - a 태그

```html
<!-- Inline, 다른/같은 페이지로 이동하는 하이퍼링크 지정하는 요소 -->
<a href="http://www.google.com" target="_blank">Google</a>
<!-- URL                       URL의 표시(브라우저 탭) 위치 -->
```


<br>

### - span 태그

```html
<span>가나다</span> <!-- Inline, 특별한 의미가 없는 구분을 위한 요소-->
```


<br>

### - br 태그

```html
<p>가나다라<br/>마바사아</p> <!--Inline, 줄바꿈 요소-->
```
```
가나다라
마바사아
```


<br>

### - input 태그

```html
<!--Inline-Block, 데이터를 입력하는 요소-->
<input type="text" value="xxx" placeholder="yyy" disabled/> 
<!--  타입         입력된 값     힌트            비활성화 -->
```


<br>

### - label 태그

```html
<label> <!--Inline, 라벨 가능 요소(input)의 제목-->
  <input type="checkbox" /> Dog
</label>
<label>
  <input type="checkbox" checked /> Cat
</label> 

<label> <!-- animals 그룹에서 1개만 입력 -->
  <input type="radio" name="animals" /> Dog
</label>
<label>
  <input type="radio" name="animals" /> Cat
</label> 
```


<br>

### - table, tr, td 태그

```html
<table>  <!-- Table, 표 요소, 행과 열의 집합 -->

  <tr>   <!-- Table, 행을 지정하는 요소 -->
    <td>A</td><td>B</td> <!-- Table, 열을 지정하는 요소 -->
  </tr>
  <tr>
    <td>C</td><td>D</td>
  </tr>

</table>
```
```
A B
C D
```


## HTML 전역 속성

```html
<태그 title="설명"></태그>   <!-- 요소의 정보나 설명을 지정 -->
<태그 style="스타일"></태그> <!-- 요소에 적용할 스타일 지정 -->
<태그 class="이름"></태그>   <!-- 요소를 지칭하는 중복 가능한 이름 -->
<태그 id="이름"></태그>      <!-- 요소를 지칭하는 고유한 이름 -->
<태그 data-이름="데이터"></태그> <!-- 요소에 데이터를 지정 -->
```