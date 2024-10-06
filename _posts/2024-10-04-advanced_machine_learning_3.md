---
title: "[KT AIVLE] 머신러닝 5일차 - 심화학습"
description: 
author:
date: 2024-10-04 22:00:00 +0900
categories: [KT aivle school, 머신러닝]
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

<br/>

## **1. 머신러닝**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
이어서 기본 앙상블부터 정리부터 시작하도록 하겠습니다.

<br/>

## **2. 앙상블**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
앙상블? = 통합!!
![Desktop View](/assets/img/20241003_post/ensemble.JPG){: width="800" height="400"}

### 보팅(voting)
- 여러 모델들(다른 유형의 알고리즘 기반 )의 예측 결과를 투표를 통해 최종 예측 결과를 결정하는 방법
- 하드 보팅: 다수 모델이 예측한 값이 최종 결괏값 (모델 3개가 1을 예측하고 1개가 2를 예측하면 1)
- 소프트 보팅: 모든 모델이 예측한 레이블 값의 결정 확률 평균을 구한 뒤 가장 확률이 높은 값을 최종 선택 (모델 평균구한뒤 가장 높은값)
![Desktop View](/assets/img/20241003_post/voting.JPG){: width="800" height="400"}

### 배깅(Bagging:Bootstrap AGGregatING)
- 데이터로부터 부트스트랩 한 데이터로 모델들을 학습시킨 후, 모델들의 예측 결과를 집계해 최종 결과를 얻는 방법
- 같은 유형의 알고리즘 기반 모델
- 데이터 분할 시 중복을 허용
- 범주형 데이터(Categorical Data)는 투표 방식(Voting)으로 결과를 집계
- 연속형 데이터(Continuous Data)는 평균으로 결과를 집계
- 대표적인 배깅 알고리즘: Random Forest
![Desktop View](/assets/img/20241003_post/bagging.JPG){: width="800" height="400"}
  - 랜덤 포레스트(Random Forest)
    - 여러 Decision Tree 모델이 전체 데이터에서 배깅 방식으로 각자의 데이터 샘플링
![Desktop View](/assets/img/20241003_post/random_forest.JPG){: width="800" height="400"}
    - 두 가지 의미의 randoom
      - 랜덤하게 데이터를 샘플링
      - 개별 모델이 트리를 구성할 때 분할 기준이 되는 Feature를 랜덤하게 선정
        - 무작위로 뽑은 n개의 Feature들 중에서 가장 정보이득이 큰 Feature를 기준으로 트리 분할 → 개별 모델마다 다른 구조의 트리를 구성할 것
    - 주요 하이퍼파라미터

| 파라미터             | 설명                                                                                      |
|---------------------|-------------------------------------------------------------------------------------------|
| `n_estimators`      | - Decision Tree의 개수를 지정합니다 (기본값: 100)<br>- 개수를 늘릴수록 성능 향상이 기대될 수 있지만, 반드시 그런 것은 아닙니다<br>- 개수가 너무 많으면 학습 속도가 저하될 수 있습니다 |
| `max_depth`         | - 트리의 최대 깊이를 지정합니다 (기본값: None)<br>- 기본값 설정 시, 완벽하게 분류될 때까지 또는 노드의 샘플 수가 `min_samples_split`보다 작아질 때까지 분할을 계속합니다 |
| `min_samples_split` | - 노드를 분할하기 위한 최소 샘플 수를 지정합니다 (기본값: 2)<br>- 값이 작을수록 더 많이 분할되어, 트리의 깊이가 깊어지고 과적합이 발생할 가능성이 높아집니다 |
| `min_samples_leaf`  | - 리프 노드가 되기 위한 최소 샘플 수를 지정합니다 (기본값: 1)<br>- 과적합을 방지하는 목적으로 사용됩니다 |
| `max_features`      | - 최선의 분할을 위해 고려할 피처 수를 지정합니다 (기본값: auto)<br>- 'auto' 설정 시, 모든 피처를 사용합니다<br>- 정수형으로 지정하면 해당 수의 피처를, 실수형으로 지정하면 전체 피처의 비율만큼을 사용합니다<br>- 'sqrt'는 전체 피처 수의 제곱근 만큼의 피처를, 'log'는 전체 피처 수의 로그값 만큼의 피처를 사용합니다 |

- 회귀모델 구현
```python
# 불러오기
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error, r2_score
# 선언하기
model = RandomForestRegressor(max_depth=5, n_estimators=100, random_state=1)
# 학습하기
model.fit(x_train, y_train)
# 예측하기
y_pred = model.predict(x_test)
# 평가하기
print(mean_absolute_error(y_test, y_pred))
print(r2_score(y_test, y_pred))
```

