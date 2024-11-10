---
title: "[KT AIVLE] 미니 프로젝트 4차 (02) keras를 통한 이미지 분석"
description: 
author:
date: 2024-10-28 23:00:00 +0900
categories: [KT aivle school, 미니 프로젝트]
tags: [KT aivle school, mini_project]
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
안녕하세요!

이번에는 aivle school에서 네번째 미니프로젝트를 진행하였습니다.

이번 학습의 목표는 웹캠을 통한 이미지 인식으로 사람을 구별하는 방법입니다!

또한 실습 코드는 아래 링크에서 확인하실 수 있습니다
- [**미니프로젝트 jupyter 학습 코드**](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/mini_project_04)

## **1. 주제**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
- keras를 통한 사람 구별(me, not_me)

keras를 통하여 이진분류를 하는 작업을 진행하였습니다.  

### 01 자료 수집
가장 먼저 이미지 자료 수집을 위하여 사전에 공유된 파이썬 코드를 수정하였습니다.  
이를 통해 본인 이미지를 웹캠(cv2)를 통하여 대략 1만장 정도 수집하였습니다.  

### 02 데이터 전처리
이어서 수집해온 데이터를 전처리하는 절차를 진행하였습니다.  
1. 우선 본인의 데이터와 다른사람의 이미지 데이터를 zip파일로 구글에 업로드 해준 후 colab에서 제공해주는 공간에 압축을 풀어주도록 합니다.
2. `image_dataset_from_directory`를 사용하기 위하여 폴더 구조를 `me`, `not_me` 를 상위 디랙토리로 하고 하위 디렉토리로 `test`, `train`으로 구성하고 해당 디렉토리로 랜덤하게 이미지를 배치하는 코드를 작성하여 줍니다.
3. `image_dataset_from_directory`를 통해 케라스를 통한 이미지 분석을 위한 데이터셋으로 변환해주며 val셋을 생성해주도록 합니다.
4. FaceNet 모델 구조를 사용하기때문에 기존 128차원의 출력부를 fc모델을 사용하여 출력부분을 `sigmoid`로 이진 출력을 하도록 추가 모델링을 진행해주도록 합니다. 
5. 학습된 모델을 검증후 다운로드 합니다

### 03 평가
검증된 모델로 웹캠을통해 이미지 인식결과 어느정도의 정확도를 보이는지 확인합니다.

## **2. 느낀점**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
오늘은 FaceNet을 이용하여 얼굴인식을 하는 방법에대해 확인해보았습니다.

기존에는 이론과 간단한 코드로만 배웠던 keras를 실제 적용시켜보고 학습할 수 있었던 프로젝트 경험이였던것 같습니다!

이만 가보겠습니다!
