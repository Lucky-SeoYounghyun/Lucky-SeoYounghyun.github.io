---
title: "[KT AIVLE] 12주차 정리(6차 미니프로젝트, 1차 에이블 데이)"
description: 
author:
date: 2024-11-24 13:00:00 +0900
categories: [KT aivle school, 11월]
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

이번주에는 시각지능 딥러닝 학습을 진행하였습니다.


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
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">6차 미니프로젝트(2차)</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">6차 미니프로젝트(2차)</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">6차 미니프로젝트(2차)</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">6차 미니프로젝트(2차)</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">1차 에이블 데이</td>
    </tr>
  </table>
</div>


<br>

## **2. 6차 미니프로젝트(2차)**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
### **1. 음성 데이터를 활용한 텍스트 변환(STT) 및 요약**
1. **음성 데이터를 텍스트로 변환**:
   - OpenAI **Whisper-1** 모델 활용해 음성을 텍스트로 변환.
   - 다양한 음성 데이터를 추가로 수집하고 변환 작업 수행.
   - 실제 데이터를 통해 STT 성능 확인 및 처리 방법 학습.

2. **텍스트 요약 및 키워드 추출**:
   - OpenAI **GPT-3.5-turbo**를 사용한 텍스트 요약.
   - 프롬프트 설계 및 키워드 추출 방식을 익힐 수 있음.
   - 대량의 데이터를 자동화 처리하는 워크플로 설계 학습.

### **2. 데이터 준비 및 모델 파인튜닝**
1. **응급 상황 분류 데이터 준비**:
   - 실질적인 데이터를 직접 제작하며 데이터 준비 과정 학습.
   - **KTAS 응급등급(1~5)** 기준 데이터 생성 및 정제:
     - 키워드 활용, GPT로 데이터를 보완하는 방법 이해.

2. **사전학습 모델 파인튜닝(BERT)**:
   - 한국어 특화 모델 **klue/bert-base** 활용.
   - 파인튜닝 시 **하이퍼파라미터 조정**(학습률, 에폭 등)의 중요성 학습.
   - Hugging Face 라이브러리를 활용한 **모델 학습 및 평가 방법** 습득:
     - `Trainer` 활용 및 `evaluate`로 모델 성능 검증.

3. **모델 저장 및 재사용**:
   - 훈련된 모델과 토크나이저 저장 및 로딩 방법 이해.
   - 저장된 모델을 다양한 시나리오에서 활용하는 실무적 방법 학습.

### **3. 위치 데이터 활용 및 응급실 추천 시스템**
1. **위치 기반 데이터 처리**:
   - **Haversine** 공식을 활용해 직선거리 계산 방식 학습.
   - 위치 데이터를 이용한 실질적 문제 해결(응급실 추천).

2. **효율적인 거리 계산 최적화**:
   - 필터링 기법(좌표 범위 지정)을 통해 거리 계산 성능을 개선하는 방법 이해.
   - 실시간 추천 시스템의 효율성과 정확성을 높이는 방법 탐구.

3. **외부 API 활용**:
   - **Naver Maps API**를 사용해 도로거리와 소요 시간 계산.
   - API 호출의 기본 구조와 활용법(인증키 관리, 요청-응답 처리) 익히기.
   - 입력 데이터를 활용해 실제 사용 가능한 서비스로 연결하는 기술 학습.

### **4. 프로젝트 전반적인 학습**
1. **데이터 파이프라인 설계**:
   - 데이터 수집, 전처리, 분석, 모델링, 결과 저장 및 서비스화 과정을 전체적으로 경험.
   - 실무에서 필요한 데이터 흐름 설계 능력 배양.

2. **AI 모델의 응급상황 활용**:
   - AI 모델(STT, GPT, BERT)을 응급상황 대응과 같은 **현실 문제**에 적용하는 기술 이해.
   - 텍스트 처리, 분류 모델, 거리 계산을 결합한 **통합 시스템 설계** 학습.

3. **고도화 및 확장성**:
   - 단순한 직선거리 계산을 넘어 도로거리 계산으로 서비스 고도화 방법 학습.
   - 프로젝트를 단계적으로 확장하며 효율성을 개선하는 방법 이해.

<br>

## **2. 1차 에이블 데이**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

### 코딩테스트 1차
- 총 3문제로 사전에 학습하였던 코딩마스터즈 중급정도의 난이도로 출제된것같은 느낌이였습니다.
- 자바로 200점 이상 달성시 10만원을 얻을 수 있는 기회가 부여됩니다.
![Desktop View](/assets/img/20241124_post/java.JPG){: width="800" height="400"}
- 저는 이번에 200점 이상 달성하여 10만원 획득에 성공하였습니다!!!

<br>

## **18. 느낀점**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
단순히 배우는것으로 끝나는것이아니라 다양한 실전과 같은 프로젝트를 진행하면서 실제로 어떻게 현장에 적용할 수 있을지 배울 수 있는점이 좋았던것같습니다.
특히, 이번 6차 프로젝트 같은 경우에는 실제 데이터를 활용하여 프로그램을 만드는것으로 바로 현장에 적용해도 될 정도의 데이터가 학습된것같습니다.
또한, 1차 에이블 데이를 통하여 에이블 스쿨의 반이 넘어가는 시점에서 한번 돌아볼 수 있었던 시간이 될 수 있었던것 같습니다.

<br>

## **19. 실습 코드**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

미니프로젝트 6차(2) 실습 코드는 아래 링크에서 확인 가능합니다.    
[언어지능 딥러닝](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/mini_project_06_02)