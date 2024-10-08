---
title: "[KT AIVLE] 미니 프로젝트 2차 (02) 수요량 예측 모델 선정"
description: 
author:
date: 2024-10-08 22:04:41 +0900
categories: [KT aivle school, 미니 프로젝트]
tags: [KT aivle school, second_mini_project]
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

이번에는 aivle school에서 두번째 미니프로젝트를 진행하였습니다.

프로젝트를 진행하면서 느낀점과 머신러닝 학습 방법들을 설명드리도록 하겠습니다!

또한 실습 코드는 아래 링크에서 확인하실 수 있습니다
- [**미니프로젝트 jupyter 학습 코드**](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/mini_project_02)

## **1. 주제**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
- 주택 주차공간 실주차량 예측

미니프로젝트 2차 2일차에는 x_test데이터가 주어졌으며 이를 통해 target값을 예측하는 최적의 모델을 찾는것이 과제로 주어졌습니다. 

## **2. 모델 탐색**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
금일 미니 프로젝트에서는 1일차에 진행하였던 전처리 데이터를 이용하여 최적의 학습모델을 찾은후 발표를 하는 시간을 가졌습니다.  

지금까지 배운 다양한 알고리즘중에는 RandomSearchRegression모델이 가장 학습결과가 좋은 것을 확인할 수 있었으나, 좀더 좋은 모델을 효율적으로 찾을 수 있지않을까?  

라는 의문에서 시작하여 AutoML이라는 프로그램을 찾을 수 있었습니다.  

학습을 시도한 AutoML은 h2o와 mljar모델이였습니다. 이중 금일 학습을 시도한 모델에 가장 적합한 모델은 mljar 모델이였으며 이모델을 간략히 설명하면 아래와 같습니다.  
1. 가장 최적의 하이퍼 파라미터와 학습 모델을 자동으로 찾아 학습시킨 후 결과를 출력합니다.
2. 해당 모델을 가지고 후에 학습을 진행할 수 있습니다.
이렇게 대략적인 큰 틀을 가지고있는 프로그램으로 학습을 진행하였을때 최적의 모델은 CatBoost가 나왔으며 최종적으로 스코러 87%로 준수한 값이 도출되었습니다.
사용한 모델은 아래와 같습니다.
- [**mljar**](https://github.com/mljar/mljar-supervised)
- [**H20**](https://github.com/h2oai/h2o-3)

## **4. 느낀점**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
최종적으로 전체 발표도 진행하였으며 다른조가 학습시킨 결과를 보면서 많은것을 얻어갈 수 있었던 프로젝트였습니다.

평소 혼자서 공부했을때에 비해서 다른 분들의 학습 방법또한 보면서 배울점이 많았던것 같습니다!

이만 가보겠습니다!
