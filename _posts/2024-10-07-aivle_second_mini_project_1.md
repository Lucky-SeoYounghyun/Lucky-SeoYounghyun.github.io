---
title: "[KT AIVLE] 미니 프로젝트 2차 (01) 데이터 전처리 및 분석"
description: 
author:
date: 2024-10-07 23:00:00 +0900
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

미니프로젝트 2차 1일차에는 학습용 데이터가 주어졌으며 데이터 전처리 ~ 탐색적 데이터 분석을 진행하였습니다.

## **2. 데이터 전처리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
데이터 전처리에는 결측치처리, 불필요 변수 제거, 데이터 분리등을 진행하였습니다.  
그중 저희 팀에서 중점적으로 확인한 사항은 다음과 같습니다.  

1. 결측치 처리
- 결측치는 건물형태, 난방방식, 승강기 설치여부 총 3개 칼럼에서 총 195개의 결측치를 확인하였습니다.
- 처리방식
  - 최빈값 : 초기에 셋팅하려고 했던 방법입니다. 하지만 최빈값으로 셋팅시 데이터 값이 한쪽으로 쏠리며 학습 결과에 악영향을 줄것으로 판단하였습니다.
  - XGboost : 결측치 또한 지금까지 배운 방법을 통하여 예측 할 수 있을것이라고 가정하였으며 각 결측치 칼럼을 target으로 두고 학습시켜 채워주었습니다.
- 결과
  - 실제로 최빈값에서 XGboost로 결측치를 처리하여 데이터 학습 결과의 향상을 기대할 수 있었습니다.

2. 데이터 분리
- 전용 면적 구간별 집계에서 각 구간으로 나눈 후 pivot형태로 칼럼을 생성하였습니다.
- 처리방식
  - 임의의 구간 설정 : 초기 셋팅 값이였으며, 이를 통한 구간 설정시 데이터에 학습자의 주관과 의미없는 값이 들어갈 수 있는것을 확인하였습니다.
  - kmeans를 통한 구간 설정 : kmeans를 통하여 각 값을 관련도가 높은것끼리 묶은후 구간을 나누어주었습니다. 이를통해 주관을 최대한 배재하여 데이터 학습 결과의 향상을 기대할 수 있었습니다.

## **3. 탐색적 데이터 분석**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
탐색적 데이터 분석에서는 주로 데이터 전처리에서 가공한 데이터의 이변량 분석, 단변량 분석을 하는등의 과정을 거쳐 연관성을 확인하고 시각화 하를 하였습니다..
또한 이를 통해 추가적으로 가공할 데이터를 확인하고 난방방식, 승강기 설치여부, 단지코드를 단순화하고 지역제거를 하는등의 추가 전처리 과정을 거쳤습니다.

그중 저희 팀에서 중점적으로 확인한 사항은 다음과 같습니다.
각 값에서 이상치를 확인하고 이를 바플롯을 그려 실제로 다른 칼럼과의 관련이 없는 이상치인것이 확인되면 제거를 하였습니다.
이를통해 보다 원하는 상관계수와 p-value값이 목표치에 부합하게 나오는것을 확인할 수 있었습니다.

## **4. 느낀점**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
오늘은 데이터 전처리와 분석을 진행하였습니다.

이를 통해서 다양한 경우의 수를 확인 할 수 있었고 내일있을 수요량 예측을 통해서 오늘 진행한 전처리와 분석이 어떠한 결과를 만들지 기대되는 하루였습니다!

이만 가보겠습니다!
