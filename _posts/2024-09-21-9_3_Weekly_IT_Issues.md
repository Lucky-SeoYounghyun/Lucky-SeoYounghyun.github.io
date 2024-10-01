---
title: "[주간 이슈] - 9월 3주차 IT이슈 및 분석(GitLab)"
description: 
author:
date: 2024-09-21 23:33:10 +0900
categories: [주간 IT Issues, 24년 9월]
tags: [IT issues]
pin: false
math: true
mermaid: true
# image:
#   path: /assets/img/20240912_post/KT_모집요강.jpg
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: .
---

## **0. 금주의 IT이슈**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

이번주는 개발자라면 잘 아는 도구인 Git에대한 보안 이슈로 시작하도록 하겠습니다.
우리가 자주쓰고있는 git에 이번에 어떤 보안 이슈가 발생했는지 궁금하지 않나요?

그러면 이번주 IT이슈를 시작하겠습니다!

<br/>

## **1. GitLab 인증 우회 취약점 패치**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

GitLab의 인증 우회 패치가 19일 이루어졌습니다.
해당 인증 우회는 `SAML 응답의 서명 검증 문제로 인해 발생`하였습니다. 이번 인증 우회는 CVSS기준 10/10점으로 매우 심각 수준의 보안 이슈였습니다.  

### 1.1) SAML 인증과정  
우선 해당 이슈를 이해하기 위해서는 SAML의 인증과정이 어떻게 이루어지는지 알아야합니다.  
`SAML(Security Assertion Markup Language)`은 `SSO(Single Sign-On)`을 위해 사용되는 웹 기반 인증 프로토콜입니다.  
SSO를 설명하자면 간단히 말해서 한번 로그인으로 연동된 모든 서비스를 이용할 수 있게하는 `마스터 키`라고 보면 편합니다.  
SAML을 사용하면 IdP(Identity Provider)라는 인증기관이 사용자 정보를 응답으로 보내고 GitLab이 이를 받아 인증합니다. 
이를 도식화 하면 아래와 같습니다.

<div style="text-align: center; font-family: Arial, sans-serif; margin-top: 20px;">
  <!-- 사용자 -->
  <div style="border: 2px solid #007bff; border-radius: 10px; padding: 5px; margin: 0; width: 150px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #f0f8ff;">
    사용자 (User)
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- GitLab (SP) -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 5px; margin: 0; width: 150px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #e6ffed;">
    GitLab (SP)
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- Identity Provider (IdP) -->
  <div style="border: 2px solid #dc3545; border-radius: 10px; padding: 5px; margin: 0; width: 150px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #ffe6e6;">
    IdP
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- GitLab 인증 완료 -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 5px; margin: 0; width: 150px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1); background-color: #e6ffed;">
    GitLab 인증
  </div>
</div>

### 1.2) 취약점의 원인

그래서 왜 취약점이 발생하였을까요?  

SAML은 중요한 정보를 가지고 다닙니다.(사용자 정보라던가...) 이 응답이 디지털 서명이라는것으로 보호되어야만 IdP가 이를 받았을때 응답이 중간에 위조되지 않았다고 인식하고 인증을 보장합니다.  
하지만 이번 GitLab은 Ruby-SAML 라이브러리가 해당 서명의 검증을 제대로 하지 못했습니다. 그래서 공격자가 서명을 위조한 응답을 보낼 수 있게 되었습니다.  

### 1.2) 공격방식

어떻게 공격했을까요?  
`SAML 서명 래핑 공격`을 취약점으로 악용하였습니다. 공격자가 SAML Response또는 SAML Assertion의 구조를 변경하여 검증되지 않은 서명이 포함된 새로운 SAML요소를 삽입하였습니다.  
여기서 SAML은 XML 형식으로 주고받습니다. SAML은 특정 노드를 보호하나 이번 취약점에서는 서명된 데이터와 공격자가 삽입한 데이터를 구분하지 못해 공격자가 문서 바깥에서 SAML Assertion을 임의로 추가할 수 있도록 허용하였습니다.  
이렇게 서명된 SAML Assertion이 gitlab에서 검증을 통과하면, 공격자는 임의로 로그인이 가능하였습니다.  

이러한 서버래핑 공격을 도식화하면 아래와 같습니다.

