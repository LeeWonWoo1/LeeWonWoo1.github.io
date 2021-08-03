---
title: "[Git & Github] Markdown"
excerpt: Markdown 문법 정리
categories:
- Git
tags:
- - Github
  - Git
  - Markdown
toc: true
toc_sticky: true
popular: true
date: '2021-08-03T17:00:00'
last_modified_at: 2021-08-03T17:00:00
---

## 1. 제목(Header)

- #의 개수에 따라 h1 ~ h6 태그의 크기로 Header이 적용

```
# 제목1
## 제목2
### 제목3
#### 제목4
##### 제목5
###### 제목6
```

# 제목1(Header)
## 제목2
### 제목3
#### 제목4
##### 제목5
###### 제목6



<br>

## 2. 문장(Paragraph)

```
가나다라 마바사아
자차카타 파하.
```

가나다라 마바사아
자차카타 파하.


<br>

## 3. 줄바꿈(Line Breaks)


### - 띄어쓰기 2회

```
가나다라 마바사아  
자차카타 파하
```

가나다라 마바사아  
자차카타 파하.


### - br태그

```
가나다라 마바사아 <br> 자차카타 파하.
```

가나다라 마바사아 <br> 자차카타 파하.


<br>

## 4. 강조(Emphasis)


### - 두껍게

```
**두껍게**
```

**두껍게**


### - 이텔릭(기울임)

```
*이텔릭*
_이텔릭_
```

*이텔릭* <br>
_이텔릭_


### - 취소선

```
~~취소선~~
```

~~취소선~~


### - 밑줄

- 권장되지 않음

```
<u>밑줄</u>
```

<u>밑줄</u>


### - 색상

```
<span style="color: red">색상</span>
```

<span style="color: red">색상</span>


<br>

## 5. 목록(List)


### - 순서가 필요한 목록

```
1. 순서가 필요한 목록1
2. 순서가 필요한 목록2
3. 순서가 필요한 목록3
    1. 순서가 필요한 목록1
        1. 순서가 필요한 목록1
        2. 순서가 필요한 목록2
    2. 순서가 필요한 목록2
4. 순서가 필요한 목록4
```

1. 순서가 필요한 목록1
2. 순서가 필요한 목록2
3. 순서가 필요한 목록3
    1. 순서가 필요한 목록1
        1. 순서가 필요한 목록1
        2. 순서가 필요한 목록2
    2. 순서가 필요한 목록2
4. 순서가 필요한 목록4


### - 순서가 필요하지 않은 목록

```
- 순서가 필요하지 않은 목록
- 순서가 필요하지 않은 목록
- 순서가 필요하지 않은 목록
    - 순서가 필요하지 않은 목록
        - 순서가 필요하지 않은 목록
        - 순서가 필요하지 않은 목록
    - 순서가 필요하지 않은 목록
- 순서가 필요하지 않은 목록
```

- 순서가 필요하지 않은 목록
- 순서가 필요하지 않은 목록
- 순서가 필요하지 않은 목록
    - 순서가 필요하지 않은 목록
        - 순서가 필요하지 않은 목록
        - 순서가 필요하지 않은 목록
    - 순서가 필요하지 않은 목록
- 순서가 필요하지 않은 목록


### - 체크 리스트

````
- [X] 체크
- [ ] 체크X
````

- [X] 체크
- [ ] 체크X


<br>

## 6. 링크(Links)

```
<a href="https://google.com">GOOGLE</a>
<br>
[GOOGLE](https://google.com)
```

