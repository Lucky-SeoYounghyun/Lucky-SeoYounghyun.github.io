---
title: "[KT AIVLE] 시각지능 딥러닝 1일차 - 심화학습"
description: 
author:
date: 2024-10-21 08:04:41 +0900
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
금일은 시각지능 딥러닝의 기초를 학습하였습니다.

이는 향후 학습할 시각지능 딥러닝을 위한 중요한 토대가 됩니다.

## **1. CNN(Convolutional Neural Network)**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
![Desktop View](/assets/img/20241021_post/cnn.JPG){: width="800" height="400"}

- feature map
  - 계산식 : $n_{\text{out}} = \left\lfloor \frac{n_{\text{in}} + 2p - k}{s} + 1 \right\rfloor$
    - n in : input feature map의 가로세로 사이즈
    - k : Convolution filter의 가로세로 사이즈
    - s : Convolution filter의 이동 보폭
    - p : input feature map에 덧붙일 pad의 수
    - n out : output feature map의 가로세로 사이즈
  - padding하면 자동적으로 외곽에 0으로 생성됨
    - 외곽에 0으로 생성(외곽 데이터를 좀더 의미있게 하기 위하여)
    ![Desktop View](/assets/img/20241021_post/zeropadding.JPG){: width="800" height="400"}
  - 기본적으로 Stride은 1로 설정됨
    - 한칸씩 움직인다는 뜻
    ![Desktop View](/assets/img/20241021_post/feature.JPG){: width="800" height="400"}
  - 커널
    - 이전 레이어를 그대로 가져옴
  - pooling filter
    - 움직이며 학습
  - Pooling Layer
    - 계산량 부담을 줄이기 위해 등장!
    - Max Pooling : 최대값 반환
    - Average Pooling : 대표값 반환  

다음 사진을 보고 생각해보자
![Desktop View](/assets/img/20241021_post/layer_1.JPG){: width="800" height="400"}
- s : 보폭
- filter는 다음 레이어를 보고 확인
- depth : 이전 레이어 확인
- n x n , f: 필터 크기

<br>

## **4. 정리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
금일은 전반적인 시각지능의 기본적인 원리 및 간단한 코드 구현을 진행하였습니다.

이만 가보겠습니다!

실습 코드는 아래 링크에서 확인 가능합니다.
- [**시각지능**](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/visual_intelligence)
