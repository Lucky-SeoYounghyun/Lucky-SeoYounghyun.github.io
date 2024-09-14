---
title: "[Jekyll] GitHub Blog 만들기! (01) - 개발 환경 설정"
description: 
author:
date: 2024-09-01 11:33:00 +0900
categories: [Jekyll, 환경설정]
tags: [Ruby, Node.js]
pin: true
math: true
mermaid: true
# image:
#   path: /assets/img/20240912_post/KT_모집요강.jpg
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: .
---

## **개발환경**
> OS : windows 10<br/>
Date : 2024 / 09 / 01

## **0. 들어가기에 앞서**
GitBlog 와 테마를 보다 효율적으로 사용하기위해 이번 글에서는 Ruby 설치와 jekyll설치를 하고자합니다.<br/>
모든 프로그램을 설치후 컴퓨터를 재부팅 해주어야 프로그램이 정상 작동합니다.

## **1. Ruby 설치**
[**Ruby**](https://rubyinstaller.org/downloads/archives/)에서 Ruby+Devkit 3.1.2-1 (x64)를 설치하여 주시기바랍니다.
> 현재 Ruby+Devkit 3.1.2-1 (x64)가 아닌 다른 버전을 설치하면 아래와 같은 에러가 발생하는것을 발견하였습니다.<br/>
Could not find gem 'wdm (~> 0.1.1) mingw, x64_mingw, mswin' in locally installed gems.
{: .prompt-warning }
1. 다운로드
![Desktop View](/assets/img/20240901_post/Ruby_설치.PNG){: width="800" height="400"}

2. accept하고 Next를 눌러줍니다.
![Desktop View](/assets/img/20240901_post/Ruby_install_01.JPG){: width="800" height="400"}

3. 경로 지정 및 PATH 등록을 선택해줍니다, 연결프로그램 등록을 해줍니다.
![Desktop View](/assets/img/20240901_post/Ruby_install_02.JPG){: width="800" height="400"}

4. 추가 컴포넌트를 체크해줍니다.
![Desktop View](/assets/img/20240901_post/Ruby_install_03.JPG){: width="800" height="400"}

5. 실행 체크 후 종료해줍니다.
![Desktop View](/assets/img/20240901_post/Ruby_install_04.JPG){: width="800" height="400"}

6. 엔터를 눌러줍니다.
![Desktop View](/assets/img/20240901_post/Ruby_install_05.JPG){: width="800" height="400"}

7. 실행 체크 후 종료해줍니다.
![Desktop View](/assets/img/20240901_post/Ruby_install_06.JPG){: width="800" height="400"}

8. 설치가 완료됩니다.
![Desktop View](/assets/img/20240901_post/Ruby_install_07.JPG){: width="800" height="400"}


## **2. Node.js 설치**

 [**Node.js**](https://nodejs.org/en/)에서 다운로드 후 설치하여 주시기 바랍니다.
