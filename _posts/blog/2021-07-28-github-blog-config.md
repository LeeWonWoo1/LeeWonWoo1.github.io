---
title: "[Github 블로그] _config.yml 셋팅"
excerpt: 자신의 블로그를 커스터마이징 하기 위해 _config.yml을 수정합니다.
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
date: '2021-07-28'
last_modified_at: '2021-07-28'
---

## config 수정 공식 사이트

[minimal-mistakes _config.yml 설정 공식 사이트 ]({{"https://mmistakes.github.io/minimal-mistakes/docs/configuration/"}}){:target="_blank"} 
{: .notice--info}

## _config.yml 실행

vscode로 루트경로에 있는 **_config.yml** 을 열어주고 작업한다.<br>
필요없는 부분은 제외하고 작성했다.

## _config.yml 수정

```yml
minimal_mistakes_skin    : "dark" # "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"

# 사이트 기본 세팅
locale                   : "ko-KR"
title                    : "LWW's Tech Blog" # 타이틀
title_separator          : "&#124;" # 구분자
subtitle                 : "Version 1.0" # 타이틀 하단 글씨
name                     : "이원우" # footer에 찍히는 이름
description              : "꾸준히 기록하는 블로그" # 설명
url                      : "https://LeeWonWoo1.github.io" # 호스트 주소
repository               : "LeeWonWoo1/LeeWonWoo1.github.io" # GitHub 유저이름 / 레포지 이름
teaser                   : 
logo                     : # 타이틀 옆 이미지
masthead_title           : "LWW's Tech Blog" # 최 상단 타이틀
breadcrumbs              : true # 브래드크럼 사용 여부
words_per_minute         : 200 

# 댓글
comments:
  provider               : "disqus" #
  disqus:
    shortname            : LWW # disqus에 입력한 Web Site Name
  discourse:
    server               : 

# 구글 Recaptcha
reCaptcha:
  siteKey                :
  secret                 :
atom_feed:
  path                   : 
  hide                   : 
search                   : true 
search_full_content      : true 

# Analytics
analytics:
  provider               : false 


# Site Author
author:
  name             : "이원우"
  avatar           : "/assets/images/profile/bear.jpg" # 프로필 이미지
  bio              : "CS / FrontEnd"
  location         : "Republic of Korea"
  email            : "plmplmdnjsdn@naver.com"
  links:
    - label: "Website"
      icon: "fas fa-fw fa-link"
      url: "https://LeeWonWoo1.github.io"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/LeeWonWoo1"


# Site Footer
footer:
  links:
    - label: "Email"
      icon: "fab fa-fw fa-envelope-square"
      url: mailto:plmplmdnjsdn@naver.com
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/LeeWonWoo1"

# Post에 적용될 default 설정
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
      popular: false
```

수정하면서 종종 jekyll 서버로 확인한다.

```bash
$ jekyll serve
```

## Github 연동
수정을 완료하면 Github에 연동한다.

```bash
$ git add .
$ git commit -m "commit message"
$ git push origin master
```