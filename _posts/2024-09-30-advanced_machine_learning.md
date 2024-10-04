---
title: "[KT AIVLE] 머신러닝 3일차 - 심화학습"
description: 
author:
date: 2024-09-30 20:00:00 +0900
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

## **1. 머신러닝**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
저번주에 이어서 금일도 머신러닝에대해 배웠습니다.

## 2. 기본 알고리즘
### **2.1 ) Linear Regression(회귀 모델에만 사용)**
  - 단순회귀 : x값 하나만으로 y값을 설명할 수 있는 경우
```python
# 회귀계수 확인
print(model.coef_) # 회귀계수
print(model.intercept_) # 편향
# [3.916]
# -15.80
# 𝑦 = −15.81 + 3.92 ∙ x
```
  - 다중회귀 : 여러개의 x값으로 y값을 설명
```python
# 회귀계수 확인
print(list(x_train))
print(model.coef_)
print(model.intercept_)
# ['Temp', 'Wind', 'Solar.R']
# [ 1.52 -3.56 0.06]
# -53.37
# 𝑂𝑧𝑜𝑛𝑒 = −53.37 + 1.52 ∙ 𝑇𝑒𝑚𝑝 − 3.57 ∙ 𝑊𝑖𝑛𝑑 + 0.07 ∙ 𝑆𝑜𝑙𝑎𝑟. 𝑅
```
  - 모델 구현
```python
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
```
### **2.2 ) KNN(K-Nearest Neighbor)**
  - K 최근접 이웃(주변에 누가있는지)
  - 회귀와 분류에 사용되는 매우 간단한 지도학습 알고리즘
  - 연산 속도가 느림
  - k 값에 따라 예측 값이 달라지므로 적절한 k 값을 찾는 것이 중요(기본값=5)
![Desktop View](/assets/img/20240930_post/line.JPG){: width="800" height="400"}
  - 맨하튼 거리는  >= 유클리드 거리
  - **정규화(Scaling) 과정이 반드시 필요함**
![Desktop View](/assets/img/20240930_post/scaling.JPG){: width="800" height="400"}
    - 스케일링 방법 1 (정규화 : Nomalization) : 
    $\Large X_{\text{norm}} = \frac{x - x_{\text{min}}}{x_{\text{max}} - x_{\text{min}}}$
    - 스케일링 방법 2 (표준화 : Standardization) : 
    $\Large X_z = \frac{x - x_{\text{mean}}}{x_{\text{std}}}$
  - 평가용 데이터에도 학습용 데이터를 기준으로 스케일링을 해야함
```python
# 함수 불러오기
from sklearn.preprocessing import MinMaxScaler
# 정규화
scaler = MinMaxScaler()
scaler.fit(x_train)
x_train = scaler.transform(x_train)
x_test = scaler.transform(x_test)
```
  - 회귀 모델 구현
```python
# 불러오기
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
```
  - 분류 모델 구현
```python
# 불러오기
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
```

### **2.3 ) Decision Tree(결정트리)**
- 분류와 회귀 모두에 사용
- 분석과정을 실제로 눈으로 확인가능(화이트 박스 모델)
- 스무고개처럼 질문형식
- 훈련 데이터에 대한 제약 사항이 거의 없는 유연한 모델 -> 과적합으로 모델 성능이 떨어지기 쉬움 -> 트리 깊이를 제한하는(=가지치기) 튜닝이 필요
![Desktop View](/assets/img/20240930_post/Decision_Tree.JPG){: width="800" height="400"}
![Desktop View](/assets/img/20240930_post/Decision_Tree_2.JPG){: width="800" height="400"}

- 불순도(Impurity)
  - 순도가 높을 수록 분류가 잘 된 것임
  - 불순도를 수치화 할 수 있는 지표
    - 지니 불순도(Gini Impurity)
    - 엔트로피(Entropy)

  - **지니불순도(Gini Impurity)**  
    $\Large Gini = 1 - \sum_{i=1}^{c} (p_i)^2$
    - 지니 불순도 = 1 − (양성 클래스 비율2+음성 클래스 비율2)
    - 분류후에 얼마나 잘 분류했는지를 평가하는 척도(잘분류하면 : 0, 완전 반반이면 : 0.5)
    - 지니 불순도가 낮은 속성으로 의사결정 트리 노드 결정

  - **엔트로피(Entropy)**  
    $\Large Entropy = -\sum_{i=1}^{n} p_i \log_2p_i$
    - 엔트로피 = −음성클래스비율× 𝑙𝑜𝑔2 음성클래스비율 − 양성클래스비율 × 𝑙𝑜𝑔2(양성클래스비율)
    - 𝑝𝑖 : 집합 안에서 속성 i의 확률을 나타냄
      -예를 들어 𝑝𝑖=1이면 집합 안의 모든 항목이 i 속성을 가진 경우
    - 엔트로피는 0~1 사이의 값(잘분류하면 : 0, 완전 반반이면 : 1)

