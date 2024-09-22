---
title: "[개발 방법론] - 폭포수 모델(Waterfall Model)"
description: 
author:
date: 2024-09-10 18:17:00 +0900
categories: [코딩지식, 개발방법론]
tags: [개발 방법론, 폭포수 모델]
pin: false
math: true
mermaid: true
# image:
#   path: /assets/img/20240912_post/KT_모집요강.jpg
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: .
---

## **0. 들어가기에 앞서**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
여러 사이트들에서 앱 개발 방법 혹은 앱 개발 프로세스를 다음과 같이 설명한다  
`기획 - 설계 - 구현 - 테스트 - 배포` 이러한 단계를 보다보면 궁금증이 생긴다. 설계단 이후에 기획이 바뀌면 처음부터 해야하나? 이 절차를 반드시 지켜야하나? 등의 궁금증이다.  
이개발 방법론에대한 고찰을 시리즈를 통해 다양한 모델들을 설명하고자하며 이번글은 그중 폭포수 모델이 된다.

<br/>

## **1. 폭포수 모델이란?**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
- 전통적인 소프트웨어 방법론이라고 할 수 있습니다. `분석 > 설계 > 개발 > 테스트 > 적용 > 안정화`의 단계를 따르며 `각 단계가 마무리 되기전까지 다음단계로 나아가지 못합니다`.
- 이전 단계에서 문제가 발생할경우 이전 단계로 돌아갈 수 있는 `feedback loop를 지원`하나 `순차적 모델`로 분류됩니다.
- `유연성이 떨어져` 고객의 요청사항에 즉각 대응이 어렵습니다.
- 시제품이 없으며 `최종단계에서 결과물`을 산출됩니다.
- 해당모델은 개발자가 잘 알고 응용할 수 있는 분야에 적합한 모델입니다.
- 규모가 큰 프로젝트 혹은 복잡한 시스템에는 부적절 할 수 있습니다.
- 이를 발전시킨 모델인 `v-model`이 있습니다.

<br/>

## **2. 폭포수 모델의 7단계**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

<div style="text-align: center;">
    <div style="display: inline-block; width: 150px; padding: 2px; margin: 10px; border: 1px solid black; border-radius: 10px; text-align: center; background-color: skyblue; color: blue;">계획</div>
    <br/>
    <span style="font-size: 24px; margin: 0 10px; display: inline-block; vertical-align: middle;">⇧  ⇩</span>
    <br/>
    <div style="display: inline-block; width: 150px; padding: 2px; margin: 10px; border: 1px solid black; border-radius: 10px; text-align: center; background-color: skyblue; color: blue;">요구 분석과 명세</div>
    <br/>
    <span style="font-size: 24px; margin: 0 10px; display: inline-block; vertical-align: middle;">⇧  ⇩</span>
    <br/>
    <div style="display: inline-block; width: 150px; padding: 2px; margin: 10px; border: 1px solid black; border-radius: 10px; text-align: center; background-color: skyblue; color: blue;">설계</div>
    <br/>
    <span style="font-size: 24px; margin: 0 10px; display: inline-block; vertical-align: middle;">⇧  ⇩</span>
    <br/>
    <div style="display: inline-block; width: 150px; padding: 2px; margin: 10px; border: 1px solid black; border-radius: 10px; text-align: center; background-color: skyblue; color: blue;">구현</div>
    <br/>
    <span style="font-size: 24px; margin: 0 10px; display: inline-block; vertical-align: middle;">⇧  ⇩</span>
    <br/>
    <div style="display: inline-block; width: 150px; padding: 2px; margin: 10px; border: 1px solid black; border-radius: 10px; text-align: center; background-color: skyblue; color: blue;">테스트</div>
    <br/>
    <span style="font-size: 24px; margin: 0 10px; display: inline-block; vertical-align: middle;">⇧  ⇩</span>
    <br/>
    <div style="display: inline-block; width: 150px; padding: 2px; margin: 10px; border: 1px solid black; border-radius: 10px; text-align: center; background-color: skyblue; color: blue;">배포</div>
    <br/>
    <span style="font-size: 24px; margin: 0 10px; display: inline-block; vertical-align: middle;">⇧  ⇩</span>
    <br/>
    <div style="display: inline-block; width: 150px; padding: 2px; margin: 10px; border: 1px solid black; border-radius: 10px; text-align: center; background-color: skyblue; color: blue;">유지보수</div>
</div>


### 2.1) 계획
- 프로젝트의 성공 가능성을 평가합니다.
- 경제적, 기술적으로 실현가능한지 분석하고 사업적 타당성 등 을 판단합니다.

### 2.2) 요구 분석과 명세
- 프로젝트 전반의 기준이되며 해당 프로젝트의 향후 결과를 좌지우지하는 중요한 단계입니다.
- 사용자와 이해관계자의 요구사항을 정확히 수집하고 이를 문서화하며 이는 기능적, 비기능적요구사항과 기타 제약조건등이 포함됩니다.

### 2.3) 설계
- 요구사항을 바탕으로 시스템설계와 세부설계를 하고 명세하는 단계입니다.

### 2.4) 구현
- 설계서를 바탕으로 소프트웨어 코딩을 진행하며 프로그램이 실행될 수 있도록 합니다..

### 2.5) 테스트
- 단위 테스트가 완료된 모듈, 서브 전체 시스템순서대로 통합하고 올바르게 작동하는지, 요구사항에 충족하는지 확인합니다.
- 통합테스트, 시스템 테스트, 알파테스트, 베타테스트 등이 수행됩니다.

### 2.6) 배포
- 정상적으로 운영될 수 있도록 배포하며 사용자 교육등이 포함될 수 있습니다.

### 2.7) 유지보수
- 소프트 웨어가 운영되면서 발생하는 문제를 수정하는 등의 행위가 일어납니다.

<br/>

## **3. 폭포수 모델 요약정리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

| **장점**                        | **단점**                      |
|----------------------------------|-------------------------------|
| 단순함                          | 위험분석이 결여되어있음         |
| 구조적이고 계획적임              | 변경 사항 반영이 어려움        |
| 프로젝트의 각 단계를 명확히 정의 | 각 단계가 완료되면 되돌아가기 힘듦 |
| 프로젝트 진행 상황을 쉽게 추적 가능 | 요구사항 정의 단계에서 오류 시 전체 프로젝트에 영향 |
| 문서화가 잘 되어 있음           | 고객 요구사항이 명확하지 않을 경우 문제 발생 |
| 관리 및 감독이 용이함            | 유연성이 부족하고, 예기치 않은 변경에 대응하기 어려움 |
| 초기 비용 및 일정 산정이 가능함   | 개발 기간이 길어질 수 있음     |

<br/>

## **글을 마무리하며**

<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

이번 포스팅에서는 여러 개발방법론중에서 가장 전통적인 폭포수 모델에대해서 알아보았습니다.  
해당 모델은 가장 이해하기 쉽고 많은 개발자들이 전통적으로 채택해왔던 방법론입니다.  
하지만 시대의 흐름에따라 다양한 방법론이 나오고 좀더 유연한 개발이 가능한 방법론들이 나왔습니다.  
다음 포스팅에서는 이러한 방법론들에대해 순차적으로 설명해드리도록 하겠습니다.  
궁금한점, 잘못된점 혹은 추가하면 좋을꺼같은 내용에대해서 댓글주시면 적극 반영하도록 하겠습니다.  

이만 가보겠습니다!