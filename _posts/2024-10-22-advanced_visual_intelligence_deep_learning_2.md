---
title: "[KT AIVLE] 시각지능 딥러닝 2일차 - 심화학습"
description: 
author:
date: 2024-10-22 22:04:41 +0900
categories: [KT aivle school, 시각지능 딥러닝]
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
금일은 시각지능 딥러닝 코딩 방법을 중접적으로 학습하였습니다.

## **1. Standardization **
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

금일은 흥미로운 내용으로 전체 스케일링과 채널별 스케일링을 확인해보았습니다.
RGB값을 가진 채널 데이터가 있을때 이를 스케일링 하는 방법은 두가지가있습니다.
1. 전체 스케일링
- 가장 표준적인 스케일링 방법임
  - 늘 하던대로 모든 차원에대해서 일반화하여 표준편차를 구하고 스케일링을 진행함
$$X_{\text{scaled}} = \frac{X - \mu_{\text{global}}}{\sigma_{\text{global}}}$$
- $X$: 원본 데이터
- $\mu_{\text{global}}$: 전체 데이터의 평균
- $\sigma_{\text{global}}$: 전체 데이터의 표준편차

2. 채널별 스케일링
- 각 채널별로 표준편차를 구하고 스케일링을 진행함
  - 각 채널의 값을 각각의 평균과 표준편차로 정규화함
$$X_{\text{scaled}} = \frac{X - \mu_{\text{channel}}}{\sigma_{\text{channel}}}$$
- $X$: 원본 데이터
- $\mu_{\text{channel}}$: 각 채널별 평균
- $\sigma_{\text{channel}}$: 각 채널별 표준편차

- 장단점
|                      | **채널별 스케일링 (Channel-wise Scaling)** | **전체 스케일링 (Global Scaling)**       |
|----------------------|-------------------------------------------|------------------------------------------|
| **처리 대상**        | 각 채널을 개별적으로 스케일링              | 모든 채널을 하나의 집합으로 스케일링    |
| **통계 정보**        | 채널마다 개별 평균/표준편차 사용           | 전체 데이터의 평균/표준편차 사용         |
| **장점**             | 채널별 특성 보존, 색상 정보 유지           | 일관된 스케일 적용, 빠른 처리            |
| **단점**             | 처리 시간 증가, 일관성 부족 가능성         | 채널별 차이 상실, 색상 왜곡 가능성      |

<br>

## **4. 정리**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
금일은 전반적인 시각지능의 기본적인 원리 및 간단한 코드 구현을 진행하였습니다.

이만 가보겠습니다!

실습 코드는 아래 링크에서 확인 가능합니다.
- [**시각지능**](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/visual_intelligence)
