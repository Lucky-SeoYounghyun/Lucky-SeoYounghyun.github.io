---
title: "[KT AIVLE] 11주차 정리(5차 미니프로젝트, 6차 미니프로젝트)"
description: 
author:
date: 2024-11-17 13:00:00 +0900
categories: [KT aivle school, 11월]
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

이번주에는 시각지능 딥러닝 학습을 진행하였습니다.


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
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">5차 미니프로젝트</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">5차 미니프로젝트</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">6차 미니프로젝트(1차)</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">6차 미니프로젝트(1차)</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">6차 미니프로젝트(1차)</td>
    </tr>
  </table>
</div>


<br>

## **1. 5차 미니프로젝트**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

5차 미니프로젝트는 ASSO대비 문제풀이를 진행하였습니다.

이를통해 시험유형을 사전에 확인해 볼 수 있었으며 약한 부분을 확인할 수 있었습니다.

<small>본 실습코드는 보안상 업로드 불가능합니다.</small>

<br>

## **2. 6차 미니프로젝트(1차)**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

crisp-dm을 활용하여 시계열 데이터 모델링, 상품별 판매량 예측을 진행하였습니다.
현시점 대비 2일 뒤 특정 물품들의 판매량을 예측하는 모델을 만들었습니다.

### **1. 데이터 준비**
- 데이터는 `sales_test`, `orders_test`, `oil_price_test`, `products`, `stores`로 구성.
- **데이터 전처리**:
  - 날짜 관련 파생변수 생성 (요일, 월, 계절 등).
  - 카테고리별 판매량 및 방문객 수 통계 생성.
  - LeadTime 기반 판매량 타겟 변수 생성.

### **2. 모델링**

#### **(1) 모델 생성**
- **모델 사용**: LSTM과 CNN.
- **LSTM 모델 구성**:
  - 여러 층의 LSTM과 Dropout, Dense 레이어로 구성.
  - 각 상품별로 적절한 파라미터 설정.
- **CNN 모델 구성**:
  - 아직 구체화되지 않았으나, 이미지와 시계열 데이터를 활용할 예정.

#### **(2) 주요 성능 평가 지표**
- **MAE**: 평균 절대 오차.
- **MAPE**: 평균 절대 백분율 오차.
- **R2**: 결정계수로 예측 모델의 설명력을 측정.

### **3. 데이터 파이프라인 구축**
- **파이프라인 함수**:
  - **입력**: `raw data`.
  - **출력**: `x_test`, `y_test`.
  - **예측값 생성**:
    - 각 `Product_ID`별 모델을 선택해 테스트 데이터에 적용.
  - **결과물**: 실제값과 예측값을 포함한 데이터프레임 생성.

### **4. 비즈니스 평가**

#### **(1) 재고 평가 시뮬레이터**
- **목적**: 평균 재고 금액을 산출하고, 재고 회전율 및 기회 손실을 분석.
- **평가 메트릭**:
  - **일평균 재고량** 및 **재고 금액**.
  - **재고 회전율**.
  - **기회손실 수량**.
- **로직**:
  - 기초재고 = 입고량 + 전날 기말재고.
  - 기말재고 = 기초재고 - 판매량.
  - 발주량 = 예측값 + 안전재고 - 기말재고.

#### **(2) 예측 결과 평가**
- 시뮬레이터를 통해 실제값과 예측값을 기반으로 재고금액, 재고회전율, 기회손실 수량 확인.

<br>

## **3. 느낀점**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
상품별로 LSTM을 이용한 판매량 예측은 성능이 적절한 수준으로 나오는것을 확인하였습니다.
또한 과거의 데이터 분석시 상호 연관성이 높은 칼럼을 연결하면 높은 수준의 정확도를 보이는것을 마지막 날 발표를 통해 확인할 수 있었습니다.

<br>

## **4. 실습 코드**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

6차 미니프로젝트(1차) 실습 코드는 아래 링크에서 확인 가능합니다.    
[언어지능 딥러닝](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/mini_project_06_01)