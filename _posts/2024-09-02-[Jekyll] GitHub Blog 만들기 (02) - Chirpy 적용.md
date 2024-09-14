---
title: "[Jekyll] GitHub Blog 만들기! (02) - Chirpy 적용"
description: 
author:
date: 2024-09-02 18:00:00 +0900
categories: [Jekyll, 환경설정]
tags: [Chirpy]
pin: true
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
필수 프로그램 : Ruby, node.js, git

<br/>

## **0. 들어가기에 앞서**
많은분들이 블로그를 만들기전에 다양한 블로그를 고민할것입니다.  
저도 Tstory, Velog 등 다양한 블로그를 고민하다가 Github Blog로 정착하게 되었습니다.  
그 과정에서 겪은 다양한 오류들을 공유하고자 이 글을 작성합니다.  

<br/>

## **1. 테마선정**
github blog에 적용할 수 있는 다양한 테마가 존재하며 이는 아래 사이트들에서 확인 가능합니다.  
- <http://jekyllthemes.org/>  
- <https://jekyllthemes.io/>  
- <https://jekyll-themes.com/>  

이외에도 다양한 사이트에서 테마를 선택할 수 있습니다.  
하지만 본 포스팅에서는 [**Chirpy**](https://chirpy.cotes.page) 테마를 설명해드리고자 합니다.

<br/>

## **2. Chirpy 설치방법**
Chirpy를 이용한 블로그 개설은 세가지 방법이 있습니다.
1. Chirpy에서 zip로 직접 다운로드 받는 방법
2. Chirpy에서 저장소로 Fork하는방법
3. chirpy starter를 통해 직접 설치하는 방법

본 블로그에서는 2번 Fork를 통해 설치하는 방법을 설명해드리도록 하겠습니다.

<br/>

## **3. Chirpy Fork**
[**링크**](https://github.com/cotes2020/jekyll-theme-chirpy/fork)에서 그림과같이 fork를 하여 내 Repository로 가져옵니다.
> 저장소 이름은 {UserName.github.io}로 지정해주시기 바랍니다. 추후 수정가능하지만 한번에 하기위함입니다.
{: .prompt-warning }

<br/>

## **4 Default Branch 변경**
 Repository - Setting - Default Branch를 main으로 변경하여줍니다.
 
<br/>

## **5 Local Clone**
CMD에서 원하는 경로로 git clone 합니다.

```batch
cd "원하는 폴더 경로"
git clone "Repository HTTPS 링크"
```

<br/>

## **6 chirpy 업데이트 // 이전에 clone 하신분들만 해당**
[**링크**](https://github.com/cotes2020/jekyll-theme-chirpy/fork)에서 최신 파일을 다운받아 압 축 해제 후 전체 붙여넣기를 합니다.

## 각종 모듈 설치

```batch
cd "원하는 폴더 경로"
bundle
npm install && npm run build
```

<br/>

## **commit msg 변경**
마무리하고 commit 를 하면 다음과 같은 오류 메시지를 볼 수 있습니다.
이를 해결하는 방법은 2가지입니다.

<br/>

## **Branch 변경**
 Repository - Setting - Pages - Source를 GitHub Actions 로 바꿔줍니다.

<br/>

## **참고**
Chirpy Upgrade-Guide : https://github.com/cotes2020/jekyll-theme-chirpy/wiki/Upgrade-Guide
Jekyll Chirpy 테마 사용하여 블로그 만들기 : https://www.irgroup.org/posts/jekyll-chirpy/`
Jekyll Chirpy(v6.0.1) 테마를 활용한 Github 블로그 만들기(2023.6 기준) : https://jjikin.com/posts/Jekyll-Chirpy-%ED%85%8C%EB%A7%88%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-Github-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0(2023-6%EC%9B%94-%EA%B8%B0%EC%A4%80)/