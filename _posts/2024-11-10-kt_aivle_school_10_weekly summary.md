---
title: "[KT AIVLE] 10주차 정리(언어지능 딥러닝)"
description: 
author:
date: 2024-11-10 13:00:00 +0900
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
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">언어지능 딥러닝</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">언어지능 딥러닝</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">언어지능 딥러닝</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">언어지능 딥러닝</td>
      <td colspan="1" style="border: 1px solid #ddd; padding: 10px;">언어지능 딥러닝</td>
    </tr>
  </table>
</div>


<br>

## **1. 언어지능 딥러닝**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

금주는 다양한 언어지능 모델을 학습하였으며 주요 특성들을 위주로 정리하도록 하겠습니다.
또한 5일차에는 강사님이 변경되어 기존 학습과는 약간 다른 내용을 진행하였으며 이를 주요 내용별 요약 정리를 하도록 하겠습니다.

<br>

## **2. ANN (Artificial Neural Network)**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- **특성**:
  - 기초적인 다층 퍼셉트론(Multilayer Perceptron) 기반 구조.
  - XOR 문제 해결 등 비선형 문제 해결 가능.
- **구성 요소**:
  - **입력층**: 데이터를 받아들이는 부분.
  - **은닉층**: 비선형 변환을 적용하여 특징 추출.
  - **출력층**: 최종 결과를 반환.
- **활성 함수**:
  - Sigmoid, ReLU(Rectified Linear Unit) 등 사용.
- **문제점**:
  - 기울기 소실 문제(Gradient Vanishing).
  - 과적합(Overfitting).
- **활용 사례**:
  - 기본적인 분류 및 회귀 문제.

<br>

## **3. CNN (Convolutional Neural Network)**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- **특성**:
  - 다차원 데이터를 분석하도록 설계된 모델.
- **구성 요소**:
  - **Convolution Layer**: 특징 맵 생성.
  - **Pooling Layer**: 다운샘플링으로 데이터 크기 축소.
  - **Fully Connected Layer**: 분류나 회귀 작업.
- **특징**:
  - 이미지와 영상 데이터 처리에서 강점.
  - 필터 크기, 스트라이드, 패딩 등으로 데이터 분석 범위를 조절.
- **활용 사례**:
  - 이미지 분류, 객체 탐지(Object Detection).

<br>

## **4. RNN (Recurrent Neural Network)**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- **특성**:
  - 순차적 데이터(Time Series Data) 처리.
- **구조**:
  - 이전 상태를 기억하여 새로운 입력 데이터와 함께 처리.
  - **기능적 한계**:
    - 장기 종속성(Long-term Dependency) 문제.
- **개선 모델**:
  - LSTM(Long Short-Term Memory): 장기 종속성 문제 해결.
  - GRU(Gated Recurrent Unit): 간소화된 LSTM.
- **활용 사례**:
  - 언어 모델링, 음성 인식.

<br>

## **5. GAN (Generative Adversarial Network)**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- **특성**:
  - 두 네트워크(생성자와 판별자)가 경쟁하며 학습.
- **구성 요소**:
  - **생성자(Generator)**: 가짜 데이터를 생성.
  - **판별자(Discriminator)**: 입력 데이터가 진짜인지 판별.
- **문제점**:
  - 모드 붕괴(Mode Collapse).
- **활용 사례**:
  - 이미지 생성, 스타일 전환.

<br>

## **6. Word2Vec**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- **특성**:
  - 텍스트 데이터를 벡터로 변환.
- **방식**:
  - Skip-gram: 주변 단어 예측.
  - CBOW: 중심 단어 예측.
- **활용 사례**:
  - 텍스트 유사도 측정.
  - 자연어 처리(NLP).

<br>

## **7. PCA (Principal Component Analysis)**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- **특성**:
  - 데이터의 분산을 최대화하는 주성분으로 차원을 축소.
- **문제점**:
  - 선형 관계에 제한됨.
- **활용 사례**:
  - 데이터 시각화, 얼굴 인식.

<br>

## **8. LDA (Linear Discriminant Analysis)**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- **특성**:
  - 클래스 간 분산 최대화, 클래스 내 분산 최소화.
- **활용 사례**:
  - 텍스트 및 이미지 분류.

<br>

## **9. Clustering (군집화 모델들)**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- **k-Means**:
  - 데이터를 k개의 클러스터로 분할.
  - 초기 중심점 설정에 민감.
- **DBSCAN**:
  - 밀도 기반 클러스터링.
  - 이상치(Outlier)를 효과적으로 처리.
- **Spectral Clustering**:
  - 그래프 기반으로 클러스터링.

<br>

