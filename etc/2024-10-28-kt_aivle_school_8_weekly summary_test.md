---
title: "[KT AIVLE] 8주차 정리(시각지능 딥러닝)"
description: 
author:
date: 2024-10-28 12:00:00 +0900
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
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">시각지능 딥러닝</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">시각지능 딥러닝</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">시각지능 딥러닝</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">시각지능 딥러닝</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">시각지능 딥러닝</td>
    </tr>
  </table>
</div>


<br>

## **1. 시각지능 딥러닝 기초 및 데이터 전처리 **
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### **CNN(Convolutional Neural Network)**
- 이미지 데이터를 처리하기 위한 기본 구조 학습.
- **핵심 요소**
  - **Feature Map 계산식**: 
    $$n_{\text{out}} = \left\lfloor \frac{n_{\text{in}} + 2p - k}{s} + 1 \right\rfloor$$
    - \( n_{\text{in}} \): 입력 이미지 크기, \( k \): 필터 크기, \( s \): 이동 보폭(Stride), \( p \): 패딩.
  - **Padding**: 외곽 데이터 보존을 위해 추가(Zero Padding).
  - **Pooling**: 연산량 감소 및 특성 요약.
    - Max Pooling: 최대값 반환.
    - Average Pooling: 평균값 반환.

### **Standardization(스케일링)**
- **전체 스케일링**:
  - 전체 데이터 평균과 표준편차로 스케일링.
  - 장점: 빠르고 일관성 있는 결과.
- **채널별 스케일링**:
  - 채널별로 독립적으로 스케일링.
  - 장점: 채널 간 특성 보존, 색상 정보 유지.

| **스케일링 종류** | **장점**                             | **단점**                     |
|-------------------|-------------------------------------|-----------------------------|
| 채널별 스케일링    | 채널 특성 보존, 색상 정보 유지         | 처리 시간 증가              |
| 전체 스케일링      | 일관된 스케일 적용, 빠른 처리          | 색상 왜곡 가능성, 채널 차이 상실 |

<br>

## **2. 증강 및 모델링 기초**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### **데이터 증강(Augmentation)**
- 데이터 다양성을 높이고 일반화 성능 향상.
  - **RandomRotation**: 이미지를 회전.
  - **RandomTranslation**: 가로/세로로 이동.
  - **RandomZoom**: 확대/축소.
  - **RandomFlip**: 좌우/상하로 뒤집기.
- **주의**: 과도한 증강은 데이터 훼손으로 성능 저하 가능.

### **Object Detection 개념**
- **Localization**: 단일 객체의 위치를 Bounding Box로 지정.
- **Object Detection**: 다수 객체의 위치를 Bounding Box로 지정.
- **핵심 개념**:
  - **Bounding Box**: 객체의 위치를 나타내는 최소 영역.
  - **Confidence Score**: 예측 신뢰도.
  - **IoU**: 박스 중복 영역 크기.
  - **NMS(Non-Max Suppression)**: 중복 박스를 제거.
  - **Precision/Recall**: 모델 성능 측정 지표.
  - **AP/mAP**: 클래스별 Average Precision과 전체 클래스의 평균.

<br>

## **3. YOLO 및 프로젝트 기초**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### **YOLO(Object Detection 모델)**
- Object Detection의 대표 모델.
- **YOLO 기본 사용법**:
  ```python
  from ultralytics import YOLO
  model = YOLO('yolov8n.pt')
  model.train()
  model.val()
  model.predict()
  ```
- ### **YOLO 활용 팁**
  - **Colab 사용 시 `wandb` 오류 해결:**
    ```python
    import os
    os.environ['WANDB_MODE'] = 'disabled'

## **4. Roboflow**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

Computer Vision 데이터 준비 및 학습에 최적화된 플랫폼.
End-to-End 지원으로 데이터 전처리, 증강, 모델 학습 간소화.

<br>

## **5. 모델 저장 및 로딩**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### **모델 저장**

1. **학습 중 가장 좋은 모델 저장**:
    ```python
    from keras.callbacks import ModelCheckpoint
    mcp = ModelCheckpoint(filepath='./model1.keras',
                          monitor='val_loss',
                          save_best_only=True,
                          save_weights_only=False)
    ```

2. **현재 모델 저장**:
    ```python
    model.save('./my_model.keras')
    ```

### **모델 로드**

- **저장된 모델 불러오기**:
    ```python
    from keras.models import load_model
    model = load_model('./my_model.keras')
    ```

<br>

## 2 ) 실습 코드
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
이번 주는 CNN의 기본 개념, 데이터 증강(Augmentation), Object Detection의 주요 기법 과 YOLO를 활용한 Object Detection 모델 실습과 데이터 관리에 대한 Roboflow 사용법 학습하였습니다.

시각지능 딥러닝 코드는 git에 업로드 하였습니다.  
[시각지능 딥러닝](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/visual_intelligence)