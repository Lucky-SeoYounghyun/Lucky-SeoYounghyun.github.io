---
title: "[Jekyll] GitHub Blog 만들기! (07) - Chirpy google analytics 등록"
description: 
author:
date: 2024-09-07 19:00:00 +0900
categoranalyticsies: [Jekyll, analytics]
tags: [Chirpy, analytics]
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
Date : 2024 / 09 / 07 <br/>
필수 프로그램 : [GitHub Blog 만들기!(02)](https://lucky-seoyounghyun.github.io/posts/Jekyll-GitHub-Blog-%EB%A7%8C%EB%93%A4%EA%B8%B0-(02)-Chirpy-%EC%A0%81%EC%9A%A9/)까지 완료

<br/>

## **0. 들어가기에 앞서**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
이전 글에서는 서치엔진을 통하여 등록하는 방법에대해서 알아보았습니다.  
이번 글에서는 블로그의 유입경로와 활성정도등을 분석할 수 있는 google analytics를 github blog에 연동하는 방법에 대해서 알아보도록 하겠습니다.

<br/>

## **1. google analytics 란 무엇인가?**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

git blog는 자유도가 높은만큼 셋팅을 해주지않으면 불친절한게 현실입니다.
다른 블로그들은 하루 방문자수, 유입경로 등을 분석하여 보다 양질의 개시글을 만들 수 있도록 서포트 해주고있습니다.
일반 사용자들이 이런 데이터들을 수집하고 분석할 수 있도록 제공해주는 툴이 google analytics라고 할 수 있습니다.

<br/>

## **2. google analytics 등록**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

### 2.1) 계정 생성
[**google analytics**](https://analytics.google.com/analytics/web)에 들어갑니다.  
이후 가운데에있는 `측정하기` 버튼을 클릭합니다.
그러면 아래와 같은 창으로 넘어갑니다.  
해당 단계에서는 계정 이름을 적은 후 다음 버튼을 클릭합니다.
![Desktop View](/assets/img/20240907_post/analytics_02.JPG){: width="800" height="400"}

### 2.2) 속성 만들기
본인 사이트 주소를 아래 사진과 같이 입력한 후 시간대와 통화를 원하는 속성으로 선택한 후 다음 버튼을 클릭합니다.
![Desktop View](/assets/img/20240907_post/analytics_03.JPG){: width="800" height="400"}

### 2.3) 비즈니스 세부정보
비즈니스 세부정보는 개인이므로 `작음`을 선택 후 다음 버튼을 클릭합니다.
![Desktop View](/assets/img/20240907_post/analytics_04.JPG){: width="800" height="400"}

### 2.4) 비즈니스 세부목표
비즈니스 목표또한 원하는 세부사항을 선택 후 만들기 버튼을 클릭합니다.
![Desktop View](/assets/img/20240907_post/analytics_05.JPG){: width="800" height="400"}

### 2.5) 데이터 수집
저희는 웹을 분석할것이므로 플랫폼으로 웹을 선택합니다.
![Desktop View](/assets/img/20240907_post/analytics_06.JPG){: width="800" height="400"}

### 2.6) 데이터 스트림 설정
웹사이트 URL을 입력 후 스트림 이름은 원하는 이름으로 설정합니다.
![Desktop View](/assets/img/20240907_post/analytics_07.JPG){: width="800" height="400"}

### 2.7) 데이터 스트림 설정
웹사이트 URL을 입력 후 스트림 이름은 원하는 이름으로 설정합니다.
![Desktop View](/assets/img/20240907_post/analytics_07.JPG){: width="800" height="400"}

### 2.8) 웹 스트림 세부정보
웹 스트림 세부정보를 닫으셨으면 `관리` > `데이터 수집 및 수정` > `데이터 스트림` > `원하는 정보 클릭` 하시면 볼 수 있습니다.
웹 스트림 세부 정보에서 측정 ID 값을
![Desktop View](/assets/img/20240907_post/analytics_09.JPG){: width="800" height="400"}
복사한 태그 부분중 content 부분을 `_config.yml`의 `Web Analytics Settings`부분에 복사하여 줍니다.

```html
# Web Analytics Settings
analytics:
  google:
    id: #복사한 ID값
```

### 2.8) 완료
셋팅을 완료하면 다음과 같은 화면이 뜨면 성공입니다.
![Desktop View](/assets/img/20240907_post/analytics_10.JPG){: width="800" height="400"}
잠시 기다리면 아래와 같은 화면이 뜨며 정보 수집 결과가 나오기 시작합니다.
![Desktop View](/assets/img/20240907_post/analytics_11.JPG){: width="800" height="400"}

<br/>

## **글을 마무리하며**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

이번 포스팅에서는 블로그를 보다 효율적으로 관리할 수 있도록 다양한 기능을 제공해주는 google analtice를 github blog에 연동하는 방법에대해 알아보았습니다.  
다음에는 기회가되면 GA의 다양한 사용방법에대해서 설명한 게시글을 올리도록 하겠습니다.  
혹시 궁금한점이 있으시면 댓글로 남겨주시면 확인하도록 하겠습니다!  

이만 가보겠습니다!

<br/>