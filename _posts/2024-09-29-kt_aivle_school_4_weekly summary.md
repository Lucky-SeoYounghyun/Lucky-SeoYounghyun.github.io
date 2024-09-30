---
title: "[KT AIVLE] 4주차 정리(웹크롤링, 미니프로젝트 1차, 머신러닝)"
description: 
author:
date: 2024-09-29 20:00:00 +0900
categories: [KT aivle school, 4주차 정리]
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
이번주는 저번주에 이은 웹크롤링에 이어 첫 미니프로젝트 이어서 머신러닝으로 보다 바쁜 한주가 되었습니다.
그러면 정리 시작하도록 하겠습니다.

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
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">웹 크롤링</td>
      <td colspan="2" style="border: 1px solid #ddd; padding: 10px;">미니프로젝트 1차</td>
      <td colspan="2" style="border: 1px solid #ddd; padding: 10px;">머신러닝</td>
    </tr>
  </table>
</div>

## **1. 웹 크롤링**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

저번주에 이어서 작성하도록 하겠습니다.

### 1.1) CSS Selector
CSS 셀렉터는 CSS 스타일을 적용시킬 HTML 엘리먼트를 찾기 위한 방법.

#### Element Selector
- 엘리먼트를 이용하여 선택할때 사용
- css selector로 div 를 사용하면 가장 위에 있는 dss1이 선택

```html
<div>dss1</div>
<p>dss2</p>
<span>dss3</span>
```

#### ID Selector
- 아이디를 이용하여 선택할때 사용
- 아이디를 셀렉할때는 #(아이디 이름) 으로 선택
- css selector로 #ds2 를 사용하면 dss2가 선택
- 여러개를 셀렉할때는 ,로 구분
- css selector로 #ds2, #ds3 를 사용하면 dss2와 dss3가 선택

```html
<p id="ds1">dss1</p>
<p id="ds2">dss2</p>
<p id="ds3">dss3</p>
```

#### Class Selector
- 클래스를 이용하여 선택할때 사용
- 클래스를 셀렉할때는 .(클래스 이름) 으로 선택
- 엘리멘트를 그룹핑하여 스타일을 적용할때 사용
- css selector로 .ds2 를 사용하면 dss2, dss3가 선택

```html
<p class="ds1">dss1</p>
<p class="ds2">dss2</p>
<p class="ds2">dss3</p>
```

#### not Selector
- 셀렉터로 엘리먼트를 하나만 제거하고 싶을때 사용
- not을 사용하여 셀렉트 할때에는 :not(선택에서 제거하고 싶은 셀렉터) 으로 선택
- 아래의 HTML에서 .ds:not(.ds2) 으로 셀렉트 하면 class가 ds2인 클래스를 제외 하고 나머지 ds1, ds3, ds4, ds5가 선택

```html
<p class="ds ds1">ds1</p>
<p class="ds ds2">ds2</p>
<p class="ds ds3">ds3</p>
<p class="ds ds4">ds4</p>
<p class="ds ds5">ds5</p>
```

#### first-child Selector
- 엘리먼트로 감싸져있는 가장 처음 엘리먼트가 설정한 셀렉터와 일치하면 선택
- .ds:first-child 로 설정하면 ds1과 ds3가 선택

```html
<body>
<p class="ds" id="ds1">ds1</p>
<p class="sc" id="ds2">ds2</p>
<div class="ds">
 <p class="ds ds1">ds3</p>
 <p class="ds ds2">ds4</p>
 <p class="ds ds3">ds5</p>
 <p class="ds ds4">ds6</p>
 <p class="ds ds5">ds7</p>
</div>
</body>
```

- div.ds 엘리먼트의 가장 처음 .ds 를 선택하고 싶으면 div.ds > .ds:first-child 로 셀렉터를 작성

#### last-child Selector
- 엘리먼트로 감싸져있는 가장 마지막 엘리먼트가 설정한 셀렉터와 일치하면 선택
- .ds:last-child 로 div.ds 가 선택되어 ds3~ds7이 선택

```html
<body>
<p class="ds" id="ds1">ds1</p>
<p class="sc" id="ds2">ds2</p>
<div class="ds">
 <p class="ds ds1">ds3</p>
 <p class="ds ds2">ds4</p>
 <p class="ds ds3">ds5</p>
 <p class="ds ds4">ds6</p>
 <p class="ds ds5">ds7</p>
</div>
</body>
```

