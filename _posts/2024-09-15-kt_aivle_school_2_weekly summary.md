---
title: "[KT AIVLE] 2주차 정리(데이터 처리, 데이터 분석 및 의미찾기)"
description: 
author:
date: 2024-09-15 23:00:00 +0900
categories: [KT aivle school, 2주차 정리]
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
이번 포스팅은 개인적으로 주간 학습내용을 정리하기위해 작성하는 글입니다.
주간 일정은 다음과 같습니다.

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
      <td colspan="2" style="border: 1px solid #ddd; padding: 10px;">데이터 처리</td>
      <td colspan="3" style="border: 1px solid #ddd; padding: 10px;">데이터 분석 및 의미찾기</td>
    </tr>
  </table>
</div>

## **1. 데이터 처리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### 1.1) 데이터 프레임 변경
열 이름 변경 :
- columns : 모든 열 이름 변경
 ```python
 data.colums = ['colum_1','colum_2']
 ```
- rename : 지정 열 이름 변경
 ```python
 data.rename = [colums = {'colum_1' : 'change_name_colum1'}]
 ```

열 추가 :
- 없는열 선언하면 됨
 ```python
 data['new_colums'] = data['colum_1]*2
 ```
- 지정한 위치에 추가(잘 안씀) : insert사용하면 됨

열 삭제 :
- drop (axis = 0 / 행삭제, axis = 1 / 열 삭제, inplace = True 삭제한것 반영)
```python
data.drop('new_colums', axis = 1, inplace = True)
```

값 변경 :
- 모두 변경은 그냥 칼럼 선언하고 원하는거 넣기
- 조건에 의한 변경 (1) 
```python
data.loc[data['colum_1'] < 10, 'colum_1'] = 0
```
- 조건에 의한 변경 (2) 
```python
data['colum_1'] = np.where(data['data'] < 10, 0, 1) // 참이면 0 아니면 1
```
- 매핑(.map)
```python
data['colum_2'] = data['colum_2'].map({'Male' : 1, 'Female' : 0})
```

cut() 메소드 :
- pd.cut()는 숫자형을 범주형으로 변환함(예를들어 구매액을 고객 등급으로 지정)
```python
data['tip_grp] = pd.cut(data['tip'], 3, labels = ['c', 'd', 'e']) // tip열을 균등하게 3등분 한 후 값 변경
```

### 1.2) 데이터 프레임 결합
pd.concat :
- 방향 axis = 0(아래로 붙음), axis = 1(옆으로 붙음)
  - 방법 : join
    - 'outer' : 모든 행과 열 합치기(defort) // 이때 데이터가 없으면 NaN 생성
    - 'inner' : 같은 행과 열만 합치기

pd.merge : 지정한 칼럼 기준 병합
- 방향은 무조건 옆으로만
  - 방법 : how
    - 'inner' : 같은 데이터만 붙음
    - 'outer' : 다 붙음
    - 'left' : 왼쪽 데이터 기준으로 붙음
    - 'right' : 오른쪽 데이터 기준으로 붙음

pd.pivot : 집계된 데이터를 재구성함
- 아래 사진과 같음
![Desktop View](/assets/img/20240915_post/pivot.JPG){: width="800" height="400"}


### 1.3) 시계열 데이터 처리
단순히 날짜만을 의마하는게 아니라 행과 행의 시간의 순서가 있고 시간간격이 동일한 데이터를 의미함  
Time Series Data ⊂ Sequential Data 와같다.  
.dt :
- 날짜요소를 추출할때 사용
.shift :
- 시간의 흐름을 전 후 로 이동시킬 수 있음
![Desktop View](/assets/img/20240915_post/shift.JPG){: width="800" height="400"}
.rolling().mean() :
- 시간의 흐름에따른 평균
![Desktop View](/assets/img/20240915_post/mean.JPG){: width="800" height="400"}
.diff() :
- 특정 시점데이터, 이전 시점 데이터와의 차이를 구함
![Desktop View](/assets/img/20240915_post/diff.JPG){: width="800" height="400"}

### 1.4) 데이터 분석 방법론
Crisp - DM을 계속 보고 이해하도록 하자, 앞으로 작업에서 기반이되는 프로세스임
![Desktop View](/assets/img/20240915_post/crisp.JPG){: width="800" height="400"}

### 1.5) 시각화 라이브 러리
데이터 시각화는 다음과같이 크게 두가지로 나누어진다.
- 그래프(시각화)
  - Histogram, scatter, Bar Plot etc
- 통계량(수치화)
  - Min, Max, Sum, Mean, Std, P-value etc

