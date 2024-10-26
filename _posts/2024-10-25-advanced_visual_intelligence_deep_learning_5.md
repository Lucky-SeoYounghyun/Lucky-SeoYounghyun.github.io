---
title: "[KT AIVLE] 시각지능 딥러닝 5일차 - 심화학습"
description: 
author:
date: 2024-10-25 17:21:41 +0900
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
금일은 프로젝트에 쓰이는 다양한 기법들과 Object Detection에대해 학습하였습니다.

<br>

## **1. 지난 학습 복습 **
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

Classification + Localization
- Localization : 단 하나의 Object 위치를 Bounding Box로 지정하여찾음
- Object Detection : 여러 개의 Object들의 위치를 Bounding Box로 지정하여찾음

Object Detection 주요 개념
- Bounding Box
  - 하나의Object가포함된 최소크기박스
  - 위치정보 : x min, y min, x max, y max, x center, y center, width, height
- Class Classification
  - 클래스 분류
- Confidence Score
  - bounding box안에 해당 물체가 있는지에대한 확신 정도 //확율아님!!
- IoU
  - 두박스의중복영역크기를통해측정 -> 겹치는영역이넓을수록음!!
- NMS - predict(추론)과정에서 작동함
  - 동일Object에대한 중복박스제거
    1. Confidence score 임계값이하의 Bounding Box 제거
    2. 남은Bounding Box들을 Confidence score 내림차순으로정렬
    3. 첫Bounding Box(Confidence score가 가장높은!)와의IoU 값이임계값이상 인다른박스들을제거
    4. Bounding Box가 하나될때까지반복

- Precision, Recall, AP, mAP
  - confidence score threshold에따라 모델이 알아서 precision과 recall값을 계속 확인함
    - precision - 참중참
    - Recall - 실제A중 예측 A확률
  AP(Average Precision)
    - Prevision - Recall Curve 그래프 아래 면적
  mAP(mean Average Precision)
    - 각 클래스별 AP를 합산하여 평균을 낸것
- Annotation
  - 이미지 내 Detection 정보를 별도의 설명 파일로 제공되는것

<br>

## **2. YOLO**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

기본 구조
```python
!pip install ultralytics
from ultralytics import YOLO
model = YOLO()
model.train()
model.val()
model.predict()
```

YOLO의 역사
![Desktop View](/assets/img/20241025_post/yolo.JPG){: width="800" height="400"}

현재 yolo11n버전에 살짝 이슈가 있음
```
wandb: Paste an API key from your profile and hit enter, or press ctrl+c to quit: ··········
```
로컬에서는 문제가 없으나 colab과같이 온라인 환경에서는 위와같이 잘못된 wandb가 실행된다. 이를위해 아래와같이 disabled를 해줘야한다.
```python
import os
os.environ['WANDB_MODE'] = 'disabled'
```

## **2. roboflow**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
[**roboflow**](https://universe.roboflow.com/)
- Computer Vision End-to-End 개발 가능 

<br>

## **4. 정리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
금일은 이전에 배운내용 정리와 Object Detection 주요 개념을 학습하였습니다.

이만 가보겠습니다!

실습 코드는 아래 링크에서 확인 가능합니다.
- [**시각지능**](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/visual_intelligence)
