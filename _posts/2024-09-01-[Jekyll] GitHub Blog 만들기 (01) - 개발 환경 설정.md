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

<br/>

## **0. 들어가기에 앞서**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
GitBlog 와 테마를 보다 효율적으로 사용하기위해 이번 글에서는 Ruby 설치와 jekyll설치를 하고자합니다.<br/>
모든 프로그램을 설치후 컴퓨터를 재부팅 해주어야 프로그램이 정상 작동합니다.

<br/>

## **1. Ruby 설치**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
[**Ruby**](https://rubyinstaller.org/downloads/archives/)에서 Ruby+Devkit 3.1.2-1 (x64)를 다운로드하여 아래글을 참고하여 설치하여 주시기바랍니다.
> 현재 Ruby+Devkit 3.1.2-1 (x64)가 아닌 다른 버전을 설치하면 아래와 같은 에러가 발생하는것을 발견하였습니다.<br/>
Could not find gem 'wdm (~> 0.1.1) mingw, x64_mingw, mswin' in locally installed gems.
{: .prompt-warning }
1. 다운로드<br/>
![Desktop View](/assets/img/20240901_post/Ruby_설치.PNG){: width="800" height="200" .w-75 }

2. accept하고 Next를 눌러줍니다.<br/>
![Desktop View](/assets/img/20240901_post/Ruby_install_01.JPG){: width="800" height="400" .w-75 }

3. 경로 지정 및 PATH 등록을 선택해줍니다, 연결프로그램 등록을 해줍니다.<br/>
![Desktop View](/assets/img/20240901_post/Ruby_install_02.JPG){: width="800" height="400" .w-75}

4. 추가 컴포넌트를 체크해줍니다.<br/>
![Desktop View](/assets/img/20240901_post/Ruby_install_03.JPG){: width="800" height="400" .w-75}

5. 실행 체크 후 종료해줍니다.<br/>
![Desktop View](/assets/img/20240901_post/Ruby_install_04.JPG){: width="800" height="400" .w-75}

6. 엔터를 눌러줍니다.<br/>
![Desktop View](/assets/img/20240901_post/Ruby_install_05.JPG){: width="800" height="400" .w-75}

7. 설치가 완료됩니다.<br/>
![Desktop View](/assets/img/20240901_post/Ruby_install_06.JPG){: width="800" height="400" .w-75}

<br/>

## **2. Node.js 설치**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

 [**Node.js**](https://nodejs.org/en/)에서 다운로드 후 아래 글을 참고하여 설치하여 주시기 바랍니다.
1. 다운로드<br/>
![Desktop View](/assets/img/20240901_post/nodejs_install_01.JPG){: width="800" height="200" .w-75 }

2. accept하고 Next를 눌러줍니다.<br/>
![Desktop View](/assets/img/20240901_post/nodejs_install_02.JPG){: width="800" height="400" .w-75 }

3. 자동 설치를 클릭하고 Next를 눌러줍니다..<br/>
![Desktop View](/assets/img/20240901_post/nodejs_install_03.JPG){: width="800" height="400" .w-75}

4. CMD창이 뜨면 아무키나 누른후 설치가 완료될때까지 기다려줍니다.<br/>
![Desktop View](/assets/img/20240901_post/nodejs_install_04.JPG){: width="800" height="400" .w-75}

<br/>

## **3. 글을 마무리하며**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
이번글은 본격적인 GitBlog를 활용해 Chirpy 테마적용한 블로그를 만들기 위한 사전 프로그램 설치 방법 글이였습니다.
다음 글에서는 GitBlog를 Chirpy테마로 만드는 방법을 설명해드리도록 하겠습니다.

이만 가보겠습니다!

<br/>

## **참조**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
<a href="https://stackoverflow.com/questions/78553132/shopify-error-coming-from-bundle-install/78617137#78617137" target="_blank">Could not find gem err</a>