Focus
- 우리가 다루는 데이터에는 비즈니스가 담겨 있습니다.
- 데이터 시각화의 목적은
  - 아름다운 그래프가 아니라, 
  - 통계적인 해석을 넘어,
  - `비즈니스의 인사이트`를 파악하는 것입니다.

한계
- 그래프와 통계량에는 `요약된 정보(원본)`가 표현 됩니다.
- 요약을 하는 `관점`에 따라 해석의 결과가 달라질 수 있습니다.
- 어떤 식으로 든 요약을 하면, `정보의 손실`이 발생 됩니다. 

시각화 패키지는 크게 두가지가 있으며 다음과 같다.
- matplotlib
- seaborn

### 1.6) 단병량 분석 - 숫자형
숫자형 변수 정리방법은 아래와 같이 두가지가 있다
- 기초 통계량(숫자로 요약하기 : 정보의 대푯값)
  - 평균(mean) : 산술, 기하, 조화 평균
  - 중위수(median) : 자료의 순서상 가운데 위치한 값
  - 최빈값(mode) : 자료중 가장 빈번한 값
  - 사분위수 : 데이터를 오름차순으로 정렬한 후, 전체를 4등분하고, 각 경계에 해당되는 값( 25%, 50%, 75%) 을 의미
- 도수 분포표(구간을 나누고 빈도수(frequency) 계산)
  - Histogram : bins에따라 모양이 변할 수 있다.
  - Density Plot (KDE Plot) : 밀도함수 그래프이며 면적은 1이다.
  - box plot : 박스를 기준으로 왼쪽 선부터 1사분위 ~ 4사분위이다. 3사분위 - 2사분위 =IQR이라고 한다.
    - Actual Whisker Length : 1.5*IQR 범위 이내의 최소, 최대값으로 결정
    - Potential Whisker Length : 1.5*IQR 범위, 잠재적 수염의 길이 범위
![Desktop View](/assets/img/20240915_post/boxplot.JPG){: width="800" height="400"}


시각화

- 숫자로 요약
```python
df.describe()
```

- Histogram
```python
plt.hist(titanic.Fare, bins = 30
 , edgecolor = 'gray')
plt.xlabel('Fare')
plt.ylabel('Frequency')
plt.show()
```

- KDE Plot
```python
sns.kdeplot(titanic['Fare'])
plt.show()
```

- Box Plot
```python
plt.boxplot(temp['Age']) // plt.boxplot(temp['Age'] , vert = False)라고하면 수평버전 
plt.grid()
plt.show()
```

### 1.7) 단변량 분석 - 범주형
sns.countplo : 알아서 범주 별 빈도수가 계산되고 bar plot으로 그려짐
```python
sns.countplot(titanic['Pclass'])
plt.grid()
plt.show()
```
![Desktop View](/assets/img/20240915_post/fin.JPG){: width="800" height="400"}

<br/>

## **2. 데이터 분석  및 의미찾기**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

이번 강의에서는 다음 그림이 아주 중요하였습니다.
![Desktop View](/assets/img/20240915_post/graph.JPG){: width="800" height="400"}

### 2.1) 이변량 분석 1 : 숫자 -> 숫자
두가지 방법으로 분석이 가능하다.
- 산점도(그대로 점을 찍어서 그래프)
  - 산점도에서 중요한것은 직선이 보이는가?
```python
// matplotlib
plt.scatter( x축 값, y축 값 )
plt.scatter( ‘x변수’, ‘y변수’, data = df)
// seaborn
sns.scatterplot( ‘x변수’, ‘y변수’, data = df)
// 한번에 그리기
sns.pairplot(dataframe)
```

- 공분산 / 상관계수(각 점들이 얼마나 직선에 모여 있는지를 계산)
눈으로는 관계파악이 쉽지않은것을 보완하기 위하여 수치로 나타냄
  - 직선의 관계를 수치화 → 상관계수(correlation coefficient)
  - 상관계수가 유의미한 지를 검정(test) → 상관분석
  - 상관계수('r') 공식은 다음과 같음(1에 가까울수록 강한 상관관계)
![Desktop View](/assets/img/20240915_post/r_fun.JPG){: width="800" height="400"}
  - P-value : 관계를 수치화 한 값(상관계수)이 유의미한 지 판단하는 숫자 판단 기준 (유의 수준)
    - 0.05보다 작으면 상관관계가 있다고 판단
  - 주의할점은 상관계수의 한계가 존재한다는 것이다.(직선의 기울기, 비선형관계등은 고려하지 않는다. 다만 선형관계만 수치화 해줌)
