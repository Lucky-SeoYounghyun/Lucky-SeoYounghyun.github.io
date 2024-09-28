---
title: "[Computer Science] 소수점의 배신"
description: 
author:
date: 2024-09-24 20:00:00 +0900
categories: [코딩지식, CS]
tags: [CS]
pin: false
math: true
mermaid: true
image:
  path: /assets/img/20240924_post/main_image.JPG
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: 0.1 + 0.2 == 0.3
---




## **0. 들어가기전에**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
여러분은 두수를 비교하기 위하여 어떻게 하시나요?  
부등호를 이용해 비교하시나요?  
그러면 한번쯤 다음과 같은 오류를 겪어보셨을겁니다.  

```python
0.1 + 0.2 == 0.3

# False
```

이는 상식적으로 이해가 되지않습니다. 이를 이해하기 위해 이번 포스팅을 시작하겠습니다.

## **1. 비트와 바이트**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
흔히 정보는 0과 1로 이루어져있다고합니다.  
이는 컴퓨터가 인식할 수 있는 것이 0과 1이기때문입니다.  

### **1.1) 비트**
- 데이터를 표현할 수 있는 가장 작은 단위입니다(0과 1)

### **1.2) 바이트**
- 8개의 비트가모이면 1개의 바이트가 됩니다. 컴퓨터 메모리가 파일을 측정할 수 있는 가장 기본적인 단위입니다.

<br/>

## **2. 정수처리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### **2.1) 양수가 컴퓨터에 저장되는 방법**
10진수를 2진수로 바꾸면 됩니다.  
예를들어 숫자 5는 다음과 같이 표현됩니다

<div class="box_container">
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">1</div>
  <div class="box">0</div>
  <div class="box">1</div>
</div>

### **2.2) 음수가 컴퓨터에 저장되는 방법**
음수를 저장하려면 2의 보수로 변환하는 추가 과정이 포함되며 과정은 아래와 같습니다.  

- **STEP 1 ) 2진수로 변환**
<div class="box_container">
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">1</div>
  <div class="box">0</div>
  <div class="box">1</div>
</div>

<br/>

- **STEP 2 ) 1의 보수(각 비트를 반전시켜줍니다.)**

<div class="box_container">
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">0</div>
  <div class="box">1</div>
  <div class="box">0</div>
</div>

<br/>

- **STEP 3 ) 2의 보수(1을 더해줌)**
<div class="box_container"> 
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">0</div>
  <div class="box">1</div>
  <div class="box">0</div>
</div>

<div class="plus">+</div>

<div class="box_container">
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">1</div>
</div>

<div class="plus">=</div>

<div class="box_container"> 
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">0</div>
  <div class="box">1</div>
  <div class="box">1</div>
</div>

### **2.3) 컴퓨터가 양수, 음수를 구별하는 방법**

가장 앞의 자리의 비트를 비교해서 양수와 음수를 구별하며 이를 `부호비트` 라고 합니다.  
그러면 129를 8비트로 표현하면 다음과 같다고 생각하실겁니다.
<div class="box_container">
  <div class="box">1</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">1</div>
</div>
  
<br/>

하지만 이는 틀렸습니다.  
가장 앞의 자리수는 `부호비트`이므로 컴퓨터는 이 숫자를 -1이라고 인식할것입니다.  
따라서 128은 8비트에 저장하지못하고 16비트에 저장해야되서 다음과 같이 저장이 됩니다.

<div class="box_container">
  <div class="box" style="background-color: #ff9ebd;">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
</div>
  
<div class="box_container">
  <div class="box">1</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
</div>

<br/>
이제 -128을 저장하면 가장 앞의 부호비트가 1이니까 다음과 같습니다.
  <div class="box_container">
    <div class="box" style="background-color: #ff9ebd;">1</div>
    <div class="box">0</div>
    <div class="box">0</div>
    <div class="box">0</div>
    <div class="box">0</div>
    <div class="box">0</div>
    <div class="box">0</div>
    <div class="box">0</div>
  </div>
  
  <div class="box_container">
    <div class="box">1</div>
    <div class="box">0</div>
    <div class="box">0</div>
    <div class="box">0</div>
    <div class="box">0</div>
    <div class="box">0</div>
    <div class="box">0</div>
    <div class="box">0</div>
  </div>

<br/>

## **3. 소수처리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

소수를 저장하기 위해서는 컴퓨터가 소수를 인식하기위해서 사회적 합의를 본 규칙을 이해해야하며 이 규칙은 IEEE에서 만들어진 표준을 사용합니다.  
이를 3.375를 저장하는 과정을 통해 보여드리겠습니다.

- **step 1 ) 부호비트(Sign bit)**
  - 양수이므로 0
<div class="box_container">
  <div class="box" style="background-color: #ff9ebd;">0</div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
</div>
<div class="box_container">
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
</div>
<div class="box_container">
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
</div>
<div class="box_container">
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
</div>

<br/>

