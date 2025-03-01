---
title: "[Ubuntu] Ubuntu를 활용하여 개인용 Nas서버 구축하기"
description: 
author:
date: 2025-03-01 23:00:00 +0900
categories: [Nas, Linux, Ubuntu]
tags: [Nas server]
pin: false
math: true
mermaid: true
image:
  # path: /assets/img/20250118_post/KT_모집요강.JPG
  # lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  # alt: ktaivel_image
---

## **0. 서버란?**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

[요청을 받으면 데이터를 보내주는 어떠한것]이라고 생각하시면 편합니다.  

요즘에는 저장소도 많이 제공해주는데 왜 만드냐? 하면 공부 + 좀더 보안이 강화된 개인용 Nas를 만들고 싶었습니다.

그래서 오늘은 집에서 굴러다니는 노트북으로 우분투 서버를 이용하여 Nas를 만들고자 합니다.

<br/>

## **1. Ubuntu server 설치**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
Ubuntu server를 아래 링크에서 다운로드 받아 컴퓨터에 설치해줍니다.  

[Ubuntu server](https://ubuntu.com/download/server)  

고정 IP를 추천드립니다.  

설치방법은 어렵지 않으나 궁금하신부분은 댓글 혹은 인터넷을 참조하시면 가능합니다!

<br/>

## **2. ssh 포트 개방**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

2.1) 혹시 서버 설치시 ssh를 설치 하지 않으신 분들은 아래 코드로 ssh를 설치하시면 됩니다.

```bash
sudo apt update
sudo apt install openssh-server
```

2.2) ssh 동작을 확인합니다. 만약 active면 3번은 건너뛴 후 4번으로 바로 이동하시면 됩니다.

```bash
sudo systemctl status ssh
```

2.3) ssh를 동작시키기

```bash
sudo systemctl start ssh
//아래 코드는 서버 재부팅시 자동으로 ssh동작하도록 하는 코드입니다.
sudo systemctl enable ssh
```

2.4) 방화벽 확인. 방화벽이 작동중이면 바로 6번으로 넘어가시면 됩니다.
```bash
sudo ufw status
```

2.5) 방화벽 활성화 ()
```bash
sudo ufw enable
//혹시 방화벽이 없으신 분들은 아래 코드로 먼저 설치바랍니다.
sudo apt update
sudo apt install ufw
```

2.6) ssh용 포트 열기(기본은 22번입니다만...보안으로 인하여 변경하시는걸 추천 드립니다. 보안관련 글은 2편에 추가적으로 작성하도록 하겠습니다.)

```bash
sudo ufw allow 22/tcp
```

이러면 기본적인 ssh 설정은 끝이 납니다.

<br/>

## **3. 공유기 포트포워딩**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

여기서부터는 사용하시는 공유기에따라 달라집니다.
저는 LG U+를 사용하므로 해당 링크로 들어간다음 포트포워딩을 설정해주었습니다.

[http://192.168.219.1/] 링크 접속 후 네트워크 설정 -> NAT 설정에 포트 번호(지금은 22번), IP주소(Ubuntu ip주소), 서비스 포트 22번, 프로토콜 TCP/IP로 설정하였습니다.
Ubuntu ip 주소를 모르시는 분들은 아래 명령어로 확인 가능합니다.

```bash
ip a
```

<br/>

## **3. samba 설정**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

3.1) samba 설치
```bash
sudo apt install samba
```

3.2) 접근 제어를 위해 nasgroup라는 그룹만 접근 가능하도록(최소한의 보안)
```bash
sudo groupadd nasgroup
sudo usermod -aG nasgroup username
```

3.3) samba 공유 폴더 생성(nas로 생성하겠습니다.)
```bash
sudo mkdir /nas
```

3.4) 소유권 설정
```bash
sudo chown :nasgroup /nas
sudo chmod 770 /nas
```

3.1) samba에 nas 설정(가장 아래에 [nas] 추가)
```bash
sudo nano /etc/samba/smb.conf
```

```
[nas]
   path = /nas
   browseable = yes
   read only = no
   writable = yes
   valid users = @nasgroup
```

<br/>

## **4. DDNS 설정**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />
이것도 통신사마다 약간씩 다릅니다.
위 2번에서 접속하셨던 주소로 들어간다음 DDNS를 설정해주시면 됩니다.

<br/>

## **5. 연결 테스트**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

5.1 ) windows는 [내PC] 우클릭 -> 네트워크 드라이브 연결 -> DDNS 주소 기입 -> 포트번호 기입 -> id/pw 기입

5.2 ) android는 cx 파일 탐색기 기준으로 [네트워크] -> 새 저장소 -> 이하 위와 동일

> 여기서 내부 혹시DDNS로 접속이 안되는 분들께서는 ip 주소를 확인해보시기 바랍니다.  
내부 네트워크에서 접속하실때는 로컬ip[ ubuntu 명령어 : ip a ] 외부에서 접속할때는 공인 ip [ ubuntu 명령어 : curl ifconfig.me ]
{: .prompt-tip }


<br/>

## **2. 요약**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

1. Ubuntu server 설치(고정IP 추천)
2. sshd 포트 열어주기(기본 22번 포트이지만 보안상 바꾸는것을 추천)
3. samba 설정(Nas 구축을 위해)
4. 외부 접속용 모뎀 포트 열어주기
5. 유동 IP 대처를 위한 DDNS 설정

요약하자면 간단합니다! 여러분도 도전해보세요!

## **추후 예정된 사항**
<hr style="height: 0.5px; background-color: rgba(0, 0, 0, .1); border: none;" />

미러 서버와 토렌트를 구축해보고자합니다.  

미러서버는 보다 안정적인 파일 관리를 위함이고 토렌트는 서버를 보다 효율적으로 사용하기 위함입니다.  

또한 2편에서는 이번에 자세히 다루지못한 보안에 관련하여 다루도록 하겠습니다.  