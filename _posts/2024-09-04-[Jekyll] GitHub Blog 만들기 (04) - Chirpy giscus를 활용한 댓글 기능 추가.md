---
title: "[Jekyll] GitHub Blog 만들기! (04) - Chirpy giscus를 활용한 댓글 기능 추가 // 작성중"
description: 
author:
date: 2024-09-04 19:00:00 +0900
categories: [Jekyll, Chirpy]
tags: [Chirpy, giscus, 댓글기능]
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
필수 프로그램 : [GitHub Blog 만들기!(02)](https://lucky-seoyounghyun.github.io/posts/Jekyll-GitHub-Blog-%EB%A7%8C%EB%93%A4%EA%B8%B0-(02)-Chirpy-%EC%A0%81%EC%9A%A9/)까지 완료

<br/>

## **0. 들어가기에 앞서**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
이전 글에서는 블로그를 다양하게 커스터마이징 하는 방법에대해서 알아보았습니다.  
블로그를 보고 궁금한것을 물어보거나 작성자와 의사소통하는 방법중 가장 대표적인 기능이 댓글 기능입니다.  
여러 댓글 기능을 알아보고 해당 기능을 사용하는 방법에대해 알아보고자 합니다.

<br/>

## **1. 다양한 댓글 기능 프로그램**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

### 1.1) <a href="https://disqus.com/" target="_blank">Disqus</a>
- 특징
  - 소셜 댓글기능을 지원한다.
- 장점
  - 회원가입이 필요없으며 SNS계정만 있으면 댓글을 달 수 있다.
- 단점
  - 무겁다.
  - 무료버전 사용시 광고가 기본설정되어있다.

### 1.2) <a href="https://github.com/utterance/utterances" target="_blank">Utterances</a>
- 특징
  - git의 Issue 기능을 이용하여 댓글기능을 지원한다.
- 장점
  - 가볍다.
  - 광고가 없다.
- 단점
  - git로그인만을 지원한다

### 1.3) <a href="https://github.com/apps/giscus" target="_blank">Giscus</a>
- 특징
  - git의 Discussions 기능을 이용하여 댓글기능을 지원한다.
- 장점
  - 가볍다.
  - 광고가 없다.
  - 대댓글 기능을 지원한다.
- 단점
  - git로그인만을 지원한다

이 외에도 다양한 차이점이 존재합니다.  
이중 본 블로그에서는 광고도 없으며 기능도 다양한 **Giscus**를 활용한 댓글 기능 구현을 다루도록 하겠습니다.
  
<br/>

## **2. 설치 방법**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

### 2.1) Blog Repositorie에 giscus를 설치
- [**설치링크**](https://realfavicongenerator.net/)에 접속하여 아래 사진과 같이 install 버튼을 눌러줍니다.

![Desktop View](/assets/img/20240904_post/install.JPG){: width="800" height="400"}

- Only select repositories를 클릭후 아래 사진과 같이 블로그 Repositorie를 선택 후 insatll을 눌러줍니다.

![Desktop View](/assets/img/20240904_post/repositories.JPG){: width="800" height="400"}

### 2.2) Repositorie 셋팅
- settings에 들어가 휠을 내리다보면 Features에 아래 그림과 같은 Discussions가 보입니다. 이를 체크해줍니다.

![Desktop View](/assets/img/20240904_post/Discussions.JPG){: width="800" height="400"}

- 상위 메뉴에 Discussions가 생성된 모습을 볼 수 있습니다.

![Desktop View](/assets/img/20240904_post/menu.JPG){: width="800" height="400"}

### 2.3) giscus 추가
- [**정보 확인링크**](https://giscus.app/ko)에 들어가서 아래 사진과 같이 설정해준다.

![Desktop View](/assets/img/20240904_post/setting.JPG){: width="800" height="400"}

> `저장소 주소와`, `Discussion 카테고리`만 주의하여 설정해주신 후 나머지는 원하시는 설정으로 하시면 됩니다.
{: .prompt-warning }

- 이후 그 아래에 `giscus 사용` 값들을 참고하여 `_congig.yml`파일을 수정하여 준다.

```yaml
comments:
  # Global switch for the post-comment system. Keeping it empty means disabled.
  provider: giscus // 이부분 수정
  # The provider options are as follows:
  disqus:
    shortname: # fill with the Disqus shortname. › https://help.disqus.com/en/articles/1717111-what-s-a-shortname
  # utterances settings › https://utteranc.es/
  utterances:
    repo: # <gh-username>/<repo>
    issue_term: # < url | pathname | title | ...>
  # Giscus options › https://giscus.app
  giscus:
    repo: // 깃허브 저장소 위치
    repo_id: // 저장소 고유 ID
    category: // 카테고리 설정
    category_id: // 원하는 카테고리 ID
    mapping: // 댓글을 어느 방식으로 페이지에 연결할지
    strict: // 매핑모드 설정
    input_position: // 댓글창 위치 지정
    lang: // 언어 지정
    reactions_enabled: // 이모지를 사용할것인지 설정
```

### 2.4) 확인
아래 명령어를 입력하여 로컬에서 아래 사진과 같이 동작하는지 확인한 후 git에 commit해주면 끝입니다.
```
jekyll serve
```
![Desktop View](/assets/img/20240904_post/success.JPG){: width="800" height="400"}

<br/>

## **글을 마무리하며**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

이번 포스팅에서는 giscus를 활용한 블로그 댓글 기능 추가 방법을 알아보았습니다.
이 외에도 다른 방법으로 댓글 기능을 구현할 수 있으며 원하시는 댓글창을 구현하실 수 있으십니다.  
다음 포스팅에서는 블로그 통계 및 분석을 할 수 있는 google analytics를 활용하는 방법을 설명드리도록 하겠습니다!  
혹시 궁금한점이 있으시면 댓글로 남겨주시면 확인하도록 하겠습니다!

이만 가보겠습니다!

<br/>