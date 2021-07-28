---
title: "[Github 블로그] Github Blog 시작!"
excerpt: Github 블로그를 시작하기 위해 필요한 환경을 셋팅하고 Github과 연동합니다.
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

Github blog를 개설하는 과정을 간단하게 알아봅니다.

**주의!** Git의 사용법을 어느정도 숙지해야 합니다.
{: .notice--danger}

## 1. Github repository 생성
새 repository 이름을 **[자신의 Github ID].github.io** 로 설정한다.

![create-repository](https://user-images.githubusercontent.com/62803763/127294001-f4640a23-8c82-47b9-bb55-243c7157a5fb.PNG){: .align-center .open-new}

## 2. Import code
원하는 Jekyll 테마를 선택하고 코드를 복사한다. Jekyll 테마를 모아둔 사이트는 다음과 같다.

**Jekyll ?** Ruby 언어로 만들어져 html, markdown 등의 텍스트를 가공하는 텍스트 변환 엔진
{: .notice--info}
<br>
[http://jekyllthemes.org/]({{"http://jekyllthemes.org/"}}){:target="_blank"}<br>
[http://themes.jekyllrc.org/]({{"http://themes.jekyllrc.org/"}}){:target="_blank"}<br>
[https://jekyllthemes.io/]({{"https://jekyllthemes.io/"}}){:target="_blank"}<br>
<br>
나의 경우 [minimal-mistakes]({{"https://github.com/mmistakes/minimal-mistakes"}}){:target="_blank"} 의 'dark' 테마가 마음에 들어 선택했다.

코드를 복사한 뒤 생성한 **[자신의 Github ID].github.io** repository로 돌아와 import 한다.

![clone-https](https://user-images.githubusercontent.com/62803763/127293828-d60e753f-9aa8-4293-a9b9-2af122c8c66d.PNG){: .align-center .open-new}

![import-repository](https://user-images.githubusercontent.com/62803763/127293893-f7b72c9d-915f-45ef-b14b-9ee19273a4f6.PNG){: .align-center .open-new}

![import-repository2](https://user-images.githubusercontent.com/62803763/127293953-9ae44db5-abec-4273-90d0-6784d399e580.PNG){: .align-center .open-new}

이때 나와 같이 Import하지 않고 repository를 fork 하거나 파일을 Download해도 된다.

## 3. git clone
Import한 파일들을 작업하기 위해 vscode 터미널에서 clone한다.

```bash
$ git clone https://github.com/Github ID/Github ID.github.io.git
```

## 4. Rubby 설치
Jekyll을 설치하기 **전에** Ruby를 설치한다.

**Linux Ubuntu 환경** 
{: .notice--info}

```bash
$ sudo apt-get install ruby-full
$ ruby -v
```

설치가 잘 되었다면 cmd 창에 버전이 잘 출력될 것이다.

<br>

**Windows 환경** 
{: .notice--info}

[ Ruby 다운로드 사이트 ]({{" https://rubyinstaller.org/downloads/ "}}){:target="_blank"}에서 다운받아 설치한다.<br>
설치 과정에서 `"Add Ruby executables to your PATH"` 에 체크하면 자동으로 환경변수 설정이 완료된다.

## 5. Jekyll, Bundler 설치
본인이 clone한 폴더로 들어가면 **Gemfile** 이라는 파일이 있을 것이다. cmd를 켜서 이 파일이 있는 경로로 들어간 후, 아래의 명령을 수행한다.

```bash
$ gem install jekyll bundler
$ bundle
$ jekyll -v
```

Jekyll이 잘 설치되었다면 cmd 창에 버전이 잘 출력될 것이다. 
그 다음 아래의 명령어를 통해 로컬 환경에서 자신이 개발하는 블로그를 확인해 볼 수 있다.

```bash
$ jekyll serve
```

정상적으로 설치 되었다면 로컬서버 [http://localhost:4000/ ]({{"http://localhost:4000/"}}){:target="_blank"} 에서 확인하자.

![first-page](https://user-images.githubusercontent.com/62803763/127294147-7b1c13aa-6e30-4066-8e96-504d0ef6c4a0.PNG){: .align-center .open-new}

## 6. 불필요한 파일 삭제
Github에 commit하기 전에 본인이 clone한 폴더에서 불필요한 파일을 삭제한다.

![delete-file](https://user-images.githubusercontent.com/62803763/127295569-ea06e4f0-f4ae-47ce-ba1d-bc2ffc7b84d6.PNG){: .align-center .open-new}

**docs 폴더 :** post 샘플이 들어가 있으므로 백업해 놓는다.
{: .notice--danger}
**README.md :** 다시 작성하기 위해 삭제했다.
{: .notice--danger}

## 7. Github 연동
수정된 사항들을 깃헙에 "add-commit-push" 하여 반영한다.

```bash
$ git add .
$ git commit -m "commit message"
$ git push origin master
```

---
push가 완료되면 **[자신의 Github ID].github.io** 에서 블로그를 확인할 수 있다.