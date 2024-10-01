---
title: "[주간 이슈] - 9월 4주차 IT이슈 및 분석(Linux -CUPS(RCE취약점))"
description: 
author:
date: 2024-09-28 22:33:10 +0900
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

이번주 IT이슈는 리눅스 관련 소식을 전해드리도록 하겠습니다.
해당 이슈는 `10년전부터 존재하던 코드`에대해 이번에 새로 발견된 보안 이슈입니다.
이 이슈는 `CVE-2024-47176, CVE-2024-47076, CVE-2024-47175, CVE-2024-47177`다음과 같은 세부 이슈를 포함하고 있습니다.
흥미로운 사실은 본 이슈가 사실 9월 30일에 발표 예정이였으나...CUPS의 주요 개발자이자 창시자인 Michael R Sweet가 git에 버그 수정 내역을 업로드 하면서 먼저 취약점이 들어나 부랴부랴 26일에 발표되었습니다.

<br/>

## **1. CUPS(RCE취약점)**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" /> 
CVE-2024-47076, CVE-2024-47175, CVE-2024-47176, CVE-2024-47177 이 체인 형태로 연결되어 발생한 문제로 공격자가 인증되지 않은 상태에서 임의의 코드를 원격으로 실행 할 수 있는 보안 이슈입니다.
각 취약점들을 설명리도록 하겠습니다.

### 1.1 ) CVE-2024-47176
- `cups-browsed` 서비스가 UDP 631포트를 통해 수신한 모든 패킷을 신뢰한다.
> cups-browsed는 CUPS의 서비스로 로컬 네트워크에서 브라우징을 통하여 프린터를 자동으로 검색하고 CUPS에 프린터를 추가하는 역할을 합니다.
{: .prompt-info }
- 취약점
  - 공격자가 조작된 IPP요청을 통해 악의적인 IPP 서버를 등록하여 해당 서버의 프린터 속성을 조작합니다.

### 1.2 ) CVE-2024-47076
- `libcupsfilters` 모듈이 IPP 서버로부터 수신한 프린터 속성 데이터를 제대로 검증하지않고 IPP서버를 통해 데이터를 반환합니다.
> libcupsfilters는 CUPS의 필터 라이브러리로 필터와 백엔드 드라이버들을 관리하고 처리하며 다양한 인쇄 테이터 포맷을 CUPS에서 사용할 수 있는 포맷으로 변환하고 이를 프린터로 보냅니다.
{: .prompt-info }
- 취약점
  - 검증되지 않은 IPP 속성 값이 다른 모듈에서 임시 파일로 작성 되거나 다른 프로세스로 전달되면서 악성 데이터가 시스템에 반영됩니다.

### 1.3 ) CVE-2024-47175 
- `libppd` 모듈이 ppdCreatePPDFromIPP2 함수에서 발생하는 입력 검증 취약점으로 IPP 속성을 PPD 버퍼에 생성할때, IPP 속성을 제대로 검증하지 않고 처리합니다.
> libppd 모듈은 CUPS 및 관련 인쇄 시스템에서 사용하는 PPD 파일을 처리하고 관리하는 라이브러리 입니다.
{: .prompt-info }
- 취약점
  - 임시 PPD 파일에 악성코드를 삽입하고 이후 파일이 실행될때 코드가 실행되도록 하여 시스템에 접근합니다.

### 1.4 ) CVE-2024-47177
- `foomatic-rip` 필터가 PPD 파일의 FoomaticRIPCommandLine 속성을 처리할때, 임의의 명령어를 실행할 수 있도록 허용합니다.
> foomatic-rip은 다양한 프린터 드라이버와 CUPS 사이에서 호환성을 제공하여 프린터를 쉽게 설정하고 사용할 수 있도록 도와주는 시스템입니다.  
FoomaticRIPCommandLine속성은 명령줄 옵셩을 정의하는데 사용되며 특정 동작을 지정할 수 있습니다.
{: .prompt-info }
- 취약점
  - 공격자는 인쇄 작업이 시작될때 Foomatic -rip 필터가 실행되도록 PPD 파일의 속성값을 조작하여, 임의의 명령어가 실행되도록 만듭니다.

### 1.5 ) 공격 흐름

