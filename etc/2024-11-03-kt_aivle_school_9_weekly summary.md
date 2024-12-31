---
title: "[KT AIVLE] 9주차 정리(4차 미니프로젝트)"
description: 
author:
date: 2024-11-03 13:00:00 +0900
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
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">4차 미니프로젝트</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">4차 미니프로젝트</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">4차 미니프로젝트</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">4차 미니프로젝트</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">4차 미니프로젝트</td>
    </tr>
  </table>
</div>


<br>

## **1. FaceNet 모델 제작**
- **데이터 준비**: 
  - 본인 얼굴과 다른 사람 얼굴 이미지를 Training, Validation, Test 세트로 분할.
  - 이미지를 160x160 크기로 스케일링.

- **FaceNet 모델 생성**:
  - Pretrained FaceNet 모델을 불러와 가중치 적용 및 레이어 일부 고정.
  - Dense 레이어를 추가하여 이진 분류 문제로 변형.

- **학습 및 저장**:
  - 모델 학습 시 EarlyStopping, ModelCheckpoint 활용.
  - 학습 완료 후 `.keras` 파일로 저장 및 다운로드.

<br>

## **2. YOLO 활용 실습**

### **(1) YOLO-cls**
- **데이터 준비**:
  - 본인 얼굴과 다른 사람 얼굴 데이터를 YOLO-cls 요구 형식(`train`, `val`, `test`)으로 재구성.
  
- **모델 학습**:
  - YOLOv11n-cls 모델로 10 Epoch 동안 학습.
  - 학습 후 Top-1 및 Top-5 정확도 평가.

- **모델 저장**:
  - 최적 가중치를 `.pt` 파일로 저장 및 다운로드.

### **(2) YOLO-detect**
- **데이터 준비**:
  - 얼굴 인식 데이터를 크롭 및 리사이즈하여 라벨과 함께 YOLO-detect 요구 형식으로 구성.
  - 데이터셋 정보를 포함한 YAML 파일 생성.

- **모델 학습**:
  - YOLOv11n 모델을 사용해 학습(10 Epoch).
  - 하이퍼파라미터 최적화 적용.

- **모델 저장 및 추론**:
  - 학습된 모델로 얼굴 감지 수행.
  - 최적화된 가중치를 `.pt` 파일로 저장.

<br>

## 3 ) 느낀점
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
다중 이미지 분류 결과가 낮게 나온 점을 확인하였습니다. 이는 여러 요인에 기인할 수 있으나, 현재 사용된 데이터셋이 단일 분류 문제에 적합하도록 구성되었다는 점이 주요 원인으로 보입니다.  
이를 개선하기 위해서는 한 이미지에 다양한 클래스의 요소를 포함한 데이터셋을 활용하여 모델을 학습시키는 접근이 필요할 것입니다..  
이러한 방법은 보다 효과적인 다중 이미지 분류 모델을 구축하는 데 기여할 수 있을것으로 생각됩니다.  

이번 프로젝트를 통해 학습 기반 알고리즘과 모델 설계에서 하이퍼파라미터 튜닝과 모델 구조의 중요성도 크지만, 무엇보다 데이터의 품질과 적합성이 성공적인 모델 성능의 핵심이라는 점을 깊이 깨달을 수 있었습니다.  

<br>

## 4 ) 실습 코드
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

실습코드는 아래 링크에서 확인 가능합니다.    
[3차 미니 프로젝트](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/mini_project_04)