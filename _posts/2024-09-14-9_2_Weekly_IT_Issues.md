---
title: "[주간 이슈] - 9월 2주차 IT이슈 및 분석(CrowdStrike)"
description: 
author:
date: 2024-09-14 18:33:10 +0900
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

## **0. IT이슈를 알아야 하는 이유**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 

코딩을 하면서 중요한것은 어떤것들이 있을까요? 기술? 능력? 기타 등등 다양한 것들이 중요할것입니다!  
하지만 코딩을 이해하기 위해서는 IT관련 이슈를 이해할 필요가 있습니다!  
예를들어 과거 클라우드 컴퓨팅의 확산으로 인해서 이후 DevOps와 CI/CD 방법론이 활성화 되었습니다. 그리고 18년 Meltdown, Spectre등의 보안 취약점이 발견됨에따라 이를 CPU보안 취약점을 해결하기위해 KPTI 기술이 도입되는등의 기술 발전이 있었습니다.  
이렇게 IT이슈를 안다는것은 향후 기술의 방향성을 미리 알 수 있는것입니다!  

그러면 이번주 IT 이슈를 시작하겠습니다!

<br/>

## **1. CrowdStrike 법적책임 이슈**
아니 7월 이슈를 왜 지금 가져오느냐? 라는 분이 계실 수 도 있습니다!  
하지만 이 이슈를 지금 가져온 이유는 현재 CrowdStrike가 관련 문제로 인해서 법적 책임을 회피하지못하고 델타항공을 비롯한 다양한 기업들과의 거대한 소송전에 휘말리고 있어 이슈가 되고있어서 가져왔습니다.  
또한 8월 30일 미국 의회로부터 청문회 출석을 요구받았으며 이는 IT 시스템에 발생한 대규모 장애와 그 영향에관한 대책 및 사과와 재발방지를 요구하기 위한것으로 보입니다.  
하지만 우리가 알고자 하는 사실은 CrowdStrike가 어떤 IT문제를 일으켰으며 왜 발생했는지가 궁금한것이므로 이를 설명하도록 하겠습니다.  

### 1.1 ) 문제 발생
한국시각으로 2024년 7월 19일 13시 쯤에 CrowdStrike는 센서 소프트웨어 업데이트를 배포하였습니다만, 사소한 오류를 품고있었으며 배포하기 직전까지 발견하지 못한상태에서 배포가 되었습니다.(심지어 자동 업데이트...)  
그래서 해당 업데이트를 진행한 PC는 시스템 충돌로 인해서 블루 스크린을 띄우며 고장나게 됩니다.  

### 1.2 ) 문제 확산
하지만 여기서 문제가 한개 더 있습니다.  
해당 프로그램은 매우 많은 기업에서 채택하여 사용하고 있던 프로그램이라는 것입니다.  
그래서 전세계 컴퓨터에 동시다발적으로 문제를 일으키게 되었습니다.  
특히 이번에 크게 문제가 되었던곳이 공항 시스템과 금융 시스템으로 전산망 마비로 공항 시스템과 전산망이 마비가되어 막대한 경제적 손실을 입었습니다.

### 1.3 ) 아니...왜?
이 프로그램이 보안 프로그램이라는데에 있습니다.  
이는 Windows에서 높은 권한과 컴퓨터 모니터링을 통해 시스템 보안을 강화하기 위해서 일부 파일들을 부팅과 동시에 시작되는 Boot-Sart 드라이버로 설정되어있어 문제가 발생시 시작부터 오류가 발생합니다.  
이러한 시작 드라이버로 설정되어있는 파일중 일부인 `Channel File 291(C-00000291-XXXX.sys)`가 말썽을 일으키면서 부팅시 블루스크린이뜨며 무한 부팅 버그가 발생하였습니다.

- **문제를 일으킨 순서**
  - 업데이트
  - `IPC 템플릿 유형 정의 불일치` Channel File 291(C-00000291-XXXX.sys)의 `IPC 템플릿 정의에는 21개의 입력 템플릿을 요구`하였습니다만...
    > IPC 템플릿이란 프로세스간 통신을 모니터링하고 탐지하기 위해 설계된 탐지 규칙과 입력 데이터 구조를 기술한 템플릿이다.
    {: .prompt-info }
  - 어라라...? `Content Interpreter(내용 해석기)는 20개의 입력만을 처리`하도록 설정되어있음
  - 입력 필드 불일치로인해 21번째 입력 필드를 찾으려고할때 메모리 배열의 범위를 벗어난 잘못된 메모리 주소를 참고하여 `메모리 접근 오류(Out of Bounds Read)` 발생
  - 컴퓨터 다운 즉 블루스크린이 발생
  - 그 과정에서 비정상적인 시스템 종료가 발생하면서 CcZeroData 함수가 비정상적인 파일의 섹터를 0으로 초기화하면서 초창기에는 Nullpointer참조 오류로 인한 버그라고 잘못 알려지기도 하였습니다.

