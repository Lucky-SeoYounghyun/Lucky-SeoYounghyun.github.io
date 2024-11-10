---
title: "[KT AIVLE] 6주차 정리(2차 미니프로젝트, 딥러닝)"
description: 
author:
date: 2024-10-13 13:00:00 +0900
categories: [KT aivle school, 10월]
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

머신러닝 미니 프로젝트와 딥러닝을 진행하였습니다.

>[2차 미니 프로젝트_01](https://lucky-seoyounghyun.github.io/posts/aivle_second_mini_project_1/)  
[2차 미니 프로젝트_02](https://lucky-seoyounghyun.github.io/posts/aivle_second_mini_project_2/)  

이번 주간 정리에는 최종 summary만 하도록 하겠습니다.

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
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">2차 미니프로젝트</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">2차 미니프로젝트</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">휴무</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">딥러닝</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">딥러닝</td>
    </tr>
  </table>
</div>

<br>

## **1. 2차 미니 프로젝트**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

2차 미니 프로젝트에서는 1차 미니프로젝트에서 간과했던 시간관리를 보다 체계적으로 관리하여 제한시간안에 PPT제작까지 끝마칠 수 있었습니다.
또한 이번 프로젝트를 통해 머신러닝에서 추가적으로 무엇을 배워야할지, 앞으로 어떤것을 공부해야할지를 알 수 있었습니다.
이외에 세부적인 정리내용은 각 `2차 미니프로젝트 각 일차별 정리` 에 기록하였습니다.

<br>

## **2. 딥러닝**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

최종 summary를 진행하겠습니다.

딥러닝 개념은 다음과 같다
- 가중치 초기값을 할당.
- 초기 모델로 예측
- 오차를 계산(loss function)
- 가중치 조절 : 오차를 줄이는 방향으로 가중치를 적절히 조절(optimizer)
  - 적절히 조절 -> 얼마 만큼 조절할 지 결정하는 하이퍼 파라미터 : lr(learing rate)
- 다시 처음으로 가서 반복
  - 전체 데이터를 적절히 나눠서(mini batch)반복 : batch_size
  - 전체 데이터를 몇 번 반복 학습할 지 결정 : epoch

- 딥러닝 전처리
  - NaN 조치, 가변수화, 스케일링
- Layer
  - 첫번째 Layer는 input_shape를 받는다.(분석단위의 shape)
    - 2차원 데이터셋의 분석단위 1차원 → shape는 ( feature수, )
  - Output layer의 node 수 : 1
  - Activation Function
    - Hidden layer에 필요 : 
      - 비선형 모델로 만들려고 ➔ hidden layer를 여럿 쌓아서 성능을 높이려고.
    - 회귀 모델링에서 Output Layer에는 활성화 함수 필요하지 않음!

- Output Layer의 Activation
  - Sigmoid : 0 ~ 1 사이 확률 값으로 변환해주는 역할
-Loss Function : binary_crossentropy

- 다중분류를 위해 y 값 전처리 필요
  - 방법1 : y값을 0,1,2,3,… 로 만들고, loss = ‘sparse_categorical_crossentropy’
  - 방법2 : y값을 one-hot encoding 하고, loss = ‘categorical_crossentropy’
- Output Layer의 Activation
  - softmax : 0 ~ 1 사이 확률 값으로 변환해주는 역할

- 총 정리

<table border="0" cellpadding="5" cellspacing="0" style="margin: 0 auto; border-collapse: collapse;">
  <tr>
    <th rowspan="2" style="text-align: center;">구분</th>
    <th colspan="1" style="text-align: center;">Hidden Layer</th>
    <th colspan="2" style="text-align: center;">Output Layer</th>
    <th colspan="2" style="text-align: center;">Compile</th>
  </tr>
  <tr>
    <th style="text-align: center;">Activation</th>
    <th style="text-align: center;">Activation</th>
    <th style="text-align: center;">Node수</th>
    <th style="text-align: center;">optimizer</th>
    <th style="text-align: center;">loss</th>
  </tr>
  <tr>
    <td style="text-align: center;">Regression</td>
    <td style="text-align: center;">relu</td>
    <td style="text-align: center;">X</td>
    <td style="text-align: center;">1</td>
    <td style="text-align: center;">adam</td>
    <td style="text-align: center;">mse</td>
  </tr>
  <tr>
    <td style="text-align: center;">2-Class</td>
    <td style="text-align: center;">relu</td>
    <td style="text-align: center;">sigmoid</td>
    <td style="text-align: center;">1</td>
    <td style="text-align: center;">adam</td>
    <td style="text-align: center;">binary_crossentropy</td>
  </tr>
  <tr>
    <td style="text-align: center;">Multi-Class</td>
    <td style="text-align: center;">relu</td>
    <td style="text-align: center;">softmax</td>
    <td style="text-align: center;">Class수</td>
    <td style="text-align: center;">adam</td>
    <td style="text-align: center;">sparse_categorical_crossentropy<br>categorical_crossentropy</td>
  </tr>
</table>

<br>

## 2 ) 실습 코드
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

2차 프로젝트와 딥러닝 코드는 git에 업로드 하였습니다.  
[2차 미니 프로젝트](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/mini_project_02)  
[딥러닝](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/DL)