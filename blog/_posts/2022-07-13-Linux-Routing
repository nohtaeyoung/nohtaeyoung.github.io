---
layout: post
title: Routing - Linux
subtitle: 리눅스로 라우팅
gh-repo: nohtaeyoung/nohtaeyoung.github.io
gh-badge: [star, fork, follow]
cover-img: /assets/img/security.jpg
tags: [network, Routing, System, Linux, GitHub, infosec_oh_nohoooooo_tae_young, taeyoung noh]
comments: true
---


## 초기 작업
{: .box-note}
블로그 내의 모든 예시와 실습은 VMware15 workstation, centos7(CLI 환경),Moboxterm,window xp, window 2003을 활용 합니다.<br>
또한 구성도의 가장 왼쪽의 있는 부분을 작업합니다.

< br>

{: .box-note}
vmware 상단에 edit->virtual network editor 클릭<br>
-> add network 클릭 vmnet2 클릭<br>
하단에 use local dhcp service to distribute ip address to vms 체크 해제(모든 네트워크에 체크 해제)

{: .box-note}
xp에는 setting -> network adepter -> custom-> vmnet2(host-only)<br>
2003에는 setting -> network adepter -> custom-> vmnet1(host-only)<br>



<br>
## 구성도

![리눅스 라우터 구성도1](../assets/img/리눅스 라우터 구성도1.png)

## Window XP ip 주소 설정

![리눅스 라우터 xp ip2](../assets/img/리눅스 라우터 xp ip2.png)

## Window 2003 ip 주소 설정

![리눅스 라우터 2003 ip3](../assets/img/리눅스 라우터 2003 ip3.png)

## Cent OS7 Network adepter 설정

![리눅스 라우터 centos 네트워크 추가4](../assets/img/리눅스 라우터 centos 네트워크 추가4.png)

## nmcli connection으로 네트워크 인터페이스 확인

![리눅스 라우터 인터페이스 확인5](../assets/img/리눅스 라우터 인터페이스 확인5.png)

## ens32 설정
- <b>vi /etc/sysconfig/network-scripts/ifcfg-ens32</b>
- 사진과 같이 설정 (UUID는 다를 수 있음)

![리눅스 라우터 ens32 설정 수정6](../assets/img/리눅스 라우터 ens32 설정 수정6.png)

## ens32 적용

![리눅스 라우터 ens32 적용7](../assets/img/리눅스 라우터 ens32 적용7.png)

## ip 주소 확인 명령어:ifconfig ens32

![리눅스 라우터 ens32 ip 확인8](../assets/img/리눅스 라우터 ens32 ip 확인8.png)

## 이제 moboxterm에서 ifconfig

![리눅스 라우터 모박스텀 접속9](../assets/img/리눅스 라우터 모박스텀 접속9.png)

## 주변 사람과 통신

![리눅스 라우터 주변사람 ping10](../assets/img/리눅스 라우터 주변사람 ping10.png)

## ens34 ens32로 복사
- /etc/sysconfig/network-scripts 하고 tab 치면 ens-32 외에는 나오지 않는다.<br>그럼 복사해서 만들어 주자

![리눅스 라우터 ens34 복사11](../assets/img/리눅스 라우터 ens34 복사11.png)

## ens 34를 만들어주자!

![리눅스 라우터 ens34 ip 설정 및 필요없는 부분 삭제12](../assets/img/리눅스 라우터 ens34 ip 설정 및 필요없는 부분 삭제12.png)

## ifconfig ens34로 확인

![리눅스 라우터 ens34 주소 확인13](../assets/img/리눅스 라우터 ens34 주소 확인13.png)

## ens35는 mac주소로 만들어주자!- mac주소 확인하기

![리눅스 라우터 ens35 mac주소 확보14](../assets/img/리눅스 라우터 ens35 mac주소 확보14.png)

## ens35 ens34로 파일로 복사하기

![리눅스 라우터 ens34 ens35로 복사15](../assets/img/리눅스 라우터 ens34 ens35로 복사15.png)

## ens35 파일을 수정하기 uuid 삭제 hwaddr 생성

![리눅스 라우터 ens35 mac주소로 설정16](../assets/img/리눅스 라우터 ens35 mac주소로 설정16.png)

## 윈도우XP, 윈도우2003, 외부 게이트웨이에 ping 통신

![리눅스 라우터 각pc에 ping 통신17](../assets/img/리눅스 라우터 각pc에 ping 통신17.png)

## 리눅스를 라우터로 만들기 작업 1

![리눅스 라우터 sysctl.conf18](../assets/img/리눅스 라우터 sysctl.conf18.png)

## 리눅스를 라우터로 만들기 작업 2
- 위 파일로 들어가 하단에 추가로 net.ipv4.ip_forward=1 추가

![리눅스 라우터 sysctl에 추가19](../assets/img/리눅스 라우터 sysctl에 추가19.png)

## 리눅스 라우터로 만들기 작업 3
- sysctl net.ipv4.ip_forward 명령어로 아래 사진 처럼 1이 됐는지 확인

![라우터로 만들기 3](../assets/img/라우터로 만들기 3.png)

## 리눅스 라우터로 만들기 최종
- route 명령어 입력하면 routing table이 나온다.

![리눅스 라우터 라우터로 만들기20](../assets/img/리눅스 라우터 라우터로 만들기20.png)

## 각 window에서 옆사람 ip로 ping 통신하고 종료
- 난 옆사람들이 PC를 끔... 확인 불가...