- 분류모델 구현
```python
# 불러오기
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import confusion_matrix, classification_report
# 선언하기
model = RandomForestClassifier(max_depth=5, n_estimators=100, random_state=1)
# 학습하기
model.fit(x_train, y_train)
# 예측하기
y_pred = model.predict(x_test)
# 평가하기
print(confusion_matrix(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

### 부스팅(Boosting)
- 같은 유형의 알고리즘 기반 모델 여러 개에 대해 순차적으로 학습을 수행
- 이전 모델이 제대로 예측하지 못한 데이터에 대해서 가중치를 부여
- 예측 성능이 뛰어나 앙상블 학습을 주도
- 배깅에 비해 성능이 좋지만, 속도가 느리고 과적합 발생 가능성 
- 대표적인 부스팅 알고리즘: XGBoost, LightGBM
![Desktop View](/assets/img/20241003_post/boosting.JPG){: width="800" height="400"}
  
  - XGBoost(eXtreme Gradient Boosting)
    - 부스팅을 구현한 대표적인 알고리즘 중 하나가 GBM(Gradient Boost Machine)
    - GBM 알고리즘을 병렬 학습이 가능하도록 구현한 것이 XGBoost

| 장점                          | 설명                                                                                                           |
|-------------------------------|---------------------------------------------------------------------------------------------------------------|
| 높은 예측 성능                | • 분류와 회귀 모두에서 뛰어난 성능을 보임                                                                      |
| 빠른 수행 시간(GBM 대비)       | • 병렬 수행 및 다양한 기능으로 GBM에 비해 빠르게 수행됨<br>• 하지만 여전히 다른 알고리즘에 비해서는 느림         |
| 규제(Regularization)          | • GBM에는 없었던 과적합 규제 기능을 가지고 있음                                                                 |
| 가지치기(Tree Pruning)         | • max_depth 등의 하이퍼파라미터로 가지치기를 할 수 있음<br>• Tree Pruning 기능으로 성능에 이점이 없는 분할은 가지치기 할 수 있음 |
| 내장된 교차 검증 (Cross Validation) | • 반복 수행시마다 내부적으로 학습 데이터와 검증 데이터에 대한 교차 검증을 수행<br>• 지정된 반복 횟수가 아닌 교차 검증을 통해 성능을 확인하여 필요시 조기 중단 가능 |
| 결측치 자체 처리               | • 알아서 결측치를 고려해서 학습을 함(결측치 여부를 노드 분기를 위한 질문에 포함시킴)<br>• 하지만 명시적으로 결측치에 대한 처리를 진행하기를 권고 |

  - 주요 하이퍼파라미터

| 파라미터             | 설명                                                                                                         |
|----------------------|--------------------------------------------------------------------------------------------------------------|
| `learning_rate`      | • 0~1 사이 값을 지정하여 부스팅 스텝을 반복적으로 수행할 때 업데이트되는 학습률 값<br>• 일반적으로 0.01~0.2 사이 값을 지정, 기본값=0.1 |
| `n_estimators`       | • weak learner 개수로, 개수가 많을 수록 일정 수준까지는 성능이 좋아질 수 있음<br>• 너무 많이 지정하면 학습에 많은 시간이 소요됨, 기본값=100 |
| `min_child_weight`   | • 트리에서 추가적으로 분할할 지를 결정하기 위해 필요한 데이터들의 weight 총합<br>• 이 값이 클 수록 분할을 자제함, 기본값=1 |
| `gamma`              | • 트리에서 추가적으로 분할할 지를 결정하기 위해 필요한 최소 손실 감소 값<br>• 이 값보다 큰 손실이 감소된 경우에 분할함, 값이 클 수록 과적합 위험 감소, 기본값=0 |
| `max_depth`          | • 트리 기반 알고리즘의 max_depth와 같은 의미<br>• 0을 지정하면 깊이 제한이 없어짐, 기본값=6 |
| `sub_sample`         | • weak learner가 학습에 사용하는 데이터 샘플링 비율<br>• 과적합이 염려되는 경우 1보다 작은 값으로 설정, 기본값=1(전체 데이터를 기반으로 학습) |
| `colsample_bytree`   | • 트리 생성에 필요한 Feature 샘플링 비율<br>• Feature가 많은 경우 과적합을 조절하기 위해서 사용, 기본값=1(모든 Feature 사용) |
| `reg_lambda`         | • L2 규제 적용 값, Feature가 많은 경우 이 값을 키워 과적합 위험을 줄일 수 있음, 기본값=1 |
| `reg_alpha`          | • L1 규제 적용 값, Feature가 많은 경우 이 값을 키워 과적합 위험을 줄일 수 있음, 기본값=0 |

- 회귀모델 구현
```python
from xgboost import XGBRegressor
from sklearn.metrics import mean_absolute_error, r2_score
# 선언하기
model = XGBRegressor(max_depth=5, n_estimators=100, random_state=1)
# 학습하기
model.fit(x_train, y_train)
# 예측하기
y_pred = model.predict(x_test)
# 평가하기
print(mean_absolute_error(y_test, y_pred))
print(r2_score(y_test, y_pred))
```

- 분류모델 구현
```python
# 불러오기
from xgboost import XGBClassifier
from sklearn.metrics import confusion_matrix, classification_report
# 선언하기
model = XGBClassifier(max_depth=5, n_estimators=100, random_state=1)
# 학습하기
model.fit(x_train, y_train)
# 예측하기
y_pred = model.predict(x_test)
# 평가하기
print(confusion_matrix(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

### 스태킹(Stacking)
- 여러 모델의 예측 값을 최종 모델의 학습 데이터로 사용하여 예측하는 방법
- 예를 들면
  - KNN, Logistic Regression, XGBoost 모델을 사용해 4종류 예측값을 구한 후
  - 이 예측 값을 최종 모델인 Randomforest 학습 데이터로 사용
-  기본 모델로 4개 이상 선택해야 좋은 결과를 기대할 수 있음 
![Desktop View](/assets/img/20241003_post/stacking.JPG){: width="800" height="400"}

<br/>

## **3. 실습 코드**
머신러닝 또한 실습 위주로 진행하였으며 코드는 git에 업로드 하였습니다.  
[실습코드](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/ML/2024.09.26)