- **step 2 ) 정규화(Exponent)**
  - 정수부분 3<small>(10)</small> = 11<small>(2)</small>
  - 소수부분 0.375<small>(10)</small> = 0.011<small>(2)</small>
  - 2진수 변경 결과 : 3.375<small>(10)</small> = 11.011<small>(2)</small>

  - IEEE 754 부동소수점 형식에서는 소수점은 항상 첫번째 1 뒤에 오도록 해야합니다.
  - 결과 : 11.011 = 1.1011 x 2<sup>1</sup>

  - IEEE는 Bias라는것을 사용하며 단정도에서는 Bias가 127이므로 실제 지수값은 127을 더한 후 2진수로 변환합니다.
  - 지수부분 결과 : 127 + 1 = 128 = 10000000<small>(2)</small>

<div class="box_container">
  <div class="box" style="background-color: #ff9ebd;">0</div>
  <div class="box">1</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
</div>
<div class="box_container">
  <div class="box">0</div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
</div>
<div class="box_container">
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
</div>
<div class="box_container">
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
  <div class="box" style="background-color: #f0f0f0;"></div>
</div>

<br/>

- **step 3 ) 가수(Mantissa)**
  - 정규화된 이진수에서 소수점 이하의 숫자만을 사용합니다.
  - 가수비트는 23비트로 저장되며 나머지는 0으로 채웁니다.
  - 결과 : 0110000000000000000000

<div class="box_container">
  <div class="box" style="background-color: #ff9ebd;">0</div>
  <div class="box">1</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
  <div class="box">0</div>
</div>
<div class="box_container">
  <div class="box">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
</div>
<div class="box_container">
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
</div>
<div class="box_container">
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
</div>

## **4. 순환소수 문제**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
여기서 소수점을 2진법으로 바꿀때 문제가 생깁니다.  
0.1을 2진법으로 바꾸면 0.1<small>(10)</small> = 0.000110011001100110011...<small>(12)</small>와 같이 0011이 계속 반복되며 이를 순환소수라고 합니다.  
이를 IEEE를 통해서 바꾸면 다음과 같이 일부 숫자가 누락됩니다.
<div class="box_container">
  <div class="box" style="background-color: #ff9ebd;">0</div>
  <div class="box">0</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">1</div>
  <div class="box">0</div>
  <div class="box">1</div>
</div>
<div class="box_container">
  <div class="box">1</div>
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
</div>
<div class="box_container">
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
</div>
<div class="box_container">
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">1</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
  <div class="box" style="background-color: #c8f7a1;">0</div>
</div>

<div class="box_container">
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">1</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">1</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">0</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">0</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">1</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">1</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">0</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">0</div>
</div>

<div class="box_container">
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">1</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">1</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">0</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">.</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">.</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">.</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">.</div>
  <div class="box" style="background-color: transparent; border: 1px solid transparent; color: #575757;">.</div>
</div>

이렇게 일부 누락된 숫자만큼의 오차가 발생하게 됩니다.
그래서 아래 코드는 True를 반환하게됩니다.

```python
0.1 + 0.2 > 0.3

# True
```

<br/>

## **3. 해결방법**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
1. 소수를 연산을 피합니다.
- 소수를 지양하면서 0.01계산이 필요하면 x100을 하여 1로 계산하는등의 노력이 필요합니다.

2. 일정수치 이하의 오차는 허용합니다.
- Epsilon와 같은 일정 수치 이하의 오차는 허용하는 방식이 있습니다.

3. 정밀도 함수를 사용합니다.
- Decimal같은 함수를 사용하여 소수를 정확하게 나타냅니다.
- 하지만 이는 어쩔 수 없는 오차를 포함합니다.

4. 분수를 통하여 계산합니다.
- 소수점말고 분수로 계산을하면 매우 효과적으로 해결할 수 있으나 사용에 제약이 많이 따릅니다.

이외에도 다양한 해결방법이 존재합니다.  
이를 고민하고 본인의 상황에 맞는 방법을 채택하여 사용하면됩니다.

<br/>

## **글을 마무리하며**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
이번에는 많은 초보 코더들이 실수할 수 있는 순환소수문제를 분석해보았습니다.  
실제로 이를 이해하고 메모리구조에대해 접근하는 시각을 가질 수 있으면 추후 다양한 문제상황을 진면할때 보다 손쉽게 이해하고 해결 할 수 있을겁니다.  
혹시 궁금한점 혹은 잘못된점이 있으면 언제라도 댓글주시면 확인하도록하겠습니다!  

이만 가보겠습니다!

<style>
  .box {
    display: inline-block;
    width: 35px;
    height: 35px;
    line-height: 30px;
    border: 2px solid #3b80d1; /* 푸른색 테두리 */
    background-color: #E1F5FE; /* 푸른색 배경 */
    text-align: center;
    margin: 2px;
    margin-top: 0px;
    font-family: monospace;
    border-radius: 8px; /* 둥근 모서리 */
    color: #3b80d1; /* 숫자 색상도 파란색 */
    font-weight: bold; /* 굵은 텍스트 */
  }

  .box_container {
    display: flex;
    justify-content: center; /* 중앙 정렬 */
    flex-wrap: wrap; /* 다음 줄로 넘어갈 수 있도록 */
  }

  .plus {
    font-weight: bold; /* +를 굵게 처리 */
    font-size: 24px; /* 크기를 키움 */
    margin: 0 10px; /* 좌우 여백 */
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>