---
title: "[python] 컴프리헨션"
description: 
author:
date: 2024-09-16 14:17:00 +0900
categories: [코딩지식, python]
tags: [컴프리헨션]
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
이번 포스팅은 파이썬다운 방법인
간결하고 효율적인 방식으로 코드를 만드는 컴프리헨션에대해 글을 작성하도록 하겠습니다.

## **1. 컴프리 헨션 종류**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
컴프리헨션 종류는 기본적으로 3가지로 아래와 같습니다.
1. 리스트 컴프리헨션
2. 딕셔너리 컴프리헨션
3. 집합 컴프리헨션
이제 각 컴프리헨션을 자세히 설명해드리도록 하겠습니다.

<br/>

### 1.1 ) 리스트 컴프리 헨션 (List Comprehension)
한마디로 정리하면 엄청 자주 쓰입니다.  
리스트 컴프리 헨션은 말그대로 리스트를 간결하게 표현하는 방법이며 이는 다음과 같이 표현합니다.  

- 예시 1 ) 짝수 구하기

```python
# 기존
custom_list = []
for i in range(1, n):
  if i % 2  == 0:
    custom.append(i)

# 리스트 컴프리헨션
custom_list = [i for i in range(1,n) if i % 2 == 0]
```

- 예시 2 ) 제곱수 구하기

```python
# 기존
custom_list = []
for i in range(1, n):
  custom_list.append(i**2)
  
# 리스트 컴프리헨션
custom_list = [i**2 for i in range(1, n)]
```

- 정리

```
custom_list = [표현식 for 항목 in 반복 가능한 객체 if 조건문]
```

<br/>

### 1.2 ) 딕셔너리 컴프리 헨션 (Dictionary Comprehension)
리스트 컴프리헨션과 비슷하나 딕셔너리 생성을 위한 컴프리 헨션입니다.  
- 예시 1 ) key값이 있는 짝수 구하기

```python
# 기존
custom_dict = {}
custom = 0
for i in range(1, n+1):
  if i % 2 == 0:
    custom_dict[custom] = i
    custom += 1

# 딕셔너리 컴프리헨션
custom_dict = {index: i for index, i in enumerate(range(1, n+1), start=0) if i % 2 == 0}
```

> enumerate는 자동으로 인덱스와 요소를 동시에 추출할 수 있도록 도와줍니다.  
{: .prompt-info }

- 예시 2 ) key값이 있는 제곱수 구하기

```python
# 기존
custom_dict = {}
for i in range(1, n+1):
  custom_dict[i] = i**2

# 딕셔너리 컴프리 헨션
custom_dict = {i : i**2 for i in range(1, n+1)}
```

- 정리

```
custom_dict = {키 표현식: 값 표현식 for 항목 in 반복 가능한 객체 if 조건문}
```

<br/>

### 1.3 ) 집합 컴프리 헨션 (Set Comprehension)
마찬가지로 리스트 컴프리헨션과 유사하나 중복을 허용하지 않는 집합을 대상으로 합니다.  

- 예시 1 ) 짝수 집합 구하기

```python
# 기존
custom_set = set()
for i in range(1, n):
    if i % 2 == 0:
        even_set.add(i)

# 집합 컴프리 헨션
custom_set = {i for i in range(1,n) if i % 2 == 0}
```

- 예시 2 ) 제곱수 구하기

```python
# 기존
custom_set = set()
for x in range(1, 11):
    square_set.add(x**2)

# 집합 컴프리 헨션
custom_set = {x**2 for x in range(1, 11)}
```

- 정리

```
custom_set = {키 표현식: 값 표현식 for 항목 in 반복 가능한 객체 if 조건문}
```

<br/>

### 1.4 ) 제너레이터 컴프리 헨션 (Generator Comprehension)
리스트 컴프리 헨션과 비슷하지만 결과를 제너레이터로 반환하여 메모리를 효율적으로 사용할 수 있습니다.

차이점은 리스트 컴프리헨션은 대괄호 `'[]'`를 사용하지만 제너레이터 컴프리 헨션은 소괄호 `'()'`를 사용합니다.
이 외에는 차이점이 마땅히 없어 정리 식만 알려드리겠습니다.

- 정리

```
custom_gen = (표현식 for 항목 in 반복 가능한 객체 if 조건문)
```

<br/>

## **2. 최종 정리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- 리스트 컴프리헨션
```
custom_list = [표현식 for 항목 in 반복 가능한 객체 if 조건문]
```
- 딕셔너리 컴프리헨션
```
custom_dict = {키 표현식: 값 표현식 for 항목 in 반복 가능한 객체 if 조건문}
```
- 집합 컴프리헨션
```
custom_set = {표현식 for 항목 in 반복 가능한 객체 if 조건문}
```
- 제너레이터 컴프리헨션
```
custom_gen = (표현식 for 항목 in 반복 가능한 객체 if 조건문)
```


이외에도 기능별로 나누면 다양한 컴프리헨션이 있으나 다들 비슷비슷하게 동작합니다. 따라서 충분히 응용하여 대처 가능합니다.

<br/>

## **글을 마무리하며**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
이번에는 파이썬을 파이썬 답게? 쓸 수 있는 컴프리헨션에대해 알아보았습니다.
보단 간결한 코드를 작성할 수 있으며 가독성이 더 좋아질것입니다.

지금은 익숙하지 않을지라도 계속 하다보면 언젠가는 내것처럼 익숙해질때가 있을겁니다!
궁금한점 있으시면 언제든지 댓글주시면 확인해보도록 하겠습니다!

이만 가보도록 하겠습니다.