- 정보이득(Information Gain)  
$\Large \text{Gain}(T, X) = \text{Entropy}(T) - \text{Entropy}(T, X)$
  - 정보 이득이 크다 = 어떤 속성으로 분할할 때 불순도가 줄어든다
  - 모든 속성에 대해 분할한 후 정보 이득 계산
  - 정보 이득이 가장 큰 속성부터 분할

- 가지치기
  - 가지치기를 하지 않으면 모델이 학습 데이터에는 매우 잘 맞지만, 평가 데이터에는 잘 맞지 않음  
  → 과대적합, 일반화되지 못함  

| Parameter          | Description                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `max_depth`        | • 트리의 최대 깊이 (기본값: None).<br>• 기본값으로 설정하면 완벽하게 분류될 때까지 분할하거나,<br>• 노드가 갖는 샘플 개수가 min_samples_split 설정값 보다 작아질 때까지 계속 분할.<br>• 계속 분할되면 트리 깊이가 너무 깊어져 과적합이 발생할 수 있으니 적절한 값 설정 필요. |
| `min_samples_split`| • 노드를 분할하기 위한 최소한의 샘플 개수 (기본값: 2).<br>• 값을 작게 설정할 수록 계속 분할되어 트리 깊이가 깊어져 과적합 발생 가능.<br>• 적절한 값을 지정해 과적합을 방지할 필요가 있음.                                     |
| `min_samples_leaf` | • 리프 노드가 되기 위한 최소한의 샘플 수 (기본값: 1).<br>• min_samples_split과 함께 과적합을 방지할 목적으로 사용.<br>• 불균형 클래스인 경우 이를 고려하여 작은 값을 설정할 필요가 있음.                                  |
| `max_features`     | • 최선의 분할을 위해 고려할 Feature 수 (기본값: None).<br>• 기본값으로 설정하면 모든 Feature를 사용해서 분할 수행.<br>• 정수형으로 선언하면 Feature 수, 실수형으로 선언하면 Feature 비율.<br>• 'sqrt'로 선언하면 전체 Feature 수의 루트 값.<br>• 'auto'로 설정하면 'sqrt'와 같은 의미.<br>• 'log'로 선언하면 log2(전체 Feature 수). |
| `max_leaf_nodes`   | • 리프 노드의 최대 개수.                                                                                                                                 |

- plt_tree로 시각화
  - 불순도가 낮을 수록 진한 배경색
```python
# 시각화 모듈 불러오기
from sklearn.tree import plot_tree
fig = plt.figure(figsize=(12, 10))
plot_tree(model,
filled=True,
feature_names=list(x), 
class_names=['setosa', 'versicolor', 'virginica'],
fontsize=10)
plt.show()
```

- export_graphviz로 시각화
  - 좀더 가독성 있는 시각화 가능
```python
# 시각화 모듈 불러오기
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
```

- 변수 중요도 시각화
  - feature_importances_속성 값으로 변수 중요도 확인
```python
# 변수 중요도 시각화
plt.figure(figsize=(6, 8))
plt.barh(list(x), model.feature_importances_)
plt.ylabel('Features')
plt.xlabel('Importances')
plt.show()
```
- 회귀모델 구현
```python
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
```

- 분류모델 구현
```python
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
```


- 용어집
  - Root Node(뿌리 마디): 전체 자료를 갖는 시작하는 마디
  - Child Node(자식 마디): 마디 하나로부터 분리된 2개 이상의 마디
  - Parent Node(부모 마디): 주어진 마디의 상위 마디
  - Terminal Node(끝 마디): 자식 마디가 없는 마디(=Leaf Node)
  - Internal Node(중간 마디): 부모 마디와 자식 마디가 모두 있는 마디
  - Branch(가지): 연결되어 있는 2개 이상의 마디 집합
  - Depth(깊이): 뿌리 마디로부터 끝 마디까지 연결된 마디 개수(오른쪽 트리의 경우 5)


### 3 ) 실습 코드
머신러닝 또한 실습 위주로 진행하였으며 코드는 git에 업로드 하였습니다.
[실습코드](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/ML/2024.09.26)