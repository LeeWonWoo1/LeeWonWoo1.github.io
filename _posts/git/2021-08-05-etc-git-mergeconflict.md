---
title: "[Git & Github] Merge & Conflict"
excerpt: 병합과 충돌
categories:
- Git
tags:
- - Github
  - Git
toc: true
toc_sticky: true
popular: true
date: '2021-08-05T19:00:00'
last_modified_at: 2021-08-05T19:00:00
---

## 1. Merge & Conflict

- 2개의 branch를 통합하는 것
- 현재의 branch와 merge하고자 하는 branch에서 같은 위치의 코드를 수정했을 경우 conflict 발생
- conflict가 발생했을 경우 상의하여 코드 수정


<br>

## 2. 명령어

```bash
# 현재 branch에서 merge
$ git merge 이름

# merge할 때, commit 이력을 제거하고 수정된 내용만 merge
$ git merge --squash 이름

# fast-forward 방식으로 merge할 때, commit message 생성
$ git merge --no-ff 이름
```


<br>

## 3. Fast-Forward merge


### - master branch에서 작업

```html
<!-- master branch -->
<body>
  <h1>abc</h1>
</body>
```

```bash
$ git add .
$ git commit -m "commit message abc"
```


<br>

### - 새로운 branch에서 작업

```html
<!-- xyz branch -->
<body>
  <h1>abc</h1>
  <h2>xyz</h2>
</body>
```

```bash
$ git checkout -b xyz
$ git add .
$ git commit -m "commit message xyz"
```


<br>

### - master branch에서 xyz branch merge 수행

```bash
$ git checkout master
$ git merge xyz
```

- master branch의 HEAD가 xyz branch의 HEAD로 이동함
- master branch의 commit message와 파일 내용이 xyz에서 작성한 내용을 포함


<br>

## 4. Conflict가 발생하는 merge


### - master branch에서 작업

```html
<!-- master branch -->
<body>
  <h1>abcd</h1>
  <h2>xyz</h2>
</body>
```

```bash
$ git add .
$ git commit -m "commit message abcd"
```


<br>

### - 새로운 branch에서 작업

```html
<!-- xyz branch -->
<body>
  <h1>abcdefg</h1>
  <h2>xyz</h2>
</body>
```

```bash
$ git checkout xyz
$ git add .
$ git commit -m "commit message abcdefg"
```


<br>

### - master branch에서 xyz branch merge 수행

```bash
$ git checkout master
$ git merge xyz
```

```html
<<<<<< HEAD
  <h1>abcd</h1>
=======
  <h1>abcdefg</h1>
>>>>>> xyz
```

- master branch와 xyz branch의 commit 수가 같아 fast-forward 방식으로 merge 안됨
- h1 태그의 내용을 동시에 각각 다른 값으로 수정함
- conflict가 발생한 부분을 상호 협의를 거쳐 비교한 후 수정해야 함