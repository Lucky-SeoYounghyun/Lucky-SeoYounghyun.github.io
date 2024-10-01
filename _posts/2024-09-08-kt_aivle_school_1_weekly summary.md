---
title: "[KT AIVLE] 1주차 정리(opening day, git, python 기초)"
description: 
author:
date: 2024-09-08 23:00:00 +0900
categories: [KT aivle school, 9월]
tags: [KT aivle school]
pin: false
math: true
mermaid: true
image:
  # path: /assets/img/20240912_post/KT_모집요강.jpg
  # lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  # alt: ktaivel_image
---




## **0. 개요**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
이번 포스팅은 개인적으로 주간 학습내용을 정리하기위해 작성하는 글입니다.
주간 일정은 다음과 같습니다.

<div align="center">
  <table border="1" cellspacing="0" cellpadding="10" style="border-collapse: separate; border-radius: 12px; overflow: hidden; text-align: center; width: 60%; border: 1px solid #ddd;">
    <tr>
      <th style="border: 1px solid #ddd; padding: 10px;">월</th>
      <th style="border: 1px solid #ddd; padding: 10px;">화</th>
      <th style="border: 1px solid #ddd; padding: 10px;">수</th>
      <th style="border: 1px solid #ddd; padding: 10px;">목</th>
      <th style="border: 1px solid #ddd; padding: 10px;">금</th>
    </tr>
    <tr>
      <td colspan="2" style="border: 1px solid #ddd; padding: 10px;">오프닝데이</td>
      <td style="border: 1px solid #ddd; padding: 10px;">git</td>
      <td colspan="2" style="border: 1px solid #ddd; padding: 10px;">python</td>
    </tr>
  </table>
</div>

오프인 데이를 제외한 git 부터 정리하도록 하겠습니다.

## **1. git**
git에대한 전반적인 내용을 다루었으며 주로 visual studio GUI를 통한 git 협업에대해 알려주셨으며, git이 branch에 등록되고 main에 합류하는 과정과 방법에대해 알려주셨다.

### 1.1) 정리
- git은 데이터를 보관 및 관리를 해주는 분산형 버전 관리 시스템이다.
- 모든 회사에서는 각종 Issue, 관리감독의 유용성등으로 인해 버전관리를 중요시여기며 이는 앞으로 더 중요해질것이다.
- 개발자로서 앞으로 많은 사람들과 협업해 나갈것이다. 이때 가장 중요한것이 Git을 통한 협업일것이다.

### 1.2) 추가학습
- git consol을 활용한 git 기능 익히기
- git을 통한 버전 관리, 백업, 협업 등 계속하여 익숙해지기

### 1.3) 기능 정리

1) 깃의 대표적인 기능
```
git add -A
git commit -m "message"
git push
```
다음과 같은 흐름으로 git에 업데이트 된다.  
git add : `working directory` ->  git commit : `Stage Area` -> git push `Repository`

> git을 통해 오픈소스 협업을 할때는 commit시 branch 규칙을 유의해야한다. 대중적인 규칙은 다음과 같다.
fix, feat, 등등
{: .prompt-tip }

<br/>

2) 코드 테스트
아직 확실치 않은 실험적인 작업을 할때는 반드시 checkout을 통해 branch를 새로 생성하고 확인후 main에 merge하도록 한다.

<br/>

3) 동기화
작업전에는 동기화 작업이 필요하며 이를위한 코드는 다음과 같다.
- fetch : 새로운 브런치를 만들며 동기화 한다.
- pull : 기존 파일과 동기화한다.

> `충돌 방지`: 로컬변경사항이 많고, 원격 저장소의 변경 사항이 있는 경우바로 merge시 충돌 방생 가능, 이때는 git fetch로 변경 사항 확인 후, git merge를 수동으로 수행하는 것이 좋다.  
`수동 병합`: git fetch 후 git merge를 사용하면, pull 명령을 사용하는 것보다 병합 과정을 세밀하게 조정할 수 있다
{: .prompt-tip }

4) 버전 관리 방법
Git 에는 Head, Main(예전에는 Master라고 불렸으며 다른이름으로 대체 가능) 가 존재한다.
Head : 현재 checkout된 branch or commit를 가리키는 pointer  
Main : 그냥 이름이라고 생각하면 편함  

## **2. Python**
아주 기초적인 파이썬 문법부터 numpay, pandas 와같은 데이터 구조를 다루는 패키지에대해 설명해주셨다.  
기초적인 문법으로 어려운것은 없었으며 차주 패키지에대해서는 추가적으로 설명을 진행하기로 하였다.  
따로 정리해야할 내용은 없으며 실습내용은 다음과 같다.  
[python 기초](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/python%20%EA%B8%B0%EC%B4%88)