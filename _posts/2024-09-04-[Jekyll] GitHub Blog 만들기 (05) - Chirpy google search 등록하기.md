---
title: "[Jekyll] GitHub Blog 만들기! (05) - Chirpy 검색엔진 등록하기(1) // 작성중"
description: 
author:
date: 2024-09-05 19:00:00 +0900
categories: [Jekyll, search engine]
tags: [Chirpy, search, google]
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
이전 글에서는 giscus를 활용하여 댓글기능을 만드는 방법에대해서 알아보았습니다.  
블로그를 만들었으면 이제 많은 사람들이 찾아올 수 있게 만들어야합니다.
이를 위해 google 서치콘솔에 블로그를 등록하는 방법을 알아보고자 합니다.

<br/>

## **1. google search console 등록**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

### **1.1) URL등록**  
[**google search console**](https://search.google.com/search-console/welcome)에 들어갑니다.  
이후 아래와 같은 화면에서 오른쪽 URL 접두어 부분에 URL을 입력합니다.

![Desktop View](/assets/img/20240904_post/search_console_01.JPG){: width="800" height="400"}

### **1.2) 소유권 확인**  
아래 이미지에서 HTML 태그 부분을 클릭후 content부분을 복사하여 줍니다.

![Desktop View](/assets/img/20240904_post/search_console_02.JPG){: width="800" height="400"}

### **1.3) 메타태그 등록**  
아래 이미지에서 HTML 태그 부분을 클릭후 복사하여 줍니다.

![Desktop View](/assets/img/20240904_post/search_console_02.JPG){: width="800" height="400"}
해당 링크를 이용하여 소유권을 확인하는 방법은 아래와같이 두가지가 있습니다.
- **header 부분에 직접 넣기**  
복사한 아래 태그를 `head.html`에 직접 삽입하기

```html
<meta name="google-site-verification" content="~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~" />
```
- **chirpy에서 제공하는 기능 이용하기**  
복사한 태그 부분중 content 부분을 `_config.yml`의 `webmaster_verifications`부분에 복사하여 줍니다.

```html
webmaster_verifications:
  google: ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```

### **1.4) 소유권 확인**
메타 태그를 등록한 후 git에 commit까지 완료하였으면 다시 google search console로 돌아와 확인을 눌러줍니다.  
그러면 아래 사진과 같이 소유권 확인이 완료됩니다.
![Desktop View](/assets/img/20240904_post/search_console_03.JPG){: width="800" height="400"}

### **1.5) sitemap.xml등록**
이제 속성확인을 클릭한 후 왼쪽 메뉴에 Sitemaps를 클릭하면 아래 사진과 같은 사이트에 들어가게 됩니다.
새 사이트맵 추가에 `sitemap.xml`을 입력한 후 제출을 클릭합니다.
![Desktop View](/assets/img/20240904_post/search_console_04.JPG){: width="800" height="400"}

조금 기다리면 제출이 완료되며 아래 사진과 같이 전환이 되면 성공입니다.
![Desktop View](/assets/img/20240904_post/search_console_05.JPG){: width="800" height="400"}

### **1.6) 자주하는 질문**
- 인터넷에서 검색이 안되요!
  - 정상적입니다. 몇일 기다리다보면 등록이 완료됩니다.
- `sitemap.xml`상태가 `가져올 수 없음`이라고 떠요!
  - 상태이상처럼 보이나 단순 버그일 가능성이 큽니다.
- 새로운 개시글을 등록하였으나 페이지 색인이 안됩니다 ㅠㅜ
  - 구글 봇이 실시간으로 바로 검색을 반영하지 않아서 그렇습니다.  
  급하신 분들은 `google search console 좌측 메뉴`에 `URL검사`에 직접 해당 게시글 링크를 입력후 색인 요청을 하면 됩니다.

<br/>

## **글을 마무리하며**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

이번 포스팅에서는 google search console를 통해 google에서 블로그를 검색할 수 있도록 하는 방법에 대해서 알아보았습니다.
다음 포스팅에서는 naver, daum, bing에서 블로그를 검색할 수 있도록 등록하는 방법을 설명해드리도록 하겠습니다!
혹시 궁금한점이 있으시면 댓글로 남겨주시면 확인하도록 하겠습니다!

이만 가보겠습니다!

<br/>