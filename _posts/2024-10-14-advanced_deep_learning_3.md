---
title: "[KT AIVLE] 딥러닝 3일차 - 심화학습"
description: 
author:
date: 2024-10-14 19:15:15 +0900
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

### 알고리즘 정리

| Model               | 개념                                                                                                                                  | 전제 조건                                                   | 성능                                                                          |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------|
| **선형회귀**        | - 오차를 최소화하는 직선, 평면                                                                                                        | - NaN 조치 <br> - 가변수화 <br> - x들 간 독립               | - 변수 선택 중요 <br> - x가 많을수록 복잡                                    |
| **로지스틱회귀**    | - 오차를 최소화하는 직선, 평면 <br> - 직선을 로지스틱 함수로 변환 (0~1 사이 값으로)                                                     | - NaN 조치 <br> - 가변수화 <br> - x들 간 독립               | - 변수 선택 중요 <br> - x가 많을수록 복잡                                    |
| **KNN**             | - 예측할 데이터와 train set과의 거리 계산 <br> - 가까운 [k개 이웃의 y]의 평균으로 예측                                                  | - NaN 조치 <br> - 가변수화 <br> - 스케일링                   | - 주요 hyper-parameter <br>   - n_neighbors : k 작을수록 복잡 <br>   - metric : 거리계산법 |
| **Decision Tree**   | - 정보전달량 = 부모 불순도 - 자식 불순도 <br> - 정보 전달량이 가장 큰 변수를 기준으로 split                                              | - NaN 조치 <br> - 가변수화                                   | - 주요 hp <br>   - max_depth : 클수록 복잡 <br>   - min_samples_leaf : 작을수록 복잡      |
| **Random Forest**   | - 여러 개의 트리 <br> - 각각 예측 값의 평균 <br> - 행과 열에 대한 랜덤 : 조금씩 다른 트리들 생성                                       | - NaN 조치 <br> - 가변수화                                   | - 주요 hp <br>   - n_estimators <br>   - max_features <br>   기본값으로도 충분!          |
| **Gradient Boost**  | - 여러 개의 트리 <br> - 트리를 더해서 하나의 모델로 생성 <br> - 더해지는 트리는 오차를 줄이는 모델                                      | - NaN 조치 <br> - 가변수화                                   | - 주요 hp <br>   - n_estimators <br>   - learning_rate <br> XGB, LGBM : 과적합 회피 규제  |

## **2. 성능 관리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

과적합 : 모델이 복잡해지면, 가짜 패턴 까지 학습하게 됨.  
따라서 적절한 모델을 만들어야됨  
- 적절한 복잡도 지점 찾기
  - 알고리즘(모델)마다 각각 복잡도 조절 방법이 있음.
  - 복잡도를 조금씩 조절해 가면서 (보통 하이퍼파라미터 조정)
  - Train error와 Validation error를 측정하고 비교 (관점은 Validation error!)
- 딥러닝에서 조절할 대상
  - Epoch와 learning_rate
  - 모델 구조 : hidden layer 수, node 수
  - 미리 멈춤 Early Stopping
  - 임의 연결 끊기 Dropout
  - 가중치 규제하기 Regularization(L1, L2)

### 파라미터 수
파라미터가 많을 수록 복잡한 모델
- torchsummary 라이브러리의 summary 함수 사용

### **미리 멈춤(Early Stopping)**
반복횟수(Epoch)가 많으면 과적합 될 수 있음
- 어느 순간부터 val_err가 더이상 줄지않고 증가할때

EarlyStopping 옵션
- monitor : 기본값 val_loss
- min_delta : 오차(loss)의 최소값에서 변화량(줄어드는 량)이 몇 이상 되어야 하는지 지정. (기본값 0) 
- patience : 오차가 줄어들지 않는 상황을 몇 번(epoch) 기다려줄 건지 지정. (기본값 0)
```python
from keras.callbacks import EarlyStopping
es = EarlyStopping(monitor = 'val_loss', min_delta = 0, patience = 0)

model.fit(x_train, y_train, epochs = 100, validation_split = .2, callbacks = [es])
```

### **연결 임의로 끊기(Dropdut)**
학습시, 신경망의 일부 뉴런을 임의로 비활성화  
학습 시 적용 절차
- 훈련 배치에서 랜덤하게 선택된 일부 뉴런을 제거
- 제거된 뉴런은 해당 배치에 대한 순전파 및 역전파 과정에서 비활성화
- 이를 통해 뉴런들 간의 복잡한 의존성을 줄여 줌
- 매 epochs 마다 다른 부분 집합의 뉴런을 비활성화 ➔ 앙상블 효과
```python
model3 = Sequential( [Input(shape = (nfeatures,)),
                      Dense(128, activation= 'relu'),
                      Dropout(0.4),
                      Dense(64, activation= 'relu'),
                      Dropout(0.4),
                      Dense(32, activation= 'relu'),
                      Dropout(0.4),
                      Dense(1, activation= 'sigmoid')] )
```

### 모델 저장
```python
# 모델 저장
model1.save('hanky.keras')
#모델 로딩
from keras.models import load_model
model2 = load_model('hanky.keras')
```

<br>

## **1. 요약정리**
- 딥러닝 모델 성능 높이기
  - 데이터
    - 입력 데이터 정제, 적절한 전처리
    - 데이터 늘리기: 열(적절한 feature 추가), 행(데이터 건수 늘리기)
  - 모델 구조
    - 은닉층, 노드 수 늘리기: 성능이 증가할 때까지
    - activation
  - 학습
    - epochs, learning_rate, optimizer
- 과적합 문제
  - 모델링 목적: 모집단 전체에서 두루 잘 맞추는 (적당한) 모델 만들기
  - 과적합: 학습 데이터에서만 높은 성능, 다른 데이터에서는 낮은 성능
- 과적합 문제 해결
  - 데이터 건수 늘리기
  - 모델 복잡도 조절하기 ➔ 가중치 규제(Regularization)
  - 반복 학습 횟수(epochs) 적당히 ➔ early stopping
- 모델 저장하기
  - 최종 모델 저장
  - 체크포인트에서 모델 저장
    - 성능이 개선되면 저장하기 가능.

<br>

## **3. 실습 코드**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
딥러닝 또한 실습 위주로 진행하였으며 코드는 git에 업로드 하였습니다.  
[실습코드](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/DL)