<div style="text-align: center; font-family: Arial, sans-serif; margin-top: 20px;">
  <!-- 조작된 프린터 등록 -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 5px; margin: 0; width: 300px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1);">
    <strong>조작된 프린터 등록</strong>
    <hr style="border: none; border-top: 1px dashed #28a745; margin: 5px 0;">
    <div style="font-size: 14px; text-align: left;">
      - 공격자는 cups-browsed 가 실행중인 시스템에 IPP 패킷을 전송하여 악성 프린터 등록.  
      <br>
      - 악의적인 IPP 서버 URL이 시스템에 등록됨.
    </div>
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- 프린터 속성 값 조작 -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 5px; margin: 0; width: 300px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1);">
    <strong>프린터 속성 값 조작</strong>
    <hr style="border: none; border-top: 1px dashed #28a745; margin: 5px 0;">
    <div style="font-size: 14px; text-align: left;">
      - 악성 IPP 서버는 libcupsfilters를 통해 검증되지않은 속성 값을 반환.  
      <br>
      - 속성값은 PPD로 파일로 기록되고 공격자가 설정한 임의의 명령어가 포함됨.
    </div>
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- 임시 PPD 파일의 악성 데이터 기록 -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 5px; margin: 0; width: 300px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1);">
    <strong>임시 PPD 파일의 악성 데이터 기록</strong>
    <hr style="border: none; border-top: 1px dashed #28a745; margin: 5px 0;">
    <div style="font-size: 14px; text-align: left;">
      - libppd는 검증되지 않은 IPP 속성 값을 임시 PPD 파일에 기록함.  
      <br>
      - 이 임시 파일은 검증되지 않고 cups-filters 모듈의 foomatic-rip 필터를 통해 임의의 명령어를 실행.
    </div>
  </div>
  <!-- 화살표 -->
  <div style="margin: 0; font-size: 24px;">
    ▼
  </div>
  <!-- 명령어 실행 및 시스템 제어 -->
  <div style="border: 2px solid #28a745; border-radius: 10px; padding: 5px; margin: 0; width: 300px; display: inline-block; box-shadow: 2px 2px 5px rgba(0,0,0,0.1);">
    <strong>명령어 실행 및 시스템 제어</strong>
    <hr style="border: none; border-top: 1px dashed #28a745; margin: 5px 0;">
    <div style="font-size: 14px; text-align: left;">
      - 인쇄 작업이 시작되면 foomatic-rip 필터가 PPD 파일의 FoomaticRIPCommandLine 속성 값을 참조하여 악성 명령어를 실행.  
      <br>
      - 최종적으로 공격자는 피해 시스템에서 임의의 코드를 실행하여 제어권을 획득함.
    </div>
  </div>
</div>

### 1.6 ) 이공격에서는 어떤점이 중요한가?
이 취약점은 공격자가 별다른 인증 없이 사용자의 리눅스 시스템을 원격으로 제어할 수 있는 심각한 보안문제를 일으킵니다.
이는 한가지 오류만의 문제가아닌 다양한 문제들이 체인으로 이루어져서 RCE 취약점이 됩니다.
또한 다음과 같은 영향을 일으킬 수 있습니다.
1. 시스템 제어 : 임의의 명령어를 통해 공격자가 시스템의 제어하고, 악성코드설치, 데이터 탈취등의 문제를 야기합니다.
2. 좀비PC : 사용자의 PC의 PC가 공격자의 역할을 수행하여 다른 공격을 할 수 있습니다.
3. 권한 상승 : 로컬 권한 상승을 통해 공격자가 사용자 PC의 루트 권한을 획득할 수 있습니다.
4. 영향 범위 : 리눅스 뿐만아니라 다른 기반 시스템에서도 영향을 받을 수 있어 CUPS가 설치된 대부분의 시스템의 보안 취약점을 점검해야합니다.

### 1.7) 해결방법
근본적으로 해당 이슈는 CUPS의 오래된 소스코드를 바탕으로 문제를 일으킨것으로 보안 업데이트를 통해 대부분 해결 가능합니다.
또한 다음과 같은 방법도 권고될 수 있습니다.
1. cups-browsed서비스 비활성화
2. UDP 631번 포트 비활성화
3. CUPS관련 서시스 접근권한 설정시 네트워크와 격리를 통해 외부 네트워크로부터의 접근을 제한
4. libcupsfilters, libppd, cups-filters모듈의 최신 보안 패치

## **출처**
[evilsocket 블로그 ](https://www.evilsocket.net/)
[The Register​](https://www.theregister.com/2024/09/26/cups_linux_rce_disclosed/)
[CUPS](https://www.cups.org/doc/reporting-bugs.html)