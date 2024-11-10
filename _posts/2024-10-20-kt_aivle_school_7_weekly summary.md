---
title: "[KT AIVLE] 7주차 정리(3차 미니프로젝트, 딥러닝)"
description: 
author:
date: 2024-10-20 13:00:00 +0900
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

이번주에는 딥러닝 심화학습과 세번째 미니 프로젝트를 진행하였습니다.


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
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">딥러닝 심화학습</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">딥러닝 심화학습</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">3차 미니프로젝트</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">3차 미니프로젝트</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">3차 미니프로젝트</td>
    </tr>
  </table>
</div>


<br>

## **1. 딥러닝 심화학습**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
저번주에 이어서 딥러닝 강의를 이어서 진행하였습니다.

### 기초 학습
- 기본 알고리즘 정리

  - 선형회귀, 로지스틱 회귀, KNN, Decision Tree, Random Forest, Gradient Boost와 같은 모델의 핵심 원리 및 활용 조건 학습.
  - 각 알고리즘의 전제 조건(NaN 처리, 가변수화, 스케일링) 및 주요 하이퍼파라미터 정리.

- 과적합 방지 기법
  - Early Stopping: patience, monitor, min_delta 옵션을 활용해 과적합 방지.
  - Dropout: 신경망의 일부 뉴런을 학습 시 비활성화하여 복잡한 의존성 제거.
  - Regularization(L1, L2): 과적합을 방지하기 위한 가중치 규제.

### Functional API 학습
- 복잡한 모델 구성
  - Functional API로 다중 입력/출력 모델 구현.
  - 데이터 특성별 분리 학습 및 병합을 활용해 다양한 입력 데이터를 통합 학습.

### 시계열 모델링
- 모델링 기법 비교
  - 통계적, 머신러닝 기반, 딥러닝 기반 시계열 데이터 분석.
  - 시계열 데이터에서 시간 흐름 구간(timesteps)을 고려한 RNN, LSTM 모델 설계.

- 전처리
  - 스케일링, 데이터 3차원 변환, train/validation 분할.

- RNN/LSTM 설계
  - return_sequences 활용으로 출력 데이터의 크기 조절.
  - 장기 의존성 문제를 해결하기 위한 LSTM 구조 학습.

<br>

## **2. 3차 미니프로젝트**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### 프로젝트 개요
- 목표
  - 스마트폰 센서 데이터로 동작(Activity)을 분류하는 딥러닝 모델 개발.
  - 데이터는 561개 피처로 구성, 동적(1)과 정적(0)으로 이진 분류 후 세부 분류 진행.

### 주요 내용
- 특성 중요도 추출
  - Random Forest로 피처 중요도 분석.
  - 상위 150개 피처만 활용하여 학습 속도와 성능 향상 확인.

- 모델링 접근
  - 단순 레이어 쌓기
    - 2의 배수로 레이어 구성, 중간에 Dropout과 Regularization을 추가해 과적합 방지.
    - 높은 정확도(98% 이상)를 기록.

- Function API
  - 센서별 주요 데이터를 구분하여 다중 입력 모델 구성.
  - 기능별 분리 학습 후 통합 학습으로 높은 성능 달성(약 99%).

- 파이프라인 구축
  - 전체 모델을 통합하는 파이프라인 설계.
  - 단계별로 정확도를 확인하며 약 99%의 최종 정확도를 기록.

- 성과
  - 높은 정확도와 창의적인 접근 방식으로 강사님 극찬.
  - PCA 및 K-Fold 기법 활용 사례를 통해 다양한 학습 방법 이해.

<br>

## 2 ) 실습 코드
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

3차 프로젝트와 딥러닝 코드는 git에 업로드 하였습니다.  
[3차 미니 프로젝트](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/mini_project_03)  
[딥러닝](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/DL)