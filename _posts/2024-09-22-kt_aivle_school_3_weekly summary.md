---
title: "[KT AIVLE] 3주차 정리(웹크롤링)"
description: 
author:
date: 2024-09-22 23:00:00 +0900
categories: [KT aivle school, 3주차 정리]
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
이번 포스팅은 연휴로 인한 휴강으로
웹크롤링에대해 배운 내용만을 작성하도록 하겠습니다.

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
      <td colspan="3" style="border: 1px solid #ddd; padding: 10px;">추석 연휴</td>
      <td colspan="2" style="border: 1px solid #ddd; padding: 10px;">웹크롤링</td>
    </tr>
  </table>
</div>

## **1. 웹 크롤링**

### 1.1) Server & Client Architecture
- Client
  - Request : Browser를 사용하여 Server에 데이터를 요청
- Server
  - Response : Client의 Browser에서 데이터를 요청하면 요청에 따라 데이터를 Client로 전송

### 1.2) URL
- http://news.naver.com:80/main/read.nhn?mode=LSD&mid=shm&sid1=105&oid=001&aid=0009847211#da_727145
  - http:// - Protocol
  - News - Sub Domain
  - naver.com - Primary Domain
  - 80 - Port
  - /main/ - Path
  - read.nhn - Page ( File )
  - mode=LSD - Query
  - #da_727145 - Fragment

### 1.3) HTTP Request Methods
- Get
  - URL에 Query 포함
  - Query(데이터) 노출, 전송 가능 데이터 작음
- Post
  - Body에 Query 포함
  - Query(데이터) 비노출, 전송 가능 데이터 많음

### 1.4) HTTP Status Code
- Client와 Server가 데이터를 주고 받은 결과 정보
  - 2xx - Success
  - 3xx - Redirect
  - 4xx - Request Error
  - 5xx - Server Error

### 1.5) Cookie, Session, Cache
- Cookie
  - Client의 Browser에 저장하는 문자열 데이터
  - 사용예시 : 로그인 정보, 내가 봤던 상품 정보, 팝업 다시보지 않음 등
- Session
  - Client의 Browser와 Server의 연결 정보
  - 사용예시 : 자동 로그인
- Cache
  - Client, Server의 RAM(메모리)에 저장하는 데이터
  - RAM에 데이터를 저장하면 데이터 입출력이 빠름

### 1.6) Web Language & Framework
- Client (Frontend)
  - HTML
  - CSS - Bootstrap, Semantic UI, Materialize, Material Design Lite
  - Javascript - react.js, vue.js, angular, jQuery
- Server (Backend)
  - Python - Django, Flask, FastAPI
  - Java - Spring
  - Ruby - Rails
  - Scala - Play
  - Javascript - Express(node.js)

### 1.7) Scraping & Crawling
- Scraping
  - 특정 데이터를 수집하는 작업
- Crawling
  - 웹서비스의 여러 페이지를 이동하며 데이터를 수집하는 작업
  - spider, web crawler, bot 용어 사용

### 1.8) Internet
- 컴퓨터로 연결하여 TCP/IP 프로토콜을 이용하여 정보를 주고 받는 컴퓨터 네트워크
- 해저케이블을 사용하여 전세계 컴퓨터에 접속
- 무선 인터넷은 매체(media)를 주파수 사용

### 1.9) OSI 7 Layer
- Open System Interconnection Reference Model
- 국제표준화기구(OSI)에서 개발한 모델로 컴퓨터 네트워크 프로토콜 디자인과 통신을 계층으로 나누어 설명
- Layer가 낮을수록 페이로드 증가
![Desktop View](/assets/img/20240922_post/layer_01.JPG){: width="800" height="400"}
![Desktop View](/assets/img/20240922_post/layer_02.JPG){: width="800" height="400"}

### 1.10) 웹 크롤링
웹페이지 종류
- 정적인 페이지 : 웹 브라우져에 화면이 한번 뜨면 이벤트에 의한 화면의 변경이 없는 페이지
- 동적인 페이지 : 웹 브라우져에 화면이 뜨고 이벤트가 발생하면 서버에서 데이터를 가져와 화면을 변경하는 페이지

requests 이용
- 받아오는 문자열에 따라 두가지 방법으로 구분
  - json 문자열로 받아서 파싱하는 방법 : 주로 동적 페이지 크롤링 할 때 사용
  - html 문자열로 받아서 파싱하는 방법 : 주로 정적 페이지 크롤링 할 때 사용

selenium 이용
- 브라우저를 직접 열어서 데이터를 얻는 방법
- request를 막는 경우가 있기 때문(Abuse로 판단해서 막음)\

속도차이
- requests json > requests html > selenium

### 1.10) HTML
HTML 이란?
- HTML은 Hyper Text Markup Language의 약자로 웹 문서를 작성하는 마크업 언어 입니다.

HTML 구성 요소
- Document : 한페이지를 나타내는 단위
- Element : 하나의 레이아웃을 나타내는 단위 : 시작태그, 끝태그, 텍스트로 구성
- Tag : 엘리먼트의 종류를 정의 : 시작태그(속성값), 끝태그
- Attribute : 시작태그에서 태그의 특정 기능을 하는 값
  - id : 웹 페이지에서 유일한 값
  - class : 동일한 여러개의 값 사용 가능 : element를 그룹핑 할때 사용
  - attr : id와 class를 제외한 나머지 속성들s
- Text : 시작태그와 끝태그 사이에 있는 문자열
- 엘리먼트는 서로 계층적 구조를 가질수 있습니다.

HTML 구조
- DOCTYPE
  - 문서의 종류를 선언하는 태그 입니다.
- html
  - head
    - meta
      - 웹페이지에 대한 정보를 넣습니다.
    - title
      - 웹페이지의 제목 정보를 넣습니다.
  - body
    - 화면을 구성하는 엘리먼트가 옵니다.

```html
<!-- HTML 웹문서의 기본적인 구조 -->
<!DOCTYPE html>
<html lang="en">
<head>
 <meta charset="utf-8">
 <title></title>
</head>
<body>
</body>
</html>
```

HTML 태그
- head
  - h1, h2, h3...
- p(한줄의 문자열을 출력하기 위한 태그)
- span(한블럭의 문자열을 표현하기 위한 태그)
- pre(줄바꿈이나 띄어쓰기가 적용되는 태그)
- code(코드를 작성하는 태그, 들여쓰기나 두칸 이상의 공백은 적용이 안됨)

문자 이외의 HTML 태그
- div(레이아웃을 나타내는 태그)
- table(로우와 컬럼이 있는 테이블 모양을 나타낼때 사용하는 태그)
- ul, li(리스트를 나타내는 태그)
- a(링크를 나타내는 태그)
- image
- iframe
- input
  - text
  - password
  - radio
  - select, option
  - textarea
  - button

이번주는 실습을 위주로 진행하였으며 아래 링크에 업로드 하였습니다.
[실습코드](https://github.com/Lucky-SeoYounghyun/kt_aivle/tree/main/web)



