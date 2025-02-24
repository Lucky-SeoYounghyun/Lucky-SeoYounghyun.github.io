---
title: "[논문] Deepseek 논문 정리(chap 1. MoE 모델)"
description: 
author:
date: 2025-02-09 23:00:00 +0900
categories: [논문, deepseek]
tags: [논문]
pin: false
math: true
mermaid: true
image:
  # path: /assets/img/20250118_post/KT_모집요강.JPG
  # lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  # alt: ktaivel_image
---

## **0. DeepSeek 그것은 무엇인가**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

중국에서 24년도 중순부터 개발된 인공지능 모델로 25년 1월경에 발표가 이루어지며 사회적으로 큰 영향을 끼치고 있는 모델입니다.  
우선 가장 눈에띄는 차이점은 아래와 같습니다.
1. 뛰어난 성능 : 현재까지는 대부분의 항목에서 GPT-4를 능가하는 성능을 보여줍니다.
2. 빠른 응답속도 : 추론기반으로 빠른 응답속도를 보여줍니다.
3. 오픈소스 : 소스코드가 공개되어있어 개발자들이 자유롭게 모델링하며 개선할 수 있습니다.
4. 효율적인 모델구조 : MoE 아키텍처를 사용하여 대규모 파라미터를 효율적으로 관리합니다.
5. 다음 토큰만 예측하는것이 아닌 여러개의 토큰을 동시에 예측
6. MHA를 개선한 MLA를 활용하여 메모리 절약과 동시에 성능 유지
이중 사회적으로 가장 이슈가되고있는 모델 구조에대해서 이번에는 알아보고자합니다.

총 3편으로 진행할 예정이며  

chap 1. MoE 모델  
chap 2. MTP  
chap 3. FP8  

과같은 챕터로 진행할 예정입니다.  

이번에는 MoE에대해 설명하도록 하겠습니다.

<br/>

## **1. MoE 모델이 뭔데?**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

MoE 모델이란 단순히 말하면 아래와 같습니다.  
Mixture of Experts 모델로 LLM의 성능을 높이면서도 연산 비용을 절감할 수 있는 신경망 아키텍처입니다.  
기존 Transformer 모델은 모든 입력 토큰이 모든 파라미터 즉 전체 뉴런을 사용하여 연산하는 반면에 17년도의 Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer' (by google Brain)논문에서 시작된 MoE모델은 여러개의 전문가(Experts)중 일부만 활성화하여 연산을 수행합니다.  
이는 MoE모델이 하나의 거대한 신경망이 아닌 여러개의 전문가로 이루어진 모델이라는 것을 알 수 있습니다.  
이를 통해 계산 부담을 획기적으로 줄여 Gpu의존도를 상대적으로 낮출 수 있습니다.  

### 그러면 기존 모델들도 MoE 쓰면 되는거 아님?

실제로 많은 모델들에서 MoE를 사용합니다 대표적으로 GLaM, Switch Transformer 등이 있습니다.

하지만 만능인것같아 보이는 MoE 모델또한 단점이 존재합니다.
MoE의 주요 특징을 보겠습니다.
1. 여러개의 전문가 네트워크로 구성
- 예를들어 32개의 전문가가 있다고 하면 각 입력 토큰은 2~8개 정도의 전문가를 활성화하여 연산 수행
2. 라우터가 입력을 특정 전문가에게 분배
- 라우터가 입력 토큰을 분석후 알맞은 전문가에게 분배
3. 모델 전체 파라미터는 커지지만, 연산량은 그 이상으로 줄어듦
- 즉, 훈련과 추론시 연산량을 줄이면서 대규모 모델의 이점은 유지 가능함
4. 부하불균형 필요
- 특정 전문가만 계속 호출하면 모델이 효율적으로 학습되지않음

이렇게 보면 연산효율성 증가, 특정 도메인 학습 가능 등 이점이 보이지만, 치명적인 단점들이 있습니다.
1. 특정 전문가에게 과부하 집중 문제
2. 라우팅 연산 비용 발생
3. 추론시 전문가 분배 최적화 문제

이런 문제를 DeepSeek은 아래와 같은 방법들을 도입하여 개선시켰습니다.
1. 보조손실 없이 부하균형 최적화
- 기존 MoE모델들은 부하 균형을 위해 추가적으로 Auxiliary loss를 추가하여 해결했지만, DeepSeek-V3는 부하균형 알고리즘을 개선하여 성능 저하 없이 최적화를 진행하였습니다.

2. 동적 전문가 분배(Dynamic Expert Assignment) 적용
- 특정 전문가에게 과부하가 걸리는 문제를 해결하기 위해 실시간 전문가 분배 최적화.

3. FP8을 사용하여 학습 및 추론 비용 절감
- 저정밀 연산을 사용하여 메모리 사용량 및 GPU 비용 절감(이부분은 chap3에 상세 설명 하겠습니다.)

## **2. 정리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

| 모델             | FFN 구조                      | 사용 방식                            |
|------------------|-------------------------------|--------------------------------------|
| 기존 Transformer | 모든 토큰이 동일한 FFN을 사용 | 모든 입력이 같은 뉴런을 거침          |
| MoE 모델         | 여러 개의 FFN이 존재 (전문가들) | 특정 입력에 맞는 FFN(전문가)만 사용 |

<br/>

## **3. 결론**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
MoE모델은 대형 언어 모델(LLM)의 연상 효율성을 극대화 하는 모델이며, 이를 DeepSeek는 기존 MoE모델의 다양한 단점을 개선하여 학습과 추론을 최적화하였습니다.  

다음 챕터에서는 MTP에대해 설명하도록 하겠습니다.

<br/>

## **3. 출처**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

[DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning](https://arxiv.org/abs/2501.12948)  