#### nth-child Selector
- 엘리먼트로 감싸져있는 n번째 엘리먼트가 설정한 셀렉터와 일치하면 선택
- .ds:nth-child(3), .ds:nth-child(4) 로 설정하면 ds4, ds5가 선택
- nth-child 의 ()안의 숫자는 가장 첫번째가 0이 아니라 1로 시작

```html
<div class="wrap">
<span class="ds">ds2</span>
<p class="ds ds1">ds3</p>
<p class="ds ds2">ds4</p>
<p class="ds ds3">ds5</p>
<p class="ds ds4">ds6</p>
<p class="ds ds5">ds7</p>
</div>
```

#### 모든 하위 depth(공백) Selector
- 공백문자로 하위 엘리먼트를 셀렉트 했을때, 모든 하위 엘리먼트를 선택
- .contants h1 를 선택하면 inner_1, inner_2가 선택

```html
<div class="contants">
<h1>inner_1</h1>
<div class="txt">
 <h1>inner_2</h1>
</div>
</div>
```

#### 바로 아래 depth(>) Selector
- `>` 문자로 하위 엘리먼트를 셀렉트 했을때, 바로 아래 엘리먼트를 선택
- .contants > h1 를 선택하면 inner_1이 선택

```html
<div class="contants">
<h1>inner_1</h1>
<div class="txt">
 <h1>inner_2</h1>
</div>
</div>
```

금주도 실습을 위주로 진행하였으며 실습코드는 git에 업로드 하였습니다.
[실습코드](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/web)


## **2. 1차 미니 프로젝트**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

첫 미니프로젝트로 얻은 내용이 많았습니다.  
1차 미니프로젝트 내용은 따로 포스팅을 작성하였습니다.  
[1차 미니프로젝트](https://lucky-seoyounghyun.github.io/posts/aivle_first_mini_project/)

## **3. 머신러닝**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### 3.1 ) 학습에 따른 분휴
- 지도학습 : 학습 대상이 되는 데이터에 정답을 주어 규칙성, 즉 데이터의 패턴을 배우게 하는 학습 방법
- 비지도 학습 : 정답이 없는 데이터 만으로 배우게 하는 학습 방법
- 강화학습 : 선택한 결과에 대해 보상을 받아 행동을 개선하면서 배우게 하는 학습 방법

### 3.2 ) 과제에 따른 분류
- 분류문제 : 이미 적절히 분류된 데이터를 학습하여 분류 규칙을 찾고, 그 규칙을 기반으로 새롭게 주어진 데이터를 적절히 분류 하는 것을 목적으로 함(지도학습)
- 회귀문제 : 이미 결과값이 있는 데이터를 학습하여 입력 값과 결과 값의 연관성을 찾고, 그 연관성을 기반으로 새롭게 주어진 데이터에 대한 값을 예측하는 것을 목적으로 함(지도학습)
- 클러스터링 : 주어진 데이터를 학습하여 적절한 분류 규칙을 찾아 데이터를 분류 함을 목적으로함, 정답이 없으니 성능을 평가하기 어려움(비지도 학습)
> 해당 학습이 분류인지, 회귀인지 파악해야한다. 서로 모델이달라 적절한 알고리즘하고 평가방법이 중요하기 때문
{: .prompt-tip }

>분류 : 범줏값을 예측하는것(가입여부)
회귀 : 연속적인 숫자를 예측하는것(판매가격)

### 3.3 ) 용어사전
- 모델 : 데이터로부터 패턴을 찾아 수학식으로 정리해놓은것
- 모델링 : 오차가 적은 모델을 만드는 과정
- 모델의 목적 : 샘플을 가지고 전체를 추정
- 행 : 관측치
- 열 : 변수
- 독립변수 : 원인(x)
- 종속변수 : 결과(y)
- 평균 : 통계학에서 사용되는 가장 단순한 모델 중 하나
- 오차 : 관측값(=실젯값)과 모델 예측값의 차이: 이탈도(Deviance)
- 데이터 분리 : 데이터 셋을 학습용, 검증용, 평가용 데이터로 분리 함
  - Training, Validation, Testing
- 과대적합(overfitting) : 과하게 학습용 결과에만 정답이 맞춰짐(실전에서는 성능이 좋지 않음)
- 과소적합(Underfitting) : 학습 데이터보다 평가 데이터에서 성능이 월등히 좋거나 모든경우에 좋지않음(모델이 너무 단순함, 즉 적절히 훈련되지않음)

### 3.3 ) 모델링 코드 구조
1. 불러오기 : 사용할 알고리즘과 평가를 위한 함수 import
```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error
```
2. 선언하기 : 사용할 알고리즘용 함수로 모델 선언
```python
model = LinearRegression()
```
3. 학습하기 : 모델.fit(x_train, y_train) 형태로 모델 학습 시키기
```python
model.fit(x_train, y_train)
```
4. 예측하기 : 모델.predict(x_test) 형태로 예측한 결과 변수로 저장
```python
y_pred = model.predict(x_test)
```
5. 평가하기 : 실젯값과 예측값을 평가 함수에 전달해 성능 평가
```python
mean_absolute_error(y_test, y_pred)
```

- 데이터 준비과정
```python
# 라이브러리 불러오기
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
# 데이터 읽어오기
data = pd.read_csv('airquality.csv')
# x, y 분리
target = 'Ozone'
x = data.drop(target, axis=1)
y = data.loc[:, target]
# 학습용, 평가용 데이터 분리
from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.3) 
```

- 모델링 과정
```python
# 1단계: 불러오기
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error
# 2단계: 선언하기
model = LinearRegression()
# 3단계: 학습하기
model.fit(x_train, y_train)
# 4단계: 예측하기
y_pred = model.predict(x_test)
# 5단계: 평가하기
print(mean_absolute_error(y_test, y_pred))
```

### 3.4 ) 회귀모델 성능 평가
알아둘 기호 
- 𝑦 : 실제값
- $\hat{y}$ : 예측값
- $\bar{y}$ : 평균값

오차 제곱의 합
- SSE(Sum Squared Error)
  - $\text{SSE} = \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$

- MSE(Mean Squared Error)
  - $\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$

- RMSE(Root MSE)
  - $\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}$

