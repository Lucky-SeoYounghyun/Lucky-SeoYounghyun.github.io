---
title: "[KT AIVLE] 딥러닝 2일차 - 심화학습"
description: 
author:
date: 2024-10-11 22:15:17 +0900
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

<br>

## **1. 딥러닝 정리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
오늘은 딥러닝 12일차입니다! 많은것을 배웠으며 정리할것도 많을꺼 같습니다!

<br>

## **2. Feature Representation**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
Hidden layer에서는 뭔일이 일어날까?
- 학습
  - 예측값과 실제 값을 비교하며, loss function으로 오차를 계산하고, 오차를 줄이기 위해, 파라미터를 업데이트한다.
- 정리
  - 기존 데이터를 받아서 새로운 특징을 만들어냄
  - 그 특징은 예측값과 실제 값 사이의 오차를 최소화 해주는 유익한 특징
  - hidden layer에서는 기존 데이터가 새롭게 표현 되었으며 Feature Engineering가 진행되었음
![Desktop View](/assets/img/20241010_post/DL_ML.JPG){: width="800" height="400"}

<br>

## **2. 이진 분류**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
- Yes or No
![Desktop View](/assets/img/20241010_post/0_1.JPG){: width="800" height="400"}
- Node의 결과를 변환해주는 함수가 필요 : 활성함수 라고 함
![Desktop View](/assets/img/20241010_post/af_output.JPG){: width="800" height="400"}
- Loss Function : binary_crossentropy
  - 모델의 예측 값과 실제 레이블 간의 차이를 로그 확률로 계산하여 손실을 측정
  - 출력 결과를 0 or 1로 출력
- 모델 평가 : Confusion Matrix

<br>

## **2. 다중 분류**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
Node 수
- 노드수 : y의 범주 수
Softmax
- 각 class별로 예측한 값을 하나의 확률 값으로 변환
다중 분류 오차 계산
- cross entropy : 실제값이 1인 class와 예측 확률 비교  
![Desktop View](/assets/img/20241010_post/cross_entropy.JPG){: width="800" height="400"}
- 다중분류 모델링을 위한 전처리
  - 다중분류 : T가 범주이고, 범주가 3개 이상!
![Desktop View](/assets/img/20241010_post/multi_class_classification.JPG){: width="800" height="400"}
- 방법1 : 정수 인코딩 + sparse_categorical_crossentropy
  - y : Integer Encoding
  - loss='sparse_categorical_crossentropy’
  - Y는 인덱스로 사용됨 : 해당 인덱스의 예측확률로 계산. 
  - $\text{Loss} = -\log(\hat{y})$

```python
from sklearn.preprocessing import LabelEncoder

#선언
int_encoder = LabelEncoder()

#인코딩
data['Species_encoded'] = int_encoder.fit_transfoem(data['Species'])
data.head()

#범주 조회
int_encoder.classes_ 
```

- 방법2 : 원핫 인코딩 + categorical_crossentropy
  - y : One-Hot Encoding
  - loss='categorical_crossentropy’
  - $\text{Loss} = - \sum \mathbf{y} \cdot \log(\hat{y})$

```python
# sklearn
from sklearn.preprocessing import OneHotEncoder

# OneHotEncoder 선언
oh_encoder = OneHotEncoder()

# 데이터를 원핫인코딩하여 변환(input : 2차원)
encoded_y1 = oh_encoder.fit_transform(data[['Species']])

# 변환된 데이터 확인
print(encoded_y1.toarray())

# keras
from keras.utils import to_categorical

# 이미 정수 인코딩된 y를 이용하여 적용
encoded_y2 = to_categorical(data['Species_encoded'], 3)

print(encoded_y2)
```

이진 분류와 다른점
- 다중 분류 모델 출력층
  - 노드 수 : 다중 분류 클래스의 수와 동일
  - 활성화 함수 : softmax
예측 결과에 대한 후속 처리
- 예측결과 : 각 클래스별 확률 값
- 그중 가장 큰 값의 인덱스로 변환
  - np.argmax()

<br>

## **3. 실습 코드**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
딥러닝 또한 실습 위주로 진행하였으며 코드는 git에 업로드 하였습니다.  
[실습코드](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/DL)