---
title: "[KT AIVLE] 미니 프로젝트(01) 데이터분석"
description: 
author:
date: 2024-09-25 23:00:00 +0900
categories: [KT aivle school, 미니 프로젝트]
tags: [KT aivle school, mini_project]
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
안녕하세요!

이번에는 aivle school에서 첫 미니프로젝트를 진행하였습니다.

프로젝트를 진행하면서 느낀점과 데이터 분석의 흐름에대해서 설명해드리도록 하겠습니다.

## **1. 미니프로젝트**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### 1.1) 주제
- 서울시 생활정보 데이터로 대중교통 수요분석

### 1.2) 목표
- 데이터를 분석하여 다양한 인사이트를 얻고 도메인지식을 활용하는 방법을 안다.
- 최종적으로 어떤 지역구에 노선수를 증설해야하는지 알아본다

## **2. 데이터 분석**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### 2.1) 데이터 확인
- [**미니프로젝트 jupyter 학습 코드**](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/mini_project_01)

### 2.2) 미션 1.1 ~ 1.4
- 각 데이터를 가공하여 자치구별 연관된 데이터들로 정제할 수 있었으며 이 비교를 통해 가설을 세울 수 있었습니다.
- 각 히트맵들을 분석하여 분석전에 예측한 값이랑 차이를 보이는것을 알 수 있었습니다.  
- 다양한 데이터를 조작하기전에는 사전 도메인 지식의 중요성을 확인하였습니다.  
- 이 데이터 값만이아닌 좀더 가중치를 적용하였을때 의미있는 데이터를 가질 수 있는것을 확인하였습니다.

### 2.2) 미션 1.5
- 이번 미션은 앞선 데이터 정제를 통해 얻은 파일들을 머지하여 통합 데이터를 분석하는 미션입니다.
- 통합데이터를 분석하여 정류장수/노선수(노선수에따른 정류장수 비율)은 전체 인구수와 비교할시 유의미한 값을 나타내는것을 볼 수 있었습니다.
- 이후 해당 수치에서 이상치를 찾아낸 후 이상치를 나타내는 이유를 분석하여 최종 결론을 도달하였습니다.

## **3. 결론**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

팀 발표도 마무리한 '시간이 조금 더 있었더라면', '데이터를 조금 더 살표보았더라면' 등의 아쉬움이 있었습니다.  
하지만 저희는 저희팀 나름의 최선의 결과를 도출해냈다고 생각합니다.    

이상으로 이번 데이터 분석을 통해 얻은 지식들을 정리하고 마무리하도록 하겠습니다.
- 데이터를 통해 유의미한 인사이트를 얻기위해서는 `사전 도메인지식`을 충분히 가지고있는것이좋다
- 데이터를 추출한 후에 `후 가공에따라 결과에대한 신뢰도`가 결정된다.
  - 저희 결론 도출 과정에서도 기존 데이터를 정류장수/노선수로 나누는등 데이터 후 가공을통해 결론을 얻었습니다.
  - 다른팀 발표에서는 가중치를 곱하는 방법을 통해서 결론을 얻었습니다.
  (<small>실제로 해당팀의 아이디어가 아주 좋았다고 생각합니다.</small>)
- 다시한번 느꼈지만 `p-value와 상관관계등을 유의미한 값으로 받아들이는 절대적인 수치는 없다`입니다.

## **4. 느낀점**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
이번 프로젝트는 정말 재미있었고 얻어가는게 많았던 프로젝트였습니다.  
혼자서만 진행했을때에는 느끼짐 못했던 나 자신의 부족함을 알게되었고, 다른 사람의 아이디어를 직접 느끼면서 지금까지의 내가 너무 틀에 밖혀있었구나를 느꼈던것 같습니다.  

이런 아쉬움과 피드백, 다양한 아이디어를 나의 지식과 경험으로 쌓아올려 내일은 더욱 더 성장한 모습을 보여드리도록 하겠습니다!

이만 가보겠습니다!
