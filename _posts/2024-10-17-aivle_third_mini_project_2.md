---
title: "[KT AIVLE] 미니 프로젝트 3차 (02) 스마트폰 센서 데이터 기반 모션 분류"
description: 
author:
date: 2024-10-17 22:04:41 +0900
categories: [KT aivle school, 미니 프로젝트]
tags: [KT aivle school, third_mini_project]
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

오늘은 3차 프로젝트 2일차를 진행하였습니다!

다양한 학습 모델을 구현하였으며 이에대한 결과와 overfitting에대한 대응방법을 확실하게 알 수 있었습니다.

또한 실습 코드는 아래 링크에서 확인하실 수 있습니다.  
- [**미니프로젝트 jupyter 학습 코드**](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/mini_project_03)

<br>

## **1. 주제**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- 모델링을 통한 최적의 학습 모델 구현

금일은 본 데이터에맞는 최적의 학습모델을 찾는 프로젝트를 진행하였습니다.
이 아이디어로 학습시간에 학습했던 레이어 층을 쌓는 기법과 어제 학습했던 RandomForest에 의한 가중치에대한 학습 리스트를 통하여 구하는것이 있었습니다.

<br>

## **2. 학습모델 구성**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

1. 레이어 쌓기
기본적인 학습모델은 2의 배수를 따라갔으며 점차적으로 레이어를 단순화하는 방식을 채택하였습니다.  

다만 그렇게 레이어를 구성시 과적합 문제가 발생함에따라 lr값은 0.0001로 설정하고 중간중간 l1과 l2 정규화를 통하여 오버피팅을 방지하였습니다.  

이렇게 레이어를 구성했을때 총 40만개의 학습 데이터가 생성되었으며 정확도는 0.988정도로 상당히 우수한 능력을 보이는것을 확인하였습니다.  

2. 일부 특징 제거
이렇게 단순히 레이어만 쌓았을때는 위와같은 우수한 능력을 보이는것을 확인하였으므로 2차적으로는 561개의 특징을 전날에 학습하였던 우선순위를 기준으로 학습하였을때의 정확도를 비교하였습니다.
이에 전달 학습 데이터를 추출하여 상위 150개의 특징만을 추출하여 학습해보았을때
val값에 대해서는 96%정도의 정확도를 보여주었으며 test값에 대해서는 95%정도의 정확도를 보여주어 이러한 학습또한 좋은 방법이 될 수 있는것을 확인하였습니다.

3. function API
Function API를 통하여 각 특징을 주요 요소(ACC, GyRO, etc)로 구분하여 학습을 진행해보았습니다.
이를 통하여 학습결과 98%정도의 정확도를 보여주었으며 이 방법은 pipline를 구성한 후 각 요소를 추출할때 더 우수한 성능을 보일것으로 추측하였습니다.

<br>

## **3. 느낀점**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
오늘은 다양한 학습방법을 통해 정확도를 비교하였으며 그중 최적의 모델을 내일 있을 최종 파이프라인에 사용하는것을 목표로 진행하였습니다.

그 결과 가장 단순하고 학습 능력이 뛰어난 단순 레이어 쌓기 방법이 채택되었으며, 각 특징을 분류하는 2차 line에서는 function API를 활용하는 방법또한 고려해볼것을 최종 결정하였습니다.

오늘은 다양한 학습방법의 활용을 통하여 정확도 변화 및 overfitting의 상관관계를 확실히 알 수 있었으며 다양한 케이스를 직접 실행해볼 수 있었던 프로젝트 였습니다.

이만 가보겠습니다!
