---
title: "[KT AIVLE] 시각지능 딥러닝 4일차 - 심화학습"
description: 
author:
date: 2024-10-23 17:21:41 +0900
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

## **1. model save&load **
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
모델 저장방법은 아래와 같다

1. 학습시 베스트를 저장
```python
mcp = ModelCheckpoint(filepath='./model1.keras',       # 모델 저장 경로
                      monitor='val_loss',              # 모델 저장의 관심 대상
                      verbose=1,                       # 어느 시점에서 저장되는지 알려줌
                      save_best_only=True,             # 최고 성능 모델만 저장
                      save_weights_only=False)         # True : 가중치만 저장| False : 모델 구조 포함하여 저장

history = model.fit(train_x, train_y, validation_data=(val_x, val_y),
                    epochs=10000, verbose=1,
                    callbacks=[es, mcp]
                    )
```

2. 현재 모델을 저장
```python
model.save('./my_first_save.keras')
```

<br>

## **2. Object Detection**
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
  - bounding box안에 해당 물체가 있는지에대한 확신 정도
- IoU
  - 두박스의중복영역크기를통해측정 -> 겹치는영역이넓을수록좋은예
- NMS
  - 동일Object에대한 중복박스제거
    1. Confidence score 임계값이하의 Bounding Box 제거
    2. 남은Bounding Box들을 Confidence score 내림차순으로정렬
    3. 첫Bounding Box(Confidence score가 가장높은!)와의IoU 값이임계값이상 인다른박스들을제거
    4. Bounding Box가 하나될때까지반복
- Precision, Recall, AP, mAP
- Annotation

<br>

## **3. 프로젝트시 유용한 함수**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

- Extra: image_dataset_from_directory
```python
idfd_train = image_dataset_from_directory('/content/drive/MyDrive/my_data/my_mnist2',
                                                      label_mode='categorical',
                                                      color_mode='grayscale',
                                                      image_size=(28,28),
                                                      )
```

<br>

## **4. 정리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
금일은 이전에 배운내용 정리와 Object Detection 주요 개념을 학습하였습니다.

이만 가보겠습니다!

실습 코드는 아래 링크에서 확인 가능합니다.
- [**시각지능**](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/visual_intelligence)
