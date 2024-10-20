---
title: "[KT AIVLE] 미니 프로젝트 3차 (01) 스마트폰 센서 데이터 기반 모션 분류"
description: 
author:
date: 2024-10-16 22:04:41 +0900
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

이번에는 aivle school에서 세번째 미니프로젝트를 진행하였습니다.  

프로젝트를 진행하면서 느낀점과 딥러닝 학습 방법들을 설명드리도록 하겠습니다!  

또한 실습 코드는 아래 링크에서 확인하실 수 있습니다.  
- [**미니프로젝트 jupyter 학습 코드**](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/mini_project_03)

<br>

## **1. 주제**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- 스마트폰 센서 데이터 기반 모션 분류

이번 미니프로젝트에서는 열이 500개가 넘는 데이터를 필요한 우선순우에따라 경량화하고 딥러닝으로 학습을 진행하는 방법을 다룹니다.  

<br>

## **2. 중요도 확인**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

금일 미니프로젝트의 데이터는 5 row x 563 columns를 가진 데이터로 상당히 많은양의 columns를 가지고 있는데이터입니다.  

따라서 그중 중요도가 높은 columns를 확인하고 이를 학습에 사용하기 위한 전처리를 하는 것을 금일 진행하였습니다.  

우선 각 열에대한 설명을 받았으며 각 시간에따른 Acc와 Gyro변화량을 나타낸 데이터이며 각 구간을 특정 구간을 window설정하여 기록한 데이터 라는 사실을 알았습니다.  

이에 각 columns에서 중요도를 어떻게 추출하는 방법에 대해서는 트리기반 모델(randomfores, XGboost, etc)로 변수 중요도를 추출한 후 상위 N개의 데이터를 추출하는 방법이 있다는 사실또한 알 수 있었습니다.  

이에 데이터를 RF로 변수중요도를 추출하여 상위 5개 하위 5개를 추출한 후 각 columns의 데이터가 해당 Activity를 어떻게 분류하는지 시각화하여 비교하였으며 큰 영향을 끼치는 데이터가 어떤것이 있는지 확인할 수 있었습니다.  

또한 Activity를 정적인 동작과 동적인 동작(0과 1)로 분류하여 해당 값에서는 어떤 요소가 중요도가 높은지 확인하였습니다.  

<br>

## **3. 느낀점**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

마지막날의 데이터는 pipline를 통하여 0과 1로 나는 데이터를 각 단계에서 세부 분류를 한후 통합하는 절차로 동작할것입니다.  

이를 유의하여 각 단계별 요소의 중요도를 추출하였으며 내일부터는 기본 모델링을 통하여 실제로 해당 요소가 적용된 모델을 시험해보게 될것입니다.  

이번 미니프로젝트를 통하여 딥러닝 강의에서 이론과 실습만으로 배웠던것을 실제 활용데이터에서는 많은 columns에서 어떻게 대응하고 모델을 설계하는지에대해 알 수 있었던것같습니다.  

오늘 추출한 요소들이 내일 모델에서 어떤 결과를 보일지 기대되는 하루를 마무리하며   

이만 가보겠습니다!
