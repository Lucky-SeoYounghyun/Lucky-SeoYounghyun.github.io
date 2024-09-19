---
title: "[Jekyll] GitHub Blog 만들기! (06) - Chirpy 검색엔진 등록하기(2) // 작성중"
description: 
author:
date: 2024-09-06 19:00:00 +0900
categories: [Jekyll, search engine]
tags: [Chirpy, search]
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
Date : 2024 / 09 / 05 <br/>
필수 프로그램 : [GitHub Blog 만들기!(02)](https://lucky-seoyounghyun.github.io/posts/Jekyll-GitHub-Blog-%EB%A7%8C%EB%93%A4%EA%B8%B0-(02)-Chirpy-%EC%A0%81%EC%9A%A9/)까지 완료

<br/>

## **0. 들어가기에 앞서**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
이전 글에서는 google 서치콘솔을 사용하여 서치엔진에 등록하는 방법에대해서 알아보았습니다.  
이번에는 사용자가 보다 다양한 경로에서 블로그에 접근 할 수 있도록
다양한 서치엔진(naver, daum, bing)에 등록하는 방법에대해 알아보도록 하겠습니다.

<br/>

## **1. naver 등록**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

### 1.1) naver search advisor접속
[**naver search advisor**](https://searchadvisor.naver.com/)에 접속 후 아래 사진과 같이 `웹마스터 도구 사용하기`를 클릭합니다.
![Desktop View](/assets/img/20240906_post/naver_search_advisor_01.JPG){: width="800" height="400"}

### 1.2) URL 등록
아래 URL 기입부분에 블로그 링크를 넣어줍니다.
![Desktop View](/assets/img/20240906_post/naver_search_advisor_02.JPG){: width="800" height="400"}

### 1.3) 사이트 소유 확인
사이트 소유확인은 아래 사진과 같이 두가지 방법이 있습니다.  
![Desktop View](/assets/img/20240906_post/naver_search_advisor_03.JPG){: width="800" height="400"}

- HTML 파일 업로드  
  - 파일을 다운로드후 최상위 디렉토리인 `_config.yml`이 있는 폴더에 넣어줍니다.
- HTML 태그 복사  
  - 태그를 복사 후 `_includes` 폴더 안에있는 `head.html`에 복사하여줍니다.
    
파일을 업로드후 `소유확인`버튼을 클릭합니다.<sub>(본 포스팅에서는 HTML 파일 업로드 방식으로 진행하도록 하겠습니다.)</sub>  
요청이 완료되면 아래와 같은 팝업창이 뜨며 완료됩니다.
![Desktop View](/assets/img/20240906_post/naver_search_advisor_04.JPG){: width="400" height="400"}

### 1.4) sitemap.xml 등록
좌측 메뉴의 `요청` > `사이트맵 제출`을 클릭한 후 `블로그주소/sitemap.xml` 링크를 아래 사진과 같이 제출합니다.
![Desktop View](/assets/img/20240906_post/naver_search_advisor_05.JPG){: width="800" height="400"}

### 1.5) rss.xml 등록
이 단계를 하기전에는 아래와 같은 사전 준비가 필요합니다.  
1. [**Atom/RSS feed**](https://jekyllcodex.org/without-plugin/rss-feed/#)에 접속하여 feed.xml을 다운로드 해줍니다.  
2. 해당파일을 최상위 디렉토리인 `_config.yml`이 있는 폴더에 `다운로드한 feed.xml`을 `rss.xml`로 이름을 변경한 후 넣어줍니다.  

사전 준비가 완료되면 naver search advisor 좌측 메뉴의 `요청` > `RSS 제출`을 클릭한 후 `블로그주소/rss.xml` 링크를 아래 사진과 같이 제출합니다.
![Desktop View](/assets/img/20240906_post/naver_search_advisor_07.JPG){: width="800" height="400"}

<br/>

## **2. Daum 등록**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

### 1.1) Daum검색등록 접속
[**Daum 검색등록r**](https://register.search.daum.net/index.daum)에 접속 후 아래 사진과 같이 `신규등록하기`를 클릭합니다.
![Desktop View](/assets/img/20240906_post/Daum_검색등록_01.JPG){: width="800" height="400"}

### 1.2) URL 등록
아래 사진과 같이 블로그 등록 선택 후 https://부분을 제외한 블로그 링크를 입력하여줍니다.
![Desktop View](/assets/img/20240906_post/Daum_검색등록_02.JPG){: width="800" height="400"}

### 1.3) 절차진행
1.2단계까지 진행 후 안내대로 진행하면 아래와 같은 화면이 출력됩니다.
![Desktop View](/assets/img/20240906_post/Daum_검색등록_05.JPG){: width="800" height="400"}

<br/>

## **3. Bing 등록**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

### 1.1) bing webmasters 접속
bing등록은 google search console등록 완료를 기준으로 설명합니다.  

[**bing webmastersr**](https://www.bing.com/webmasters/about)에 접속 후 아래 사진과 같이 `시작하기`를 클릭합니다.
![Desktop View](/assets/img/20240906_post/bing_webmasters_01.JPG){: width="800" height="400"}

### 1.2) GSC에서 사이트 가져오기 클릭
아래 사진과 같이 GSC에서 사이트를 가져오기를 클릭합니다.
![Desktop View](/assets/img/20240906_post/bing_webmasters_02.JPG){: width="800" height="400"}

### 1.3) 절차 진행
1.2단계까지 진행 후 안내대로 진행하면 아래와 같은 화면이 출력됩니다.
![Desktop View](/assets/img/20240906_post/bing_webmasters_03.JPG){: width="800" height="400"}

<br/>

## **글을 마무리하며**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

2편에 걸쳐서 보다 많은 사용자가 블로그로 유입될 수 있도록 다양한 서치엔진에 블로그를 등록하는 방법을 알아보았습니다.  
본 블로그에서 설명하지않은 다양한 검색엔진에 블로그를 등록하는 방법이 있을 수 있으며, 해당 방법을 찾아나가는것도 하나의 즐거움이 될 수 있습니다.  
다음 포스팅에서는 블로그 통계 및 분석을 할 수 있는 google analytics를 활용하는 방법을 설명드리도록 하겠습니다.  
혹시 궁금한점이 있으시면 댓글로 남겨주시면 확인하도록 하겠습니다!

이만 가보겠습니다!

<br/>