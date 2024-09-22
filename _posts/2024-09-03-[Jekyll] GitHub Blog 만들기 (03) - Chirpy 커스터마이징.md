---
title: "[Jekyll] GitHub Blog 만들기! (03) - Chirpy 커스터마이징"
description: 
author:
date: 2024-09-03 18:00:00 +0900
categories: [Jekyll, Chirpy]
tags: [Chirpy, 커스터마이징]
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
필수 프로그램 : [GitHub Blog 만들기!(02)](https://lucky-seoyounghyun.github.io/posts/Jekyll-GitHub-Blog-%EB%A7%8C%EB%93%A4%EA%B8%B0-(02)-Chirpy-%EC%A0%81%EC%9A%A9/)까지 완료

<br/>

## **0. 들어가기에 앞서**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
이전 글에서는 Chirpy를 적용하여 블로그를 만들어보았습니다.  
제가 github blog로 정착한 가장 큰 이유중 한개는 다양한 커스터마이징 기능 구현 가능입니다.  
이번에는 Chirpy의 다양한 기능들을 알아보고 원하는 대로 커스터마이징 하는 방법을 알아보고자합니다.

<br/>

## **1. 기본적인 파일 설명**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

chirpy에는 다양한 커스텀 기능들을 구현할 수 있습니다.  
이번 포스팅에서 사용하는 파일들을 위주로 설명하였습니다.  

- `_config.yml` : 변수 명이 미리 설정되있고 해당 변수들에 값을 지정해주는 파일이라고 할 수 있습니다.  
- `.husky` : 이전 글에 설명드렸다싶이 commit 설정을 할 수 있습니다.
- `_data` : 사용자 정보 및 공유버튼의 구성을 변경 할 수 있습니다. 
  - `contact.yml` : 사이드바의 하단의 아이콘을 변경합니다.  
- `_includes` : 다양한 UI를 수정할 수 있는 파일이 있습니다. 대부분 모듈화되어있어 수정이 용이합니다.  
  - `sidebar.html` : 좌측 배너의 레이아웃 디자인이 지정되어있습니다.
- `_layouts` : 블로그 디자인의 전반적인 수정을 할 수 있습니다.
- `_sass` : 블로그 css파일들이 저장되어있어 다양한 커스터마이징 파일들이 있습니다.
  - `commons.scss` : 사이드바의 폰트 및 디자인을 수정할 수 있습니다.  
  - `variables.scss` : 사이드바의 크기를 조절할 수 있습니다.  
  - `typography-light.scss` : light테마에서의 색상들이 저장되어있습니다.
  - `typography-dark.scss` : light테마에서의 색상들이 저장되어있습니다.
- `_tabs` : 왼쪽 메뉴구성에대한 랜딩페이지가 있습니다.
- `assets` : 주로 이미지 저장을 하는 용도로 많이보게될 폴더입니다.

<br/>

## **2. 사용자 정보 수정**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

- 기본적인 사용자 정보들을 등록해줍니다.  
위치 : `authors.yml`
```css
cotes:
  name: user name  
  twitter: user name  
  url: https://github.com/user name/
```
위치 : `_config.yml`
```css
cotes:
  lang: ko
  timezone: Asia/Seoul
  description: 블로그 설명
  url: "https://{user name}.github.io" // 마지막 /를 제외해야합니다.
  github:
    username: {user name}
  social:
    name: {user name}
    email: {user name}@gmail.com
    links:
    https://github.com/{user name}
  theme_mode: # [light | dark] // 모드를 선택할 수 있습니다.
  paginate: 10 // 한 페이지에 표시할 게시글 수 입니다.
```


<br/>

## **3. 좌측 배너(side-bar) 수정**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

좌측 배너는 블로그에 들어왔을때 가장 많이 보이는 부분이자 가장 많은 정보가 밀집되어있는 부분입니다.  
이에 다양한 커스터마이징을 시도하고 정보를 제공할 수 있는 기능을 합니다.

<br/>

### **3.1) Avatar 수정**

- cdn과 avatar 부분을 수정해줍니다.  
위치 : `_config.yml`
```yaml
cdn: "https://{블로그 주소}.github.io" # 블로그 주소를 입력해줍니다.
```
```yaml
avatar: "/assets/img/avatar.jpg" # 원하는 avatar이미지를 해당 경로에 저장해줍니다.
```

<br/>

### **3.2) 블로그 이름(site-title) 수정**
- title를 원하는 이름으로 설정합니다.  
위치 : `_config.yml`
```yaml
title: main title # the main title
```

- title의 크기를 수정합니다.  
font-size등을 수정하여주시면 됩니다.  
위치 : `commons.scss`
```css
.site-title {
    font-family: inherit;
    font-weight: 1000;
    font-size: 2.20rem;
    line-height: 1.2;
    letter-spacing: 0.25px;
    margin-top: 1.25rem;
    margin-bottom: -0.25rem;

    a {
      @extend %clickable-transition;
      @extend %sidebar-link-hover;

      color: var(--site-title-color);
    }
  }
```

<br/>

### **3.3) 상태 메시지(sub-title) 수정**
- 상태메시지를 수정합니다.  
위치 : `_config.yml`
```yaml
tagline: sub-title # it will display as the subtitle
```

- 기울기 등을 수정하고 싶으면 아래 파일을 수정합니다.  
기울기 수정은 fst-italic를 수정하면 됩니다.  
위치 : `sidebar.html`
```html
    <p class="site-subtitle fst-italic mb-0">{{ "site.tagline" }}</p>
```

<br/>

### **3.4) 사이드바에 배경 색상 변경 및 이미지 넣기**
- light 테마시 이미지 및 색상 조정은 아래 파일을 수정합니다.  
`typography-light.scss`
```css
  --sidebar-bg: #f6f8fa; // 색상 코드 입력
```
```css
  --sidebar-bg: url('https://{블로그 주소}.github.io/assets/img/backgroundimg'); // 이미지 url 입력
```

- dark 테마시 이미지 및 색상 조정은 아래 파일을 수정합니다.  
`typography-dark.scss`
```css
  --sidebar-bg: #1e1e1e; // 색상 코드 입력
```
```css
  --sidebar-bg: url('https://{블로그 주소}.github.io/assets/img/backgroundimg'); // 이미지 url 입력
```

<br/>

### **3.5) 사이드바 크기 수정**
- 사이드 바의 가로 크기를 조정합니다.  
`variables.scss`
```css
$sidebar-width: 260px !default;
$sidebar-width-large: 350px !default; 
```

<br/>

## **5. favicon 수정**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;">
파비콘이란 블로그의 대표 이미지라고 할 수 있습니다. 아래 이미지와 같이 주소 옆에 보이는 작은 이미지 등을 말합니다.  
![Desktop View](/assets/img/20240903_post/favicon_01.JPG){: width="800" height="400" .w-50}
![Desktop View](/assets/img/20240903_post/favicon_02.JPG){: width="800" height="400" .w-75}

[**realfavicongenerator**](https://realfavicongenerator.net/)에서 원하는 이미지로 favicon을 만든 후 다운로드 합니다.  
압축 해재 후 `browserconfig.xml`와 `site.webmanifest`를 삭제해줍니다.  
그리고 남은 이미지 파일들을 `assets/img/favicons` 폴더에 넣어줍니다.

<br/>

## **글을 마무리하며**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

이번 포스팅에서는 chirpy를 활용한 GitHub블로그 커스터마이징에대해 정리해보았습니다.  
알려드린 기능 이외에도 다양한 기능이 존재하며, 자유도가 상당히 높은 커스터마이징이 가능합니다.  
다음 포스팅에서는 댓글 기능 사용방법에대해 설명드리도록 하겠습니다!  
혹시 궁금한점이 있으시면 댓글로 남겨주시면 확인하도록 하겠습니다!

이만 가보겠습니다!

<br/>

## **참조**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

<a href="https://www.irgroup.org/posts/Chirpy-%ED%85%8C%EB%A7%88-%EC%BB%A4%EC%8A%A4%ED%84%B0%EB%A7%88%EC%9D%B4%EC%A7%95/" target="_blank">하얀눈길 블로그</a><br/>
