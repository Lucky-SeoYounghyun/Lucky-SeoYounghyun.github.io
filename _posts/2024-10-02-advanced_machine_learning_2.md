---
title: "[KT AIVLE] 머신러닝 4일차 - 심화학습"
description: 
author:
date: 2024-10-02 21:00:00 +0900
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
이어서 기본 알고리즘 정리부터 시작하도록 하겠습니다.

<br/>

## **2. 기본 알고리즘**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

### **2.4 ) Logistic Regression(분류모델만 가능)**
- 로지스틱 함수
![Desktop View](/assets/img/20241002_post/logistic_fun.JPG){: width="800" height="400"}
  - 시그모이드 함수라고도 부름
  - 확률 값 𝑝 는 선형 판별식 값이 커지면 1, 작아지면 0에 가까운 값이 됨
  - (-∞, ∞) 범위를 갖는 선형 판별식 결과로 (0, 1) 범위의 확률 값을 얻게 됨
  - 기본적으로 확률 값 0.5를 임계값(Threshold)로 하여 이보다 크면 1, 아니면 0으로 분류함   
> 𝑥 데이터가 주어졌을 때 확률을 예측하는 로지스틱 회귀분석은 학습 데이터를 잘 설명하는 선형 판별식의 기울기(𝑎)와 절편(𝑏)을 찾는 문제
- 모델 구현
```python
# 불러오기
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import confusion_matrix, classification_report
# 선언하기
model = LogisticRegression()
# 학습하기
model.fit(x_train, y_train)
# 예측하기
y_pred = model.predict(x_test)
# 평가하기
print(confusion_matrix(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

<br/>

## **3. K-Fold Cross Validation**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

- Random split의 문제
  - 새로운 데이터에 대한 모델의 성능을 예측하지 못한 상태에서 최종 평가를 수행
  - 검증용 데이터가 모델의 일반화된 성능을 예측할 수 있게 도와 주기는 하지만 더욱 정교한 평가 절차가 필요함
![Desktop View](/assets/img/20241002_post/random_split.JPG){: width="800" height="400"}

### K-분할 교차검증
- 모든 데이터가 평가에 한번, 학습에 k-1번 사용(단, k는 2 이상이 되어야 함(최소한 한 개씩의 학습용, 검증용 데이터가 필요))
- K개의 분할(Fold)에 대한 성능을 예측 → 평균과 표준편차 계산 → 일반화 성능
![Desktop View](/assets/img/20241002_post/k_fold_cross.JPG){: width="800" height="400"}
- 장단점
  - 장점
    - 모든 데이터를 학습과 평가에 사용할 수 있음
    - 반복 학습과 평가를 통해 정확도를 향상시킬 수 있음
    - 데이터가 부족해서 발생하는 과소적합 문제를 방지할 수 있음
    - 평가에 사용되는 데이터의 편향을 막을 수 있음
    - 좀 더 일반화된 모델을 만들 수 있음
  - 단점
    - 반복 횟수가 많아서 모델 학습과 평가에 많은 시간이 소요됨
- K-분할 교차검증 사용방법
  - 모델 선언 후 cross_val_score(모델, x_train, y_train, 분할 개수)
  - 기본 분할 개수(cv) 값은 5이며, 필요에 따라 적절히 조절
  - cross_val_score 함수 결과로 얻은 성능들의 평균을 모델의 성능으로 봄
  - 물론 실제 평가에서 얻은 성능이 이 성능보다 더 높거나 낮을 수 있음
```python
# 1단계: 불러오기
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import cross_val_score
# 2단계: 선언하기
model = DecisionTreeClassifier(max_depth=3)
# 3단계: 검증하기
cv_score = cross_val_score(model, x_train, y_train, cv=10)
# 확인
print(cv_score)
print(cv_score.mean())
```

<br/>

## **4. Hyperparameter 튜닝**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

### Hyperparameter
- 알고리즘을 사용해 모델링할 때 모델 성능을 최적화하기 위해 조절할 수 있는 매개변수
- 튜닝하는 방법은 지식과 경험...그리고 무한 try
- 다양한 시도 방법
  - Grid Search
  - Random Search
- KNN
  - k 값이 가장 클 때(=전체 데이터 개수) 가장 단순 모델 -> 평균, 최빈값에 근사해짐
  - k 값이 작을 수록 복잡한 모델
  - 거리 계산법(metric)에 따라 성능이 달라질 수 있음(유클리드, 맨하튼)
- Decision Tree(이 모델은 과적합으로 유명함)
  - max_depth
    - 이 값이 작을 수록 트리 깊이가 얕아저 모델이 단순해짐
  - min_samples_leaf
    - leaf가 되기 위한 최소한의 샘플 데이터 수
    - 이 값이 클 수록 모델이 단순해 짐
  - min_samples_split
    - 노드를 분할하기 위한 최소한의 샘플 데이터 수
    - 이 값이 클 수록 모델이 단순해 짐

### Random Search, Grid Search
- 파라미터 값에 대한 고민(뭐가 최선일까? 일일히 다 해봐야하는걸까?)
  - 이를 위해 등장한 Random Search, Grid Search
  - Grid Search
    - 성능을 테스트할 파라미터 값의 범위를 지정(딕셔너리 형태)
    - 파라미터 값 범위를 모두 사용하는 Grid Search 모델 선언 후 학습
    - 가장 좋은 성능을 보인 파라미터 값으로 자동으로 학습
  - Random Search
    - 성능을 테스트할 파라미터 값의 범위를 지정(딕셔너리 형태)
    - 파라미터 값 범위에서 몇 개 선택할 지 정하여 Random Search 모델 선언 후 학습
    - 가장 좋은 성능을 보인 파라미터 값으로 자동으로 학습
  - 딕셔너리 형태로 파라미터 범위 지정
```python
# 파라미터 하나의 경우
param = {'n_neighbors': range(1, 101)}
# 파라미터 두 개 경우
param = {'n_neighbors': range(1, 101), 
'metric': ['euclidean', 'manhattan']}
```
- Random Search 사용 법
  1. 함수 불러오기
```python
# 함수 불러오기
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import RandomizedSearchCV
```
  2. 파리미터 값 범위 지정
    - 딕셔너리로 값 범위 지정
    - 미지정 파라미터 값은 기본값으로 지정됨
    - 리스트 형태 또는 range() 함수 등을 사용해 적절한 step 설정
```python
# 파라미터 선언
param = {'n_neighbors': range(1, 500, 10), 
'metric': ['euclidean', 'manhattan']}
```
  3. 모델 선언
    - 기본 모델 선언
    - Random Search 모델 선언
    - n_iter에 수행 횟수 / (임의로 선택할 파라미터 조합 수) 지정
    - 적절한 cv 값 지정
```python
# 기본모델 선언
knn_model = KNeighborsClassifier()
# Random Search 선언
model = RandomizedSearchCV(knn_model,
param,
cv=3, 
n_iter=20)
```
  4. 모델 학습
    - 기본 모델이 아니라 Random Search 모델 학습
    - 모델 학습 과정이 최선의 파라미터 값을 찾는 과정
    - 경우에 따라 많은 시간이 소요 될 수 있음
```python
# 학습하기
model.fit(x_train, y_train)
```
  5. 결과 확인
    - 학습 결과를 열어보면 딕셔너리 형태
```python
# 수행 정보
model.cv_results_
# 최적 파라미터
model.best_params_
# 최고 성능
model.best_score_
```
  6. 예측 및 평가
    - 최선의 파라미터 값으로 모델이 자동으로 학습된 상태

- Grid Search 사용 법
  - 다음 사항을 참고해 Random Search와 같은 과정으로 진행
    - 함수가 다름: GridSearchCV
    - n_iter 옵션을 지정하지 않음
    - 넓은 범위와 큰 Step으로 설정한 후 범위를 좁혀 나가는 방식으로 시간을 단
```python
# 함수 불러오기
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import GridSearchCV
# 파라미터 선언
param = {'n_neighbors': range(1, 500, 10), 'metric': ['euclidean', 'manhattan']}
# 기본모델 선언
knn_model = KNeighborsClassifier()
# Grid Search 선언
model = GridSearchCV(knn_model, param, cv=3)
```

- 보다 정확도 높게 예측하려면?
  - Random Search + Grid Search 적용 고려
    - Random Search로 가장 높은 값을 찾은다음 Grid Search를 통해 인근값중 최고값을 선정

<br/>

## **5. 실습 코드**
머신러닝 또한 실습 위주로 진행하였으며 코드는 git에 업로드 하였습니다.  
[실습코드](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/ML/2024.09.26)