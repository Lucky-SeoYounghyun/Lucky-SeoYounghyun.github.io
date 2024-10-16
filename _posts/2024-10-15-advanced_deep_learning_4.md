---
title: "[KT AIVLE] 딥러닝 4일차 - 심화학습"
description: 
author:
date: 2024-10-15 18:15:17 +0900
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

## **1. Functional API**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- 모델을 좀더 복잡하게 구성
- 모델을 분리해서 사용 가능
- 다중 입력, 다중 출력 가능

```python
clear_session()

il = Input(shape = (nfeature, ), )
hl = Dense(18, activation = 'relu')(il)
h2 = Dense(4, activation = 'relu')(h1)
ol = Dense(1)(hl2)

model = Model(inputs = il, outputs = ol)

model.summary()
```

- 각 입력에 맞는 특징을 도출하여 학습

```python
# 모델 구성
input_1 = Input(shape=(nfeatures1,), name='input_1')
input_2 = Input(shape=(nfeatures2,), name='input_2')
# 입력을 위한 레이어
hl1_1 = Dense(10, activation='relu')(input_1)
hl1_2 = Dense(20, activation='relu')(input_2)
# 두 히든레이어 옆으로 합치기(= pd.concat)
cbl = concatenate([hl1_1, hl1_2])
# 추가레이어
hl2 = Dense(8, activation='relu')(cbl)
output = Dense(1)(hl2)
# 모델 선언
model = Model(inputs = [input_1, input_2], outputs = output)
```

## **2. 시계열 모델링**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

시간의 흐름에 따른 패턴을 분석  
### 통계적 시계열 모델링
- y의 이전 시점 데이터들로 부터 흐름의 패턴을 추출하여 예측
  - 패턴 : Trend(추세), Seasonality(계절성) 등
  - X변수들은 사용하지 않음.
  - 모델 구조 예 : 𝑦𝑡 = 𝑤1𝑦𝑡−1 + 𝑤2𝑦𝑡−2+ 𝑤3𝑦𝑡−3+ 𝑤0
  - 패턴이 충분히 도출된 모델의 잔차는 Stationary
![Desktop View](/assets/img/20241015_post/image_1.JPG){: width="800" height="400"}


### ML 기반 시계열 모델링
- 특정 시점 데이터들(1차원)과 예측대상시점(𝑦𝑡+1) 과의 관계로 부터 패턴을 추출하여 예측
  - 모델 구조 예 : 𝑦𝑡+1 = 𝑤1𝑥1𝑡 + 𝑤2𝑥2𝑡+ 𝑤3𝑥3𝑡 + 𝑤4𝑦𝑡 + 𝑤0
  - 시간의 흐름을 x변수로 도출하는 것이 중요.
![Desktop View](/assets/img/20241015_post/image_2.JPG){: width="800" height="400"}


### DL 기반 시계열 모델링
- 시간흐름 구간(timesteps) 데이터들(2차원)과 예측대상시점(𝑦𝑡+1) 과의 관계로 부터 패턴 추출
  - 어느정도 구간(timesteps)을 하나의 단위로 정할 것인가?
  - 분석 단위를 2차원으로 만드는 전처리 필요. ➔ 데이터셋은 3차원
![Desktop View](/assets/img/20241015_post/image_3.JPG){: width="800" height="400"}

### 시계열 데이터 모델링 절차
![Desktop View](/assets/img/20241015_post/image_4.JPG){: width="800" height="400"}

### RNN으로 시계열 데이터 모델링
- 예를들어 최근 4일 기반으로 데이터를 기반으로 다음날 주가를 예측하는 모델은 아래와 같다.
![Desktop View](/assets/img/20241015_post/rnn_01.JPG){: width="800" height="400"}
- 과거의 정보를 현재 데이터에 반영하도록
![Desktop View](/assets/img/20241015_post/rnn_02.JPG){: width="800" height="400"}
- RNN을 위한 데이터 전처리
  1. 데이터 분할 1:x, y
  2. 스케일링
    - x 스케일링은 필수
    - y 값이 크다면 최적화를 위해 스케일링 필요 -> 단, 모델 평가시 원래 값으로 복원
  3. 3차원 데이터셋 만들기
  4. 데이터 분할2: train, val
- return_sequences : 출력 데이터를 다음 레이어에 전달할 크기 결정
  - True : 출력 크기 그대로 전달 ➔ timesteps * node수
  - False : 가장 마지막(최근) hidden state 값만 전달 ➔ 1 * node 수
- 마지막 RNN Layer 를 제외한 모든 RNN Layer : True
- 마지막 RNN Layer : False와 True 모두 사용 가능
  - 단, True를 사용하려면 Flatten으로 펼친 후 Dense Layer 로 연결
![Desktop View](/assets/img/20241015_post/rnn_03.JPG){: width="800" height="400"}

```python
clear_session()

model = Sequential([Input(shape = (timesteps, nfeatures)),
                    SimpleRNN(8, return_sequences = True),
                    SimpleRNN(8),
                    Dense(1)
                    ])
model.summary()
```

### LSTM으로 시계열 데이터 모델링
RNN의 장기 의존성(long-term dependencies) 문제를 해결하기 위해 나온 모델  
Cell State 업데이트
- 불필요한 과거는 잊어라(Forget Gate) 
- 현재 정보 중 중요한 것은 기억하라.(Input Gate)
- Input Gate 와 Forget Gate 을 결합해서
  - 장기 기억 메모리에 태워라.(cell state 업데이트)
Hidden State 업데이트
- [업데이트된 Cell State] 와
- [input, 이전 셀의 hidden state]으로
- 새 hidden state 값 생성해서 넘기기
![Desktop View](/assets/img/20241015_post/LSTM.JPG){: width="800" height="400"}


<br>

## **3. 실습 코드**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
딥러닝 또한 실습 위주로 진행하였으며 코드는 git에 업로드 하였습니다.  
[실습코드](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/DL)