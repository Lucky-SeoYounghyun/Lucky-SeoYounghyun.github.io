---
title: "[KT AIVLE] 미니 프로젝트 3차 (03) 스마트폰 센서 데이터 기반 모션 분류"
description: 
author:
date: 2024-10-18 23:04:41 +0900
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

오늘은 3차 미니 프로젝트 마지막날로 pipline를 만든 후 내용을 정리하여 전체 발표하는 시간을 가졌습니다!  

확실히 3번째 프로젝트여서 그런지 어느정도 만족스러운 결과를 얻을 수 있었던 미니 프로젝트 였습니다!  

그러면 금일 진행한 프로젝트의 전반적인 설명과 최종 정리내용을 정리하겠습니다!  

- [**미니프로젝트 jupyter 학습 코드**](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/mini_project_03)

## **1. 주제**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- 모델 정확도를 높이기 위한 pipline 구성!

금일은 지금까지 구성한 모델을 바탕으로 아래와 같은 pipline모델을 구성하엿습니다.  
![Desktop View](/assets/img/20241018_post/pipline.JPG){: width="800" height="400"}

<br>

## **2. 모델 구성**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

1. 파이프라인 구축
- 훈련된 모델을 통해 위 그림과 같은 파이프 라인을 구축하는 과정을 수행하였습니다.
- 저희조는 Model_1에서는 1.0의 정확도를 Model_2에서는 1.0 마지막으로 Model_3에서는 0.98로 정적 데이터를 분리할때 비교적 낮은 정확도를 보였습니다
  - 정적 데이터를 분리할때 낮은 정확도를 보인 이유로는 세부 데이터로 보았을때서로 완전히 갈라지는 특성이 적은것에서 비롯된다는것을 1일차에서 확인하였습니다.
  - 이에 Function API를 통하여 수치 향상을 기대할 수 있을것으로 보입니다.
- 전체적인 PIPLINE구성결과 약 99%의 정확도를 보이는것을 확인할 수 있었습니다.  

2. 특성 제거
- 현재 560개정도의 특성 데이터를 가지고 있으나 학습할때 이 모든 특성데이터(열)들이 필요하지 않을것이라 생각하였습니다.  
- 결론적으로 150개정도의 중요도가 높은 특성만을 사용하여도 대략 96%의 정확도를 보이는것을 확인할 수 있었습니다.  

<br>

## **2. 발표**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

마지막으로 저희 조 포함 총 5조가 발표를 진행하였으며 다른 조가 진행한 프로젝트를 확인하며 다양한 견해를 확인할 수 있었습니다.  
저희조는 아이디어와 정확도 면에서 강사님의 극찬? 을 받았습니다.  
또한 다른조에서 활용한 주요 아이디어는 아래와 같았습니다.  
1. PCA 기법(주성분 분석)
  - 현재 560개정도의 특성데이터를 주요 특성데이터와 압축 피처를 통해 정확도를 높이는 아이디어

2. KFOLDS 기법
  - 학습한 데이터를 기반으로 다른 데이터를 재학습

이외에도 다양한 아이디어들이 나왔으나 가장 흥미로웠던 학습방법의 활용은 위 두개였던것 같습니다.  

## **4. 느낀점**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
이번 미니 프로젝트를 통하여 데이터를 학습하는 방법에는 다양한 방법과 다양한 아이디어가 존재한다는것을 최종 발표시간에 다시한번 확인할 수 있었습니다.  

이러한 아이디어를 통해 추후 진행할 빅 프로젝트에 적극 반영하여 우수한 결과를 낼 수 있도록 노력하도록 하겠습니다!  

이만 가보겠습니다!
