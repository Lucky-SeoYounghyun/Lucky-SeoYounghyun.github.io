---
title: "[KT AIVLE] 시각지능 딥러닝 3일차 - 심화학습"
description: 
author:
date: 2024-10-23 22:08:41 +0900
categories: [KT aivle school, 시각지능 딥러닝]
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
금일은 시각지능 딥러닝 코딩 방법을 중접적으로 학습하였습니다.

<br>

## **1. 이전 학습 **
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
Convolution Neural Network(CNN, 합성곱 신경망) : 이미지 데이터를 훼손하지 않음
- 이미지 데이터 구조를 그대로 사용하여 접근과 더불어, 한번에 feature의 개성을 고려하기보다, 지역별 개성을 살려서 feature를 추출!
  - 필터가 움직이며 학습 -> feature map 생성!!
- pooling(sub-sampling)
  - feature map 사이즈를 줄인다(다운스케일링)
  - 연산량을 줄일 수 있음
  - Maxpool, Avgpool 이렇게 두가지가 있음
    - Maxpool : 최대값 추출
    - Avgpool : 평균값 추출
- 구성요소(Conv2D)
  - filters : 서로다른 feature를 추출하는 필터를 몇개? 사용? 할꺼?
  - kernel-size : 필터의 가로세로 크기(depth는 keras에서 자동으로 설정됨)
  - strides : 이동 보폭(default : 1,1) / 낮을수록 세부적인 패턴을 파악함
  - padding : feature map의 크기 보존, 외곽 정보 반영 (가로세로에 기본적으로 zero padding을 함)

Batch Normalization, Droput : 모델 성능을 높이기 위한 테크닉 기법

<br>

## **Preprocessing&Augmentation**
증강레이어  
이미지 데이터를 훈련할때 데이터를 랜덤하게 변환하여 데이터의 다양성을 높이고, 모델의 일반화 성능을 향상시킬 수 있습니다.
- RandomRotation
  - 이미지 회전
  - ex) RandomRotation(factor=(-0.3, 0.3))
    - factor=(-0.3, 0.3): 회전 정도를 설정하는 매개변수로, 이 범위에서 랜덤하게 회전이 발생합니다. -0.3은 시계 반대 방향으로 최대 30%의 회전을 의미하고, 0.3은 시계 방향으로 최대 30%의 회전을 의미합니다.
- RandomTranslation
  - 이미지 이동
  - ex) RandomTranslation(height_factor=(-0.3, 0.3), width_factor=(-0.3, 0.3))
    - height_factor=(-0.3, 0.3): 이미지 높이의 -30%에서 +30% 범위 내에서 랜덤한 세로 이동을 의미합니다.
    - width_factor=(-0.3, 0.3): 이미지 너비의 -30%에서 +30% 범위 내에서 랜덤한 가로 이동을 의미합니다.
- RandomZoom
  - 이미지 확대 / 축소
  - ex) RandomZoom(height_factor=(-0.2, 0.2), width_factor=(-0.2, 0.2))
    - height_factor=(-0.2, 0.2): 이미지 높이를 -20%에서 +20%로 랜덤하게 확대 또는 축소하는 매개변수입니다.
    - width_factor=(-0.2, 0.2): 이미지 너비를 -20%에서 +20%로 랜덤하게 확대 또는 축소하는 매개변수입니다.
- RandomFlip
  - 이미지 뒤집기
    - mode='horizontal_and_vertical': 이미지를 좌우로(가로 방향) 또는 상하로(세로 방향) 무작위로 뒤집습니다. 이는 좌우 반전, 상하 반전, 또는 둘 다 동시에 수행될 수 있음을 의미

위와같은 방법들이있으나 과도하게 이미지를 변경하면 원본 이미지가 훼손되어 이미지 학습에 오히여 악영향을 줄 수 있습니다.


## **4. 정리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
금일은 이전에 배운내용 간단히 정리와 증강레이어에대해서 학습하였습니다.

이만 가보겠습니다!

실습 코드는 아래 링크에서 확인 가능합니다.
- [**시각지능**](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/visual_intelligence)
