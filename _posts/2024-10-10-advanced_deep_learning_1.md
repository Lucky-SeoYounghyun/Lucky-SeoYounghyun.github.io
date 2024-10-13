---
title: "[KT AIVLE] 딥러닝 1일차 - 심화학습"
description: 
author:
date: 2024-10-10 21:00:00 +0900
categories: [KT aivle school, 딥러닝]
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
원래 주간내용으로 정리하지만 해당내용은 주간 정리로만 담기에는 한계가 있어 심화학습 내용을 추가적으로 정리하고자 합니다.

## **1. 딥러닝 정리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
오늘은 딥러닝 1일차입니다! 많은것을 배우지는 않았지만 알아야할 내용이 많아 추가 정리합니다.

## **2. 회귀 모델링**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### 모델, 모델링
- Model
  - 모델 : 데이터로부터 패턴을 찾아, 수학식으로 정리해 놓은 것
  - 모델링 : 가능한한 오차가 적은 모델을 만드는 과정
- 모델의 목적
  - 샘플을 가지고 전체를 추정
- 모델의 성능은 오차를 통해 계산
  - 모델링 : train err를 최소화 하는 모델을 생성
  - 모델 튜닝 : validation err를 최소화 하는 모델 선정
- 평가 지표
![Desktop View](/assets/img/20241011_post/performance_metrics.JPG){: width="800" height="400"}

- 간단한 딥러닝 모델 표현 방법
  - 선형 회귀 모델
![Desktop View](/assets/img/20241011_post/model.JPG){: width="800" height="400"}


- 딥러닝과 머신러닝의 코드 순서 차이
![Desktop View](/assets/img/20241011_post/code_step.JPG){: width="800" height="400"}

### 딥러닝 개념 이해
- 가중치
  - 딥러닝은 최적의 Weight를 찾기위해 오차를 가장 적은 모델을 학습한다.
- 가중치 조정을 위해 다음과 같이 반복한다.
  - 조금씩 weight를 조정하며 오차가 줄어드는지확인
  - 지정된 횟수만큼 혹은 더이상 오차가 줄지 않을때까지
  - 즉! 오차를 최소화 하는 파라미터(가중치)를 찾는다!
- 학습 절차
![Desktop View](/assets/img/20241011_post/model_step.JPG){: width="800" height="400"}
- 즉 코드로 `model.fit`를 하는 순간 아래와 같이 동작한다.
![Desktop View](/assets/img/20241011_post/model_fit.JPG){: width="800" height="400"}

### 딥러닝 모델링
- 스케일링
  - 필수! 그냥 필수! 모든 값의 범위를 0~1로 변환함
  - 방법 1 : Normalization(정규화)
    - 모든 값의 범위를 0 ~ 1로 변환
    $x' = \frac{x - x_{min}}{x_{max} - x_{min}}$
  - 방법 1 : Standardization(표준화)
    - 모든 값을, 평균 = 0, 표준편차 = 1 로 변환
    $z = \frac{x - \mu}{\sigma}$

```python
# 스케일러 선언
scaler = MinMaxScaler()
# train 셋으로 fitting & 적용
x_train = scaler.fit_transform(x_train)
# validation 셋은 적용만!
x_val = scaler.transform(x_val)
```

- 딥러닝 구조
![Desktop View](/assets/img/20241011_post/dl_structured.JPG){: width="800" height="400"}

```python
# 메모리 정리
clear_session()
# Sequential 타입
model = Sequential([Input(shape = (nfeatures,)),
 Dense(1) ])
# 모델요약
model.summary()
```

- 컴파일
  - 선언된 모델에 대해 몇가지 설정을 한 후 컴퓨터가 이해할 수 있는 형태로 변환하는 작업
  - loss function
    - 오차 계산을 뭘로 할지 결정
    - 회귀모델 : mse, 분류모델 : cross entropy
  - optimizer
    - 오차를 최소화 하도록 가중치를 업데이트하는 역할
    - Adam
      - 최근 딥러닝에서 가장 성능이 좋은 Optimizer로 평가 됨.
    - learning_rate
      - 업데이트 할 비율
      - 기울기(gradient)에 곱해지는 조정 비율
      (걸음걸이의 ‘보폭’을 조정한다고 표현)

```python
model.compile(optimizer = Adam(learning_rate = 0.1) , loss='mse')
```

- 학습
  - epoch : 반복횟수
  - validation_split : tarin 데이터에서 20%를 검증셋으로 분리
  - batch_size : 배치 단위로 학습, 전체 데이터를 적절히 나눠서
  - .history : 학습을 수행하느 과정중에 계산된 오차 기록

```python
history = model.fit(x_train, y_train, epochs = 20, validation_split=0.2).history
```

- 학습 곡선
  - 바람직한 곡선 : 초기 epoch에서는 오차가 크게 줄고 오차 하락이 꺽이면서 점차 완만해지는 그래프

- hidden layer
  - 학습 결과를 좋게 하기위해
  - 보통 활성 함수로 relu 사용
  - 예측 결과는 1개
![Desktop View](/assets/img/20241011_post/hidden_layer.JPG){: width="800" height="400"}

```python
model3 = Sequential([Input(shape = (nfeatures,)), Dense(2, activation = 'relu'), Dense(1) ])
```
- 활성함수?
  - 현재 레이어의 결과값을 다음 레이어로 어떻게 전달할지 결정/변환해주는 함수
  - 없으면?
![Desktop View](/assets/img/20241011_post/activation_function.JPG){: width="800" height="400"}
    - 다음과 같이 히든 레이어를 여러개 추가해도 그냥 선형회귀 가 되어버림...
  - 활성함수는 hidden layer에서는 선형함수를 비선형 함수로 변환, Output layer에서는 결과값을 다른 값으로 변환해주는 역할을 함
![Desktop View](/assets/img/20241011_post/Relu.JPG){: width="800" height="400"}

<div style="text-align: center;">
  <table border="0" cellpadding="5" cellspacing="0" style="margin: 0 auto;">
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
  </table>
</div>

<br>

## **3. 실습 코드**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
딥러닝 또한 실습 위주로 진행하였으며 코드는 git에 업로드 하였습니다.  
[실습코드](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/DL)