<a href="https://google.com">GOOGLE</a>
<br>
[GOOGLE](https://google.com)

<br>

- title : 링크에 마우스를 올렸을 때 나타나는 메시지

```
<a href="https://naver.com" title="NAVER로 이동!">NAVER</a>
<br>
[NAVER](https://naver.com "NAVER로 이동!")
```

<a href="https://naver.com" title="NAVER로 이동!">NAVER</a>
<br>
[NAVER](https://naver.com "NAVER로 이동!")

<br>

- target="_blank" : 링크를 클릭했을 때 창이 새 탭에 열림

```
<a href="https://naver.com" title="NAVER로 이동!" target="_blank">NAVER</a>
```

<a href="https://naver.com" title="NAVER로 이동!" target="_blank">NAVER</a>


<br>

## 7. 이미지(Image)


### - 일반

```
![이미지](경로)
```

![ggam1](https://user-images.githubusercontent.com/62803763/127985715-0184cb33-7457-4cf9-b988-97b1ba9b092f.jpg)

<br>

### - 이미지에 링크 걸기

```
[![이미지](경로)](링크 url)
```

- 사진 클릭하면 구글로 이동

[![ggam2](https://user-images.githubusercontent.com/62803763/127985728-a9c23902-b17c-4d97-9b47-b3481735f854.jpg)](https://google.com)


<br>

## 8. 인용문

```
> 남의 말이나 글에서 직접 또는 간접으로 따온 문장.  
> (네이버 국어 사전)

> 인용문을 작성하세요!
    >> 중첩된 인용문
      >>> 중중첩된 인용문 1
      >>> 중중첩된 인용문 2
      >>> 중중첩된 인용문 3
```

> 남의 말이나 글에서 직접 또는 간접으로 따온 문장.  
> (네이버 국어 사전)

> 인용문을 작성하세요!
    >> 중첩된 인용문
      >>> 중중첩된 인용문 1
      >>> 중중첩된 인용문 2
      >>> 중중첩된 인용문 3


<br>

## 9. 인라인(inline) 코드 강조

```
백틱기호 ` `를 사용해 강조

CSS에서 `background` 혹은 `background-image` 속성으로 요소에 배경 이미지를 삽입할 수 있습니다.
```

CSS에서 `background` 혹은 `background-image` 속성으로 요소에 배경 이미지를 삽입할 수 있습니다.


<br>

## 10. 블록(block) 코드 강조


```html
<a href="https://www.google.co.kr/" target="_blank">GOOGLE</a>
```

<br>

```css
.list > li {
  position: absolute;
  top: 40px;
}
```

<br>

```javascript
function func() {
  var a = 'AAA'
  return a;
}
```

<br>

```bash
$ git commit -m 'Study Markdown'
```

```plaintext
가나다라 마바사아  
자차카타 파하
```


<br>

## 11. 표(Table)

```
|:--| : 왼쪽 정렬
|--:| : 오른쪽 정렬
|:--:| : 가운데 정렬


position 속성

값 | 의미 | 기본값
--|:--:|--:
static | 기준 없음 | O
relative | 요소 자신 | X
absolute | 위치 상 부모 요소 | X
fixed | 뷰포트 | X
```

position 속성

값 | 의미 | 기본값
--|:--:|--:
static | 기준 없음 | O
relative | 요소 자신 | X
absolute | 위치 상 부모 요소 | X
fixed | 뷰포트 | X


<br>

## 12. 원시 HTML(Raw HTML)

```
동해물과 <u>백두산</u>이 마르고 닳도록<br/>
<span style="text-decoration: underline;">하느님</span>이 보우하사 우리나라 만세

<a href="https://naver.com" title="NAVER로 이동!" target="_blank">NAVER</a>

<img width="100" src="https://user-images.githubusercontent.com/62803763/127985736-2879d5fd-621b-4872-8b9b-0b0ce9141c7a.jpg" alt="ggam4" /> 
```

동해물과 <u>백두산</u>이 마르고 닳도록<br/>
<span style="text-decoration: underline;">하느님</span>이 보우하사 우리나라 만세

<a href="https://naver.com" title="NAVER로 이동!" target="_blank">NAVER</a>

<img width="100" src="https://user-images.githubusercontent.com/62803763/127985736-2879d5fd-621b-4872-8b9b-0b0ce9141c7a.jpg" alt="ggam4" /> 


<br>

## 13. 수평선(Horizontal Rule)

```
---

***
```

---

***