## **10. Autoencoder**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- **특성**:
  - 입력 데이터를 압축한 뒤 복원하는 비지도 학습 모델.
- **구성 요소**:
  - **Encoder**: 데이터 압축.
  - **Decoder**: 데이터 복원.
- **활용 사례**:
  - 노이즈 제거, 특징 학습.

<br>

## **11. Softmax Classification**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

- **특성**:
  - 다중 클래스 분류 문제 해결.
- **출력**:
  - 각 클래스에 대한 확률 값 출력.
- **활용 사례**:
  - 이미지 분류, 텍스트 분류.

<br>

### 이하 내용은 5일차 내용입니다.

## **12. 자연어 처리의 발전 단계**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

1. **전통적 자연어 처리 (~2012년)**  
   - 알고리즘 기반 텍스트 처리.  
   - TF-IDF, 단어 빈도 기반 분석.  
   - Co-occurrence Matrix 활용.  

2. **단어 임베딩 학습 (~2014년)**  
   - Word2Vec, 문장/단어 분류 등.  
   - 단어 간 유사도를 벡터 공간에서 표현.  

3. **인공지능 번역 및 문장 생성 (~2017년)**  
   - Seq2Seq 모델과 Transformer 도입.  
   - 기계 번역, 챗봇, 텍스트 요약에 활용.  

4. **사전 학습 언어 모델 (PLM, ~2019년)**  
   - BERT, GPT, BART 도입.  
   - 문맥 이해 및 분류 성능 향상.  

5. **초거대 언어 모델 (LLM, 2020년~)**  
   - GPT-3, ChatGPT와 같은 대규모 모델.  
   - 생성 기반 언어 모델로 확장.

<br>

## **13. 주요 기술 개념 및 모델**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

1. **Transformer**  
   - RNN의 한계를 극복하며 병렬 처리 가능.  
   - Attention 메커니즘으로 문맥 이해 강화.  

2. **Seq2Seq + Attention**  
   - 긴 문장을 처리하는 Encoder-Decoder 구조.  
   - Attention을 통해 문장 길이와 관계없이 성능 유지.  

3. **Self-Supervised Learning**  
   - 데이터의 일부를 가리고 복원하는 방식으로 학습.  
   - 예: Masked Language Model, Next Sentence Prediction.  

4. **Fine-tuning**  
   - 사전 학습된 모델의 파라미터를 미세 조정해 특정 태스크에 적용.  

5. **LoRA (Low-Rank Adaptation)**  
   - LLM을 미세 조정할 때 파라미터 수를 줄이는 기법.  

<br>

## **14. 주요 모델 사례**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

1. **BERT**  
   - Bidirectional Encoder Representations from Transformers.  
   - 주변 단어를 보고 중심 단어 예측.  

2. **GPT 시리즈**  
   - GPT-1, GPT-2: 단순 확장.  
   - GPT-3: In-Context Learning 도입.  

3. **Hugging Face 플랫폼**  
   - Transformer, Gradio, Dataset 제공.  
   - 학습된 모델 및 데이터셋 공유.  

<br>

## **15. 응용 사례**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

1. **언어 생성 태스크**  
   - 기계 번역, 텍스트 요약, 챗봇.  

2. **정보 검색 (RAG)**  
   - 문서를 벡터화해 의미 단위로 검색.  
   - 유사도 계산 (Dot-product, Cosine similarity).  

3. **Transfer Learning**  
   - 큰 데이터셋으로 학습 후 적은 데이터로 새로운 태스크 수행.  

<br>

## **16. 최신 연구와 응용 플랫폼**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

1. **Open LLM Leaderboard**  
   - 다양한 LLM의 성능 비교 및 평가.  

2. **LangChain**  
   - 대규모 언어 모델을 활용한 애플리케이션 개발 라이브러리.  
   - 구성 요소: Prompt, Memory, Chain, Agent 등.  

---

## **17. 결론**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

이 문서는 자연어 처리 및 딥러닝의 주요 기술 발전, 모델 구조, 그리고 응용 사례를 포괄적으로 다룹니다. 특히 PLM과 LLM의 발전 과정을 통해 최신 연구와 실무 응용의 연결점을 제공합니다.


## **18. 느낀점**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

언어지능 모델은 최근 생성형 모델이 많이 활성화되었고 시장이 열려있다는 느낌을 받았으며,  
이를 활용할 수 있는 방법이 무궁무진하다는 사실을 알 수 있었으며,  
이를 활용한 어플리 케이션 제작 방법을 알 수 있었던 유익한 시간이였습니다.  

<br>

## **19. 실습 코드**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

언어지능 딥러닝 실습 코드는 아래 링크에서 확인 가능합니다.    
[언어지능 딥러닝](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/linguistic_intelligence)