- **중간에 막을 수 는 없었는가?**
  - Content Validator(CrowdStrike의 내부 검증 도구)가 배포전에 템플릿 인스턴스를 검증해야 하지만, `검증도구의 잘못된 논리`로 인해 21개의 필드를 요구하는 템플릿 인스턴스를 허용
  - `초기 배포시에는 모든 값과 일치하게 만드는 패턴인 wildcard(*)라는 정규식`이 21번째 필드에서 사용되어 어떤 값이 입력되어도 정상 작동 하였으나, 배포시에는 `특정 값을 요구하는 정규표현식으로 변경`되어 Content Interpreter(내용 해석기)가 새로운 값을 처리할때 메모리 접근 오류 발생
  - 새로운 템플릿 인스턴스를 배포할 때, 단계적으로 천천히 배포하거나, 소프트웨어 배포 방법중 하나인 카나리아 릴리스와 같은 검증 과정이 부족하였습니다. 이번 사건으로 배포 방법의 변경과, 초기 문제 발생시 신속한 해결을 위한 신속한 롤백 기능 제공에대한 필요성이 대두되었습니다.
  - `Content Interpreter(내용 해석기) 자체의 경계성 검사 기능의 부족`으로 인해서 입력 필드의 개수 불일치가 발생했을때 이를 감지하지못하고 메모리 접근을 시도하여 시스템 충돌 및 BSOD 문제를 발생시켰습니다.

### 1.4 ) 해결조치

- 개인
  - 안전모드 -> C:\Windows\System32\drivers\CrowdStrike -> C-00000291*.sys 삭제 -> 재부팅

- CrowdStrike
  - 78분만에 롤백 파일을 배포하였습니다.

### 1.4 ) 기업의 추후 조치
- Content Configuration System 테스트 절차 개선
  - 템플릿 유형 개발시 검증 절차 강화
  - 모든 기존 템플릿 유형에 대해 자동화된 테스트를 적용하여 입력 필드 수 와 데이터 구조 검증절차 강화
  - 향후 템플릿 인스턴스가 내용 해석기와 호환되지않는 구조를 갖고 배포되는것을 방지

- 추가적인 배포 레이어 및 승인 검증 절차 추가
  - 단계적 배포 및 승인 검증을 추가
  - 새로운 배포 링 프로세스를 도입하여 각 배포 단계에서 검증이 완료 되었을때만 다음 단계 진행

- 고객의 Rapid Response Content 업데이트 배포 제어 권한 제공
  - 업데이트의 배포 시점, 범위를 제어할 수 있는 기능을 클라우드 환경에 추가
  - 원하는 시점에 업데이트를 진행해 예상치 못한 업데이트 방지

- Channel File 291 문제 방지
  - 입력 필드수 검증, 템플릿 인스턴스가 내용 해석기와 올바르게 일치하는지 확인하는 검증 로직 추가
  - Content Validator(CrowdStrike의 내부 검증 도구)가 입력 필드의 개수와 구성을 감지하고 문제가 있는 파일이 생성되지 않도록 검증 프로세스 강화

- Content Validator(CrowdStrike의 내부 검증 도구)에 추가 검증 항목 추가
  - Content Validator에 새로운 검증 항목을 추가하여, 입력 필드가 정의된 개수와 일치하는지, 잘못된 데이터 구조가 포함되지 않았는지 확인하도록 강화

- Content Interpreter(내용 해석기)에 경계 검사 기능 추가
  - Content Interpreter(내용 해석기)에 경계성 검사 기능을 추가하여 입력 필드 수가 일치하지않을 때 메모리 접근 차단

- 제3자 보안 업체와의 협력
  - 두개의 보안 업체와 협력하여 Falcon 센서 코드와 품질 관리, 배포 절차 전반을 검토하고, 전체적인 보안성과 안정성을 보장하기 위한 프로세스 개선

### 1.5 ) 요약
Channel File 291(C-00000291-XXXX.sys)가 총 21개의 입력 필드를 가지고 있었으나 내용해석기는 20개의 입력만을 처리하도록 설계되어있어 오류가 발생하였습니다.

## **출처**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
[Remediation and Guidance Hub:Channel File 291 Incident](https://www.crowdstrike.com/falcon-content-update-remediation-and-guidance-hub/)  

[Preliminary Post Incident Report](https://www.crowdstrike.com/blog/falcon-content-update-preliminary-post-incident-report/)