<div style="text-align: center;">
  <svg width="300" height="160" xmlns="http://www.w3.org/2000/svg">
    <!-- Define the arrow marker -->
    <defs>
      <!-- Arrow for end marker -->
      <marker id="arrowhead" markerWidth="5" markerHeight="3.5" 
              refX="5" refY="1.75" orient="auto" fill="#000">
        <polygon points="0 0, 5 1.75, 0 3.5" />
      </marker>
      <!-- Arrow for start marker (reversed for upward direction) -->
      <marker id="arrowhead-reverse" markerWidth="5" markerHeight="3.5" 
              refX="5" refY="1.75" orient="auto-start-reverse" fill="#000">
        <polygon points="0 0, 5 1.75, 0 3.5" />
      </marker>
    </defs>

    <!-- Identity Provider (IDP) Box with rounded corners and shadow -->
    <rect x="2" y="40" width="80" height="40" fill="#f0f8ff" stroke="#007bff" rx="10" ry="10" style="filter: drop-shadow( 2px 2px 5px rgba(0,0,0,0.1))" />
    <text x="42" y="65" font-size="16" text-anchor="middle">IDP</text>

    <!-- SAML Response Line (IDP to SP) with arrow -->
    <line x1="82" y1="60" x2="202" y2="60" stroke="black" stroke-width="2" marker-end="url(#arrowhead)" />
    <text x="142" y="50" font-size="12" text-anchor="middle">SAML Response</text>

    <!-- Dashed line to Attacker (with bidirectional arrows) -->
    <line x1="142" y1="60" x2="142" y2="100" stroke="black" stroke-width="2" stroke-dasharray="4" 
          marker-start="url(#arrowhead-reverse)" marker-end="url(#arrowhead)" />

    <!-- Attacker Box with rounded corners and shadow -->
    <rect x="102" y="100" width="80" height="40" fill="#ffe6e6" stroke="#dc3545" rx="10" ry="10" style="filter: drop-shadow( 2px 2px 5px rgba(0,0,0,0.1))" />
    <text x="142" y="125" font-size="16" text-anchor="middle">Attacker</text>

    <!-- Service Provider (SP) Box with rounded corners and shadow -->
    <rect x="202" y="40" width="80" height="40" fill="#e6ffed" stroke="#28a745" rx="10" ry="10" style="filter: drop-shadow( 2px 2px 5px rgba(0,0,0,0.1))" />
    <text x="242" y="65" font-size="16" text-anchor="middle">SP</text>
  </svg>
</div>


### 1.3) 이공격에서는 어떤점이 중요한가?

그래서 중요한 시사점이 무엇일까요?

이 공격에서 중요한 부분은 XML문서가 서명된 부분만 유효해도 서명되지 않은 다른 데이터는 검증과정에서 탐지되지 않았다는점에 있습니다.  
이는 다음과 같은 이유때문이였습니다.  
1. XPath 선택자 문제
- XML서명 검증은 `특정 XML요소에만 서명을 적용`하는 방식으로 이루어집니다.
- 서명 검증이 특정 경로에 있는 요소만 검증하고 XML 문서의 다른 요소를 검증하지 않아서 `공격자는 서명되지않은 데이터를 쉽게 추가`할 수 있습니다
  - 예를들어 초등학생이 부모님 신분증으로 술을 구매할때 판매자는 초등학생의 외모등을 보지않고 신분증만보고 술을 판매하는겁니다.
- 이러한 구조적 문제때문에 서명된 부분이 유효하기만하면 다른 부분에 위조된 데이터를 삽입해도 인증이 되었습니다.

2. XML의 구조
- XML은 매우 유연한 구조를 가졌습니다. 이는 `동일한 데이터를 여러곳에 중복 삽입` 할 수 있다는것을 뜻합니다.
- 공격자는 SAML응답 외부에 동일한 태그 구조를 포함한 추가 데이터를 삽입할 수 있으며 본래 이 데이터는 서명되어있지않아 인증이 이루어지지 않아야하지만, XML문서에서 서명된 부분만 검증하는 방식은 이를 무시합니다.

3. 서명된 부분만 검증
- 위에서 계속 말했던것처럼 SAML 응답을 처리할때, `서명된 부분만 검증을 하고 나머지 문서의 무결성 검사를 하지않습니다`.

### 1.4) 해결방법

GitLab는 이러한 취약점을 해결하기위해 OmniAuth-SAML과 Ruby-SAML 라이브러리의 새로운 버전으로 업데이트 하였고 이를통해 SAML 응답의 무결성이 정상적으로 이루어지도록 하였습니다.
또한 사용자 권고사항으로 다음 두가지 방법을 제시하였습니다.
1. 2단계 인증(2FA) 활성화
2. SAML 2FA 우회 옵션 비 활성화

[**gitlab [CVE-2024-45409] 패치 안내**](https://advisories.gitlab.com/pkg/gem/ruby-saml/CVE-2024-45409/) 