오차 절대값의 합
- MAE
  - $\text{MAE} = \frac{1}{n} \sum_{i=1}^{n} \vert y_i - \hat{y}_i \vert$

- MAPE
  - $\text{MAPE} = \frac{1}{n} \sum_{i=1}^{n} \left\vert \frac{y_i - \hat{y}_i}{y_i} \right\vert$



오차를 바라보는 다양한 관점
![Desktop View](/assets/img/20240929_post/view.JPG){: width="800" height="400"}

결정계수 R**2(R-Squared)
- Coefficient of Determination
- MSE로 여전히 설명이 부족한 부분이 있음(성능이 확실히 와 닿지 않음)
- 모델 성능을 잘 해석하기 위해서 만든 MSE의 표준화된 버전이 결정 계수임
- 전체 오차 중에서 회귀식이 잡아낸 오차 비율(일반적으로 0 ~ 1 사이)
- 오차의 비 또는 설명력이라고도 부름
- 𝑅**2 = 1이면 𝑀𝑆𝐸 = 0이고 모델이 데이터를 완벽하게 학습한 것임

![Desktop View](/assets/img/20240929_post/r.JPG){: width="800" height="400"}

### 3.4 ) 분류모델 성능 평가

![Desktop View](/assets/img/20240929_post/model.JPG){: width="800" height="400"}
- TN(True Negative, 진음성): 음성으로 잘 예측한 것(음성을 음성이라고 예측한 것)
- FP(False Positive, 위양성): 양성으로 잘 못 예측한 것(음성을 양성이라고 예측한 것)
- FN(False Negative, 위음성): 음성으로 잘 못 예측한 것(양성을 음성이라고 예측한 것)
- TP(True Positive, 진양성): 양성으로 잘 예측한 것(양성을 양성이라고 예측한 것)

$ \text{정확도 - Accuracy} = \frac{TN + TP}{TN + FP + FN + TP} $
- 정분류율 이라고도 함
- 전체중에 맞힌거

$ \text{정밀도 - Precision} = \frac{TP}{FP + TP} $
- 정밀도가 낮으면 -예측도가 낮은거임
- 정답이라고 예측한것중 진짜 정답인 비율

$ \text{재현율 - Recall} = \frac{TP}{FN + TP} $
- 정답들중에 정답이라고 예측한 비율

$ \text{특이도 - Specificity} = \frac{TN}{TN + FP} $
- Negative 중에 Nagative라고 예측한 비율(재현율의 반대?)

$ \text{F1-score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}} $
- 정밀도와 재현율의 조화 평균

코드 : classification_report

```python
from sklearn.metrics import classification_report

print(classification_report(y_test, y_pred))
```

### 3.5 ) 실습 코드
머신러닝 또한 실습 위주로 진행하였으며 코드는 git에 업로드 하였습니다.
[실습코드](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/ML/2024.09.26)