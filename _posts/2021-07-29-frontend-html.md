---
title: "[HTML] 글자와 상자"
excerpt: 요소가 화면에 출력되는 특성인 Inline 요소와 Block 요소
categories:
- HTML
tags:
- - HTML
  - Web
toc: true
toc_sticky: true
popular: true
date: '2021-07-29'
last_modified_at: '2021-07-29'
---

## 글자와 상자

요소가 화면에 출력되는 특성. 크게 2가지로 구분됨.

**인라인(Inline) 요소 :** 글자를 만들기 위한 요소<br>
**블록(Block) 요소 :** 상자(레이아웃)를 만들기 위한 요소

### - Inline 요소

```html
<span>Hello</span>
<span>World!!</span>
```
```
Hello World!!
------------->
요소가 수평으로 쌓임

가로는 포함한 콘텐츠 크기만큼 줄어듬
<---> <----->
Hello World!! ↕ 세로도 포함한 콘텐츠 크기만큼 줄어듬
```

**span**은 가장 대표적인 인라인 요소.<br>
본질적으로 아무것도 나타내지 않는 콘텐츠 영역을 설정하는 용도<br>

<br>
Inline 요소는 가로, 세로 <u>너비를 지정할 수 없음</u>

```html
<span style="width: 100px;">Hello</span>
<span style="height: 100px;">World!!</span>
```
```
Hello World!!  <-- 반응 없음
```

<br>
외부, 내부 여백을 지정할 수 있지만, <u>상하 여백은 사용 불가</u>

```html
<span style="margin: 20px 20px;">Hello</span>
<span style="padding: 20px 20px;">World!!</span>
```
```
20px         20px   20px     20px
<-->『Hello』<--> 『<-->World<-->』
```

<br>
```java
<span><div></div></span>    <!-- Inline 요소 안에 Block 요소 사용 불가 -->
<span><span></span></span>  <!-- Inline 요소 안에 Inline 요소 사용 가능 -->
```

<br>

### - Block 요소

```html
<div>Hello</div>
<div>World!!</div>
```
```
Hello     ↓
World!!   ↓  요소가 수직으로 쌓임

가로는 부모 요소의 크기만큼 늘어남
<---------------------------------->
Hello                              ↕
World!!                            ↕
세로는 포함한 콘텐츠 크기만큼 줄어듬
```

**div**은 가장 대표적인 블록 요소.<br>
본질적으로 아무것도 나타내지 않는 콘텐츠 영역을 설정하는 용도<br>

<br>
Block 요소는 가로, 세로 <u>너비를 지정할 수 있음</u>

```html
<div style="width: 100px;">Hello</div>
<div style="height: 40px;">World!!</div>
```
```
     100px
<-------------->
Hello          ↕
World!!                        ↕
                               ↕ 40px
<------------------------------>
```

<br>
외부, 내부 <u>여백을 지정할 수 있음</u>

```html
<div style="margin: 20px;">Hello</div>
<div style="padding: 20px;">World!!</div>
```
```
20px             ↕ 20px          20px
<-->『Hello                    』<-->
                 ↕ 20px
『               ↕ 20px          20px
<-->World!!                      <-->
 20px            ↕ 20px             』
```

<br>
```java
<div><div></div></div>    <!-- Block 요소 안에 Block 요소 사용 불가 -->
<div><span></span></div>  <!-- Block 요소 안에 Inline 요소 사용 가능 -->
```


