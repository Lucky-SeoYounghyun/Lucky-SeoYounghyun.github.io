---
title: "[KT AIVLE] 5주차 정리(머신러닝)"
description: 
author:
date: 2024-10-06 13:00:00 +0900
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
이번주는 징검다리 휴무가 있었으며 이를 통해 머신러닝을 정리할 수 있는 시간이 있었습니다.
이에 머신러닝 심화과정은 해당 일마다 올렸습니다.

>[ 머신러닝 3일차 - 심화학습](https://lucky-seoyounghyun.github.io/posts/advanced_machine_learning/)  
[ 머신러닝 4일차 - 심화학습](https://lucky-seoyounghyun.github.io/posts/advanced_machine_learning_2/)  
[ 머신러닝 5일차 - 심화학습](https://lucky-seoyounghyun.github.io/posts/advanced_machine_learning_3/)  

이번 주간 정리에는 최종 summary만 하도록 하겠습니다.

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
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">머신러닝</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">휴무</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">머신러닝</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">휴무</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">머신러닝</td>
    </tr>
  </table>
</div>

## **1. 머신러닝**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

최종 summary를 진행하겠습니다.

머신러닝은 학습 방법에따라
- 지도학습
- 비지도 학습
- 강화학습
이렇게 세가지로 나누어지며
과제에 따른 분류로는
- 분류 문제
- 회귀 문제
- 클러스터링 문제
가 있다.
또한 학습 방법과 평가방법에 따른 모델을 나눌 수 있으면 이는 다음과 같다

|                    | **분류 문제**                                                                                                      | **회귀 문제**                                                                                                        |
|--------------------|--------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| **학습 방법**      | • DecisionTreeClassifier <br> • KNeighborsClassifier <br> • LogisticRegression <br> • RandomForestClassifier <br> • XGBClassifier | • LinearRegression <br> • KNeighborsRegressor <br> • DecisionTreeRegressor <br> • RandomForestRegressor <br> • XGBRegressor      |
| **평가 방법**      | • accuracy_score <br> • recall_score <br> • precision_score <br> • classification_report <br> • confusion_matrix               | • mean_absolute_error <br> • mean_squared_error <br> • root mean_squared_error <br> • mean_absolute_percentage_error <br> • r2_score |


```python
# 회귀모델 성능 평가
from sklearn.metrics import mean_squared_error
from sklearn.metrics import mean_absolute_error
from sklearn.metrics import mean_absolute_percentage_error
from sklearn.metrics import r2_score
print(mean_absolute_error(y_test, y_pred))

# 분류모델 성능 평가
from sklearn.metrics import accuracy_score
from sklearn.metrics import precision_score
from sklearn.metrics import recall_score
from sklearn.metrics import f1_score
from sklearn.metrics import confusion_matrix
from sklearn.metrics import classification_report
print(accuracy_score(y_test, y_pred))
print(precision_score(y_test, y_pred, average=None))
```
기본 알고리즘으로는
- Linear Regression : 직선으로 추적한다~ / 회귀모델만 가능
  - 기울기 : 가중치(coef_), y절편 : 편향(intercept)
- KNN(K-Nearest Neighbor) : 인근에 누가있냐 확인~ / 회귀 - 분류 모델 둘다 가능
  - scaling 중요!
  - n_neighbors값 조절을 통해 주변 갯수 조절
- Decision Tree : 스무고개 게임을 통해 확인~ / 회귀 - 분류 모델 둘다 가능
  - 과적합으로 유명하다...트리깊이 제한 필요!
  - max_depth / min_samples_split / min_samples_leaf 등의 값을 적절히 조절
- Logistic Regression : 로지스틱 함수를 통해 학습(Linear 분류모델 버전이라공 생각) / 분류모델만 가능


이 있다
```python
# 회귀 계수 확인
print(model.coef_)
print(model.intercept_)

# Linear Regression
# 불러오기
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error, r2_score
# 선언하기
model = LinearRegression()
# 학습하기
model.fit(x_train, y_train)
# 예측하기
y_pred = model.predict(x_test)
# 평가하기
print(mean_absolute_error(y_test, y_pred))
print(r2_score(y_test, y_pred))
# -----------------------------------------
# 정규화 함수
from sklearn.preprocessing import MinMaxScaler
scaler = MinMaxScaler()
scaler.fit(x_train)
x_train = scaler.transform(x_train)
x_test = scaler.transform(x_test)

# KNN
# 회귀모델 불러오기
from sklearn.neighbors import KNeighborsRegressor
from sklearn.metrics import mean_absolute_error, r2_score
# 선언하기
model = KNeighborsRegressor(n_neighbors=5)
# 학습하기
model.fit(x_train, y_train)
# 예측하기
y_pred = model.predict(x_test)
# 평가하기
print(mean_absolute_error(y_test, y_pred))
print(r2_score(y_test, y_pred))

# 분류모델 불러오기
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import confusion_matrix, classification_report
# 선언하기
model = KNeighborsClassifier(n_neighbors=5)
# 학습하기
model.fit(x_train, y_train)
# 예측하기
y_pred = model.predict(x_test)
# 평가하기
print(confusion_matrix(y_test, y_pred))
print(classification_report(y_test, y_pred))
# -----------------------------------------
# plot_tree로 시각화
from sklearn.tree import plot_tree
fig = plt.figure(figsize=(12, 10))
plot_tree(model,
filled=True,
feature_names=list(x), 
class_names=['setosa', 'versicolor', 'virginica'],
fontsize=10)
plt.show()

# export_graphviz로 시각화

from sklearn.tree import export_graphviz
# 이미지 파일 만들기
export_graphviz(model,
filled=True, 
feature_names=list(x), 
class_names=['setosa', 'versicolor', 'virginica'], 
rounded=True, 
precision=3, 
out_file='tree.dot')
!dot tree.dot -Tpng -otree.png -Gdpi=300
# 이미지 파일 로딩
from IPython.display import Image
Image(filename='tree.png', width=600) 

# 변수 중요도 시각화
plt.figure(figsize=(6, 8))
plt.barh(list(x), model.feature_importances_)
plt.ylabel('Features')
plt.xlabel('Importances')
plt.show()

# Decision Tree 회귀모델 불러오기
# 불러오기
from sklearn.tree import DecisionTreeRegressor
from sklearn.metrics import mean_absolute_error, r2_score
# 선언하기
model = DecisionTreeRegressor(max_depth=5)
# 학습하기
model.fit(x_train, y_train)
# 예측하기
y_pred = model.predict(x_test)
# 평가하기
print(mean_absolute_error(y_test, y_pred))
print(r2_score(y_test, y_pred))

# Decision Tree 분류모델 불러오기
# 불러오기
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import confusion_matrix, classification_report
# 선언하기
model = DecisionTreeClassifier(max_depth=5)
# 학습하기
model.fit(x_train, y_train)
# 예측하기
y_pred = model.predict(x_test)
# 평가하기
print(confusion_matrix(y_test, y_pred))
print(classification_report(y_test, y_pred))
# -----------------------------------------
# Logistic Regression
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

단 하나의 데이터 셋에서만 학습한게 정확도가 높을까?
- K-Fold Cross Validation : 모델 일반화 가능
  - cross_val_score(모델, x_train, y_train, 분할 개수)

```python
# K-Fold Cross Validation
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

Hyperparameter : 모델튜닝방법(하지만 정답은 없음)  
Random Search : 말그대로 랜덤으로 서칭...  
  - n_iter값을 통해 조합 횟수 지정
Grid Search  
  - 모든 경우의수 확인
  - tip) 넓은 범위와 큰 Step으로 설정한 후 범위를 좁혀 나가는 방식으로 시간을 단축

Random Search + Grid Search 적용 고려
  - 둘다 적당히 믹싱하여 해보기

```python
#Random Search
# 함수 불러오기
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import RandomizedSearchCV
# 파라미터 선언
param = {'n_neighbors': range(1, 500, 10), 
'metric': ['euclidean', 'manhattan']}
# 기본모델 선언
knn_model = KNeighborsClassifier()
# Random Search 선언
model = RandomizedSearchCV(knn_model,
param,
cv=3, 
n_iter=20)

# 학습하기
model.fit(x_train, y_train)
# 수행 정보
model.cv_results_
# 최적 파라미터
model.best_params_
# 최고 성능
model.best_score_

# -----------------------------------------

#Grid Search
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

앙상블은
- 보팅(voting) / 여러모델 활용
  - 하드 보팅: 다수 모델이 예측한 값
  - 소프트 보팅: 모든 모델이 예측한 레이블 값의 결정 확률 평균을 구한 뒤 가장 확률이 높은 값
- 배깅(bagging) / 모델 한개 활용
  - 범주형 데이터(Categorical Data)는 투표 방식
  - 연속형 데이터(Continuous Data)는 평균
  - 랜덤 포레스트(Random Forest) 
    - 랜덤하게 데이터를 샘플링 / 개별 모델이 트리를 구성할 때 분할 기준이 되는 Feature를 랜덤
- 부스팅(boosting)
  - 결측치에 가중치를 부여
- 스캐킹(stacking) / 여러모델 사용
이 있다

```python
# Random Forest - 회귀모델 구현
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

# -----------------------------------------

# Random Forest - 분류모델 구현
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

# -----------------------------------------

# XGBoost - 회귀모델 구현
# 불러오기
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

# XGBoost - 분류모델 구현
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

## 2 ) 실습 코드
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

머신러닝 또한 실습 위주로 진행하였으며 코드는 git에 업로드 하였습니다.
[실습코드](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/ML/2024.09.26)