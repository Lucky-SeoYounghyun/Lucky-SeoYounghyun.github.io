---
title: "[Jekyll] GitHub Blog 만들기! (02) - Chirpy 적용"
description: 
author:
date: 2024-09-02 18:00:00 +0900
categories: [Jekyll, Chirpy]
tags: [Chirpy]
pin: false
math: true
mermaid: true
# image:
#   path: /assets/img/20240912_post/KT_모집요강.jpg
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: .
---

## **개발환경**
>OS : windows 10 <br/>
Date : 2024 / 09 / 01 <br/>
필수 프로그램 : Ruby, node.js, git <br/>
프로그램이 설치 되어있지 않으신분들은 [이전게시글](https://lucky-seoyounghyun.github.io/posts/Jekyll-GitHub-Blog-%EB%A7%8C%EB%93%A4%EA%B8%B0-(01)-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD-%EC%84%A4%EC%A0%95/)을 참고 부탁드리겠습니다.


<br/>

## **0. 들어가기에 앞서**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
많은분들이 블로그를 만들기전에 다양한 블로그를 고민할것입니다.  
저도 Tstory, Velog 등 다양한 블로그를 고민하다가 Github Blog로 정착하게 되었습니다.  
그 과정에서 겪은 다양한 오류들을 공유하고자 이 글을 작성합니다.  

<br/>

## **1. 테마선정**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
github blog에 적용할 수 있는 다양한 테마가 존재하며 이는 아래 사이트들에서 확인 가능합니다.  
- <http://jekyllthemes.org/>  
- <https://jekyllthemes.io/>  
- <https://jekyll-themes.com/>  

이외에도 다양한 사이트에서 테마를 선택할 수 있습니다.  
하지만 본 포스팅에서는 [**Chirpy**](https://chirpy.cotes.page) 테마를 설명해드리고자 합니다.

<br/>

## **2. Chirpy 설치**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

### **2.1) 테마 적용방법**
Chirpy를 이용한 블로그 개설은 세가지 방법이 있습니다.
1. Chirpy에서 zip로 직접 다운로드 받는 방법
2. Chirpy에서 저장소로 Fork하는방법
3. chirpy starter를 통해 직접 설치하는 방법

본 블로그에서는 2번 Fork를 통해 설치하는 방법을 설명해드리도록 하겠습니다.

<br/>

### **2.2) Chirpy Fork**
[**Chirpy Fork**](https://github.com/cotes2020/jekyll-theme-chirpy/fork)에서 그림과같이 fork를 하여 내 Repository로 가져옵니다.

![Desktop View](/assets/img/20240902_post/chirpy_fork.JPG){: width="800" height="400"}

> 저장소 이름은 {UserName.github.io}로 지정해주시기 바랍니다. 추후 수정가능하지만 한번에 하기위함입니다.
{: .prompt-warning }

<br/>

### **2.3) Default Branch 변경**
 Repository - Setting - Default Branch에서 master를 `main`으로 변경하여줍니다.
 
![Desktop View](/assets/img/20240902_post/brach_main.JPG){: width="800" height="400"}

<br/>

### **2.4) page 변경**
1. Repository - Setting - Pages - Source를 `GitHub Actions` 로 바꿔줍니다. 
 
![Desktop View](/assets/img/20240902_post/page_setting_01.JPG){: width="800" height="400"}

2. `Configure` 를 클릭해줍니다.. 
 
![Desktop View](/assets/img/20240902_post/page_setting_02.JPG){: width="800" height="400"}

2. 변경사항 없이 `Sign off and commit changes` 를 클릭해줍니다.. 
 
![Desktop View](/assets/img/20240902_post/page_setting_03.JPG){: width="800" height="400"}

<br/>

### **2.5) Local Clone**
CMD에서 원하는 경로로 git clone 합니다. <br/>

```batch
cd "원하는 폴더 경로"
git clone "Repository HTTPS 링크"
```
HTTPS 링크는 이미지와 같습니다.
![Desktop View](/assets/img/20240902_post/git_https_link.JPG){: width="800" height="400"}

<br/>

### **2.6) chirpy 업데이트** <span style="font-size: 16px;">// 이전에 clone 하신분들만 해당</span>
[**Chirpy 업데이트**](https://github.com/cotes2020/jekyll-theme-chirpy/tags)에서 최신 파일을 다운받아 압 축 해제 후 전체 붙여넣기를 합니다.


### **2.7 각종 모듈 설치**

```batch
cd "원하는 폴더 경로"
bundle
npm install && npm run build
```
아래와같이 뜨면 정상적으로 철치가 완료된것입니다.
![Desktop View](/assets/img/20240902_post/bundle.JPG){: width="800" height="400"}
![Desktop View](/assets/img/20240902_post/npm install & npm run build.JPG){: width="800" height="400"}
<br/>

### **2.8 로컬에서 실행해보기**

```batch
jekyll serve
```

이후 주소창에 <a href=" http://127.0.0.1:4000/" target="_blank">**http://127.0.0.1:4000/**</a> 를 입력한 후 아래와 같이 뜨면 성공입니다.<br/>

이후 기능을 테스트 해보며 정상작동하는지 확인해줍니다.

![Desktop View](/assets/img/20240902_post/success.JPG){: width="800" height="400"}

> jekyll serve가 작동하지 않으시는분은 `gem install jekyll`를 입력해보시기 바랍니다.
{: .prompt-warning }

<br/>

### **2.9 gitignore 주석처리하기**
gitignore 파일을 열어 해당부분 주석처리를 해줍니다. 

```
# Misc
# _sass/dist
# assets/js/dist
```

## **3. git 배포**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

이제 모든 설치가 완료되었으며 이를 git에 반영해주어야 합니다.<br/>
보통은 아래와 같은 메시지를 입력할것입니다.

```batch
git add -A
git commit -m "first_commit"
git push
```

하지만 이와같이 입력시 아래와같은 에러메시지가 출력됩니다.

![Desktop View](/assets/img/20240902_post/commit_err.JPG){: width="800" height="400"}

이는 Conventional commits 규칙이 설정되어 허용되는 타입만 커밋메시지를 입력받겠다는 의미입니다.

이를 해결하기 위한 방법은 두가지 있습니다.

### **3.1 feat**
첫번째는 단순하게 feat를 활용하여 커밋 메시지를 작성해주는 방법입니다.
```batch
git add -A
git commit -m "feat: first_commit"
git push
```
이러면 아래와 같이 정상적으로 커밋이 완료됩니다.

![Desktop View](/assets/img/20240902_post/commit_err_feat.JPG){: width="800" height="400"}

<br/>

### **3.2 husky 주석처리**
두번째로는 규칙에 주석처리를 해주는 방법입니다.<br/>
이를 위해서 `.husky`폴더에서 `commit-msg`파일을 txt로 열어줍니다.<br/>
이후 아래와 같이 주석처리를 해준 후 저장한 합니다.

```
# npx --no -- commitlint --edit $1
```
이후 다음과 같이 commit하면 처음과는 다르게 정상적으로 commit가 되는것을 볼 수 있습니다.

```batch
git add -A
git commit -m "first_commit"
git push
```
<br/>

### **3.3 Actions 확인**
정상적으로 git에 올랐는지 확인하려면 아래와같이 `Repository - Actions` 에서 확인 가능합니다.
![Desktop View](/assets/img/20240902_post/workflow.JPG){: width="800" height="400"}

## **4. 최종확인**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

블로그가 정확히 작동하는지 링크에 들어가 확인해줍니다.<br/>
정상적인 commit완료후 반영이 되기까지 10분정도 소요가 될 수 있습니다.
![Desktop View](/assets/img/20240902_post/success_final.JPG){: width="800" height="400"}

<br/>

## **글을 마무리하며**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

이번 포스팅에서는 본격적으로 Chirpy를 활용한 Github blog를 만드는 방법에대해 설명하였습니다.<br/>
다음 포스팅에서는 블로그 커스터마이징에 대해서 설명하고자합니다.<br/>
혹시 본 글을 참조하면서 블로그를 만드는 과정에서 오류가 발생하시는 분들께서는 댓글 달아주시면 확인해보도록 하겠습니다.

이만 가보겠습니다!

<br/>

## **참조**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
<a href="https://github.com/cotes2020/jekyll-theme-chirpy/wiki/Upgrade-Guide" target="_blank">Chirpy Upgrade-Guide</a><br/>

<a href="https://www.irgroup.org/posts/jekyll-chirpy/" target="_blank">하얀눈길 블로그</a><br/>

<a href="https://jjikin.com/posts/Jekyll-Chirpy-%ED%85%8C%EB%A7%88%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-Github-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0(2023-6%EC%9B%94-%EA%B8%B0%EC%A4%80)/" target="_blank">JJIKIN</a>