![Desktop View](/assets/img/20240915_post/fun_lim_01.JPG){: width="800" height="400"}
![Desktop View](/assets/img/20240915_post/fun_lim_02.JPG){: width="800" height="400"}
```python
// Nan값이 있으면 계산 안됨
import scipy.stats as spst
spst.pearsonr(air['Temp'], air['Ozone'])
// 한꺼번에 상관계수 구하기
df.corr()
```

### 2.2) 이변량 분석 2 : 범주 -> 숫자
- 시각화
  - 평균 비교 barplot를 통한 비교
  - sns.barplot(sns.countplot()과 plt.bar()와는 다름)
    - 평균 비교 barplot
    - 신뢰구간(오차범위)
      - 평균값이 얼마나 믿을 만 한가?
      - 좁을 수록 믿을 만 하다.
      - 데이터가 많을수록, 편차가 적을 수록 신뢰구간은 좁아 짐

- 수치화(t-test, ANOVA(분산분석))
  - 범주가 2개 : 두 평균의 차이 비교
  - 범주가 3개 이상 : 전체 평균과 각 범주의 평균 비교
  - 평균을 비교하여 차이검정을 한다.
  - T-test(범주 2개)
    - t 통계량
      - 두 그룹의 평균 간 차이를 표준오차로 나눈 값.(두 평균의 차이)
      -  t 통계량의 분
      - 유의한지 검정할려면 t-test를 통해 t통계량(유의구간 : |t통계량| > 2) 과 p-value를 구할 수 있다.
    - spst.ttest_ind(B, A)를 통해 구현한다.
  - ANOVA(범주 3개 이상)
    - $F \text{ 통계량} = \frac{\text{집단 간 분산}}{\text{집단 내 분산}} = \frac{\text{전체 평균} - \text{각 집단 평균}}{\text{각 집단의 평균} - \text{개별 값}}$
      - 값이 대략 2~3 이상이면 차이가 있다고 판단
    - 문법 : f_oneway(A, B, C)
    - 주의!
      - 분산분석은 전체 평균대비 각 그룹간 차이가 있는 지만 알려줌.
      - 어느 그룹 간에 차이가 있는지는 알 수 없음.(그래서, 보통 [사후분석]을 진행)
```python
# NaN 행 제외
temp = titanic.loc[titanic['Age'].notnull()]
# 그룹별 저장
P_1 = temp.loc[temp.Pclass == 1, 'Age']
P_2 = temp.loc[temp.Pclass == 2, 'Age']
P_3 = temp.loc[temp.Pclass == 3, 'Age']
# 2) 분산분석
spst.f_oneway(P_1, P_2, P_3)
```

### 2.3) 이변량 분석 3 : 범주 -> 범주
- 교차표
  - Pandas의 교차표 함수 : crosstab
  - 교차표로 시각화와 수치화(가설검정)을 수행한다.
  - [기대빈도]와 [실제값의 교차표]와의 차이
    - 기대빈도 : 두 범주 사이에 아무런 관계가 없을 때 나올 수 있는 빈도
```python
pd.crosstab(titanic['Survived’]
, titanic['Sex'], normalize = 'columns')
```

- 시각화
  - mosaic plot : 범주별 양과 비율을 나타냄
```python
mosaic(titanic, [ 'Pclass','Survived'])
plt.axhline(1- titanic['Survived'].mean(),
color = 'r')
plt.show()
```

- 수치화
  - 카이제곱 검정
    - $x^2 = \sum \left( \frac{(\text{관측빈도} - \text{기대빈도})^2}{\text{기대빈도}} \right)$

### 2.4) 이변량 분석 4 : 숫자 -> 범주
- 시각화
  - sns.kdeplot( )
    - common_norm = False : 생존자, 사망자 각각 kde plot 그리기
    - multiple = 'fill’ : 모든 구간에 대한 100% 비율로 kde plot 그리기 

### 2.5) 기타
- 귀무가설 𝐻0(서로 관련이 없다는것을 가설로)
- 대립가설 𝐻1(서로 관련이 있다는것을 가설로)
- 판단기준(유의수준) : 0.05(5%) 혹은 좀 더 보수적인 기준으로 0.01(1%)를 사용
- 검정(차이가 있는지 없는지 확인)하기 위한 차이 값(검정 통계량)
  - t 통계량
  - 𝑥**2(카이제곱) 통계량
  - f 통계량
  
표본으로 어떻게 모평균을 추정할까?
- 표본평균은 모평균에대한 추정치로 오차가 존재하며 이를 표준오차라고 함
- 단 표본을 뽑을수록 중심에 가까워지며 이를 중심극한정리라고함
- 표본오차를 바탕으로 95% 신뢰구간을 구할 수 있음
  - 표본을 100번 정도 뽑으면 95번 정도는 95%신뢰구간 안에 모평균을 포함함