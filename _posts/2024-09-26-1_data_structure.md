---
title: "[Computer Science] Chapter 01. 자료구조 ~ Chapter 04. 스택"
description: 
author:
date: 2024-09-26 20:00:00 +0900
categories: [코딩지식, CS]
tags: [자료구조, 알고리즘, 순환, 배열, 구조, 포인터, 스택]
pin: false
math: true
mermaid: true
image:
  path: /assets/img/20240926_post/data_structure.jpg
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: data_structure.jpg
---




## **0. 들어가기전에**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
본 포스트는 예전에 공부하였던 자료구조를 복습하는 의미에서 진행하는 공부이며 자세한 설명은 없이 중요한 키워드 중심으로 정리됩니다.  
[C언어로 쉽게 풀어쓴 자료구조_천인국,공용해,하상호_생능출판사](https://www.booksr.co.kr/product/9788970509716/)를 바탕으로 합니다.

## **1. 자료구조와 알고리즘**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### 알고리즘의 성능 분석
- 시간 복잡도 함수 : O(n)
  - 두 개의 함수 f(n)과 g(n)이 주어졌을 때 모든 n > n<sub>0</sub>에 대하여 \|f(n)\| ≤ c\|g(n)\|을 만족하는 2개의 상수 c와 n<sub>0</sub>가 존재하면 f(n) = O(g(n))이다.
 
- 최선, 평균, 최악?
  - 평균이 좋아보이나 이를 조사하기 위해서는 막대한 자료가 필요하므로, 보통 최악의 경우의 수행시간이 알고리즘의 시간 복잡도 척도로 많이 쓰인다.

<br>

## **2. 순환**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
- 순환의 기본 개념
  - 순환은 문제를 해결할 때 자기 자신을 호출하여 해결하는 함수 호출 방식.
- 일반적인 순환 구조는 다음과 같은 형태로 이루어진다
  - 기저 사례(Base Case): 재귀 호출이 더 이상 필요 없는 최소 단위.
  - 순환 호출(Recursive Call): 더 작은 하위 문제로 문제를 나누고, 이를 해결하기 위해 함수가 자기 자신을 호출함.
- 기저 사례가 존재하지 않거나 잘못 정의된 경우 무한 순환이 발생할 수 있으므로, 모든 순환 함수는 반드시 종료 조건(기저 사례)을 가져야 합니다.
- 장점
  - 복잡한 문제를 단순하게 표현할 수 있음.
  - 문제를 더 작은 하위 문제로 나누는 방식이 논리적으로 명확함.
  - 자연스럽게 트리 구조, 그래프 탐색, 백트래킹 문제를 해결할 때 유리함.
- 단점
  - 모든 순환 호출마다 메모리에 함수 호출 스택이 쌓이므로, 메모리 오버헤드가 발생할 수 있음.
  - 기저 사례가 잘못 설정되면 무한 순환으로 인해 프로그램이 멈추거나 오류가 발생할 수 있음.
  - 순환 호출은 반복문보다 속도가 느릴 수 있음
- 많은 순환 함수는 반복 구조로 변환할 수 있다.
  - 팩토리얼이나 피보나치 수열은 반복문을 사용하여 더 효율적으로 계산할 수 있음.
  - 반복 구조는 일반적으로 메모리 오버헤드가 적고 속도가 빠르지만, 순환이 논리적으로 더 이해하기 쉬운 경우에는 순환을 선호할 수 있음

<br>

## **3. 배열, 구조체, 포인터**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

배열
- 동일한 데이터 타입의 요소를 연속적인 메모리 공간에 저장하는 자료구조
  - 정적배열 : 배열 크기 고정
  - 동적배열 : 동적으로 할당되며 실행 중 메모리 크기를 결정하고 경우에따라 확장 가능

구조체
- 장점
  - 서로 관련 있는 데이터 타입을 하나로 묶어 관리 가능.
  - 객체 지향 프로그래밍에서 클래스와 유사한 개념으로 사용.
- 단점
  - 메모리 할당 시 구조체의 내부 필드 간에 **패딩(Padding)**이 발생할 수 있어 메모리 낭비가 발생할 수 있음.
  - 중첩된 구조체나 배열의 경우 관리가 복잡할 수 있음.

포인터
- 포인터는 다른 변수의 주소를 가리키며, 메모리 주소를 기반으로 데이터에 접근
- 특징
 - `*` 연산자를 사용하여 포인터 변수를 선언합니다.
 - `&` 연산자를 사용하여 변수의 주소를 가져옵니다.
 - `*` 연산자를 사용하여 포인터가 가리키는 주소의 값을 참조할 수 있습니다.
```c
int a = 100
int *p;
p = & a
// *p와 a가 같은 메모리를 참조하고 있다
```
- 장점
  - 포인터를 사용하면 메모리를 직접 제어할 수 있어 효율적인 메모리 관리가 가능.
  - 배열이나 구조체와 결합하여 동적 메모리 할당, 함수 호출 시 주소 전달 등이 가능.
- 단점
  - 포인터의 잘못된 사용(예: 잘못된 주소 접근, 메모리 누수)은 프로그램 오류나 충돌을 유발할 수 있음.
  - 포인터 연산은 상대적으로 복잡하고, 관리하기 어려움
<br>

## **4. 스택**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
- 특징
  - 후입선출(LIFO, Last-In-First-Out)
- 주요 연산
  - 삽입(Push)
  - 삭제(Drop)
  - 탑(Peek, Top)
  - isEmpty
  - isFull
- 중위, 전위, 후위 표기  

| 수식 (중위 표기)         | 전위 표기 (Prefix) | 후위 표기 (Postfix)  |
|------------------------|-------------------|---------------------|
| A + B * C              | + A * B C         | A B C * +           |
| (A + B) * C            | * + A B C         | A B + C *           |
| A + (B * C)            | + A * B C         | A B C * +           |
| (A + B) * (C - D)      | * + A B - C D     | A B + C D - *       |

<br>

## **글을 마무리하며**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />