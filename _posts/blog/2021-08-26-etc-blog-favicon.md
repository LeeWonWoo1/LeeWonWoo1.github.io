---
title: "[Github 블로그] Favicon 등록"
excerpt: Github 블로그의 Favicon을 등록합니다.
categories:
- Blog
tags:
- - Blog
  - jekyll
  - Github
  - Git
  - minimal-mistake
toc: true
toc_sticky: true
popular: true
date: '2021-08-26T21:00:00'
last_modified_at: 2021-08-26T21:00:00
---

## 1. Github 블로그 Favicon 등록하기

[https://favicon.io/emoji-favicons](https://favicon.io/emoji-favicons){:target="_blank"}에 접속해 필요한 Favicon 압축파일을 다운로드 받음

![favicon7](https://user-images.githubusercontent.com/62803763/130961778-38a8d60f-6429-48d8-850b-9043563edb3f.PNG){: .align-center .open-new}

<br>

다운받은 파일의 압축을 풀고, 내 블로그 폴더의 index.html 파일이 있는 최상위 루트 경로에 파일을 옮김(about.txt파일 제외)

![favicon2](https://user-images.githubusercontent.com/62803763/130962202-5f9d8111-ae6a-456c-9653-f2ce716618b3.PNG){: .align-center .open-new}

<br>

[https://realfavicongenerator.net](https://realfavicongenerator.net){:target="_blank"}에 접속해 `Select your Favicon image` 버튼을 클릭하고 이미지를 업로드함

![favicon3](https://user-images.githubusercontent.com/62803763/130962580-d41dc0fa-8c80-4f57-a9f7-bf379025e939.png){: .align-center .open-new}

<br>

![favicon4](https://user-images.githubusercontent.com/62803763/130962636-c0d6c822-aa1d-4a8d-bc72-2046d6a56c6f.PNG){: .align-center .open-new}

<br>

페이지 맨 하단에 `Generate your Favicons and HTML code`를 클릭

![favicon5](https://user-images.githubusercontent.com/62803763/130962788-a87d4da7-84e8-4fe5-afef-87e8f61057c3.PNG){: .align-center .open-new}

<br>

HTML 태그가 나오면, 복사해서 블로그 폴더의 _include/head/custom.html에 붙여넣기

![favicon6](https://user-images.githubusercontent.com/62803763/130963191-0c83316e-e592-4bcc-a660-a90ca6459d0c.PNG){: .align-center .open-new}

<br>

![favicon8](https://user-images.githubusercontent.com/62803763/130963240-dd272e13-fb79-41fa-9bde-79f509b5a86c.PNG){: .align-center .open-new}

<br>

![favicon9](https://user-images.githubusercontent.com/62803763/130963273-b1cee471-957b-4a30-a7ab-32ff9b123154.PNG){: .align-center .open-new}

<br>

Github에 업로드

```bash
$ git add .
$ git commit -m "commit message"
$ git push origin master
```

<br>

반영된 Favicon 확인

![favicon1](https://user-images.githubusercontent.com/62803763/130963480-e9479a97-fc25-4cb9-ac23-b39c5db768b7.png){: .align-center .open-new}


<br>

## 2. 원하는 이미지 ICO 파일로 변경

[https://www.icoconverter.com/](https://www.icoconverter.com/){:target="_blank"}에 접속해 원하는 이미지를 등록하고 변환할 수 있음(32 pixels면 충분)

![favicon10](https://user-images.githubusercontent.com/62803763/130963949-5538156b-ca80-45a8-bafe-93fe92f6c902.PNG){: .align-center .open-new}