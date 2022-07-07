---
layout: post
title: OSI 7Layer-1 Layer
subtitle: OSI 7계층-1계층
gh-repo: nohtaeyoung/nohtaeyoung.github.io
gh-badge: [star, fork, follow]
cover-img: /assets/img/security.jpg
tags: [network, OSI7 Layer,GitHub, infosec_oh_nohoooooo_tae_young, taeyoung noh]
comments: true
---


<br>
## OSI 7Layer 1Layer

- 우리가 예로 친구에게 카톡을 안녕이라고 보내게 되면 OSI 7계층에서 각자의 계층에서의 역할을 하고 1계층에 왔을 땐 그 데이터가 비트형태로 오게된다.<br> 
여기서 1계층은 마지막으로 우리가 보낸 카톡을 받을 친구에게 갈 수 있게 전기적 신호로 변환하여 보내주는 역할이다

## 1계층 주요 장비
-1계층의 주요 장비는 Cable, Connector,Ripeater,Hub 등이 있다.

## Cable, Connector
- 쉽게 우리는 케이블을 언제 쓰는가 장비를 연결할 때 케이블을 쓴다.<br>
  이것을 사전적으로 말하면 네트워크에서 물리적으로 장비를 연결하는 매체<br>
  우리가 평소에 생각하던 케이블의 정의와 얼추 비슷할 것이다.

## Cable의 종류(간단하게 알아보자)
- 동축 케이블
  - 동축케이블은 TV신호나 안테나같이 손실이 적어야 하는 장비들에 사용된다.

- 꼬임쌍선 케이블
  - 현재 LAN 구성에서 일반적으로 사용되고 있다. (LAN은 나중에 자세히 알아보자)

-시리얼 케이블
  - 직렬포트로 서로 연결하여 통신한다는데
  - 요즘에는 자주 사용이 안된다.

- 광 케이블
  -빛 신호를 이용하여 데이터를 전달하는 케이블이다.
  
## Hub & Repeater
  
# Repeater
- 리피터는 단순하게 우리가 신호를 보낼 떄 각 케이블마다의 일정거리가 넘어가게 되면 감쇠현상이 일어난다.<br>
  그때 리피터를 연결하면 거리가 연장된다.
    
# Hub
- 한쪽 포트로 전달받은 신호를 재생시켜 나머지 포트에 모두 전달한다.(자세한 설명은 아래에서)
 <td><img alt="../assets/img/repeater.png" src="../assets/img/hub.png" /></td>

## Hub 통신 방법
- 허브에는 여러개의 포트가 있다.
- 근데 한 포트에서 신호가 왔다.
- 그럼 목적지에만 신호를 보내는것이 아니고 본인의 포트에게 다 신호를 보낸다.
- 이것을 Flooding이라고 한다.
- 그러면 만약에 해커가 허브 포트와 연결된 장비의 ip주소로 변조 했다면 어떻게 될까?
- 당연히 그 신호 즉 데이터를 해커도 받는다는 보안성에 단점이 있다.
![osi flooding](../assets/img/osi7계층모델.png)

![osi 7계층 모델](../assets/img/osi7계층모델.png)

## TCP/IP Model

- 실제 통신에 사용되는 모델

![TCP/IP 모델](../assets/img/tcpip모델.png)

## Network Model 
- 1~4계층: 하위 계층(= 하드웨어 계층)
  - <span style="color:red">데이터 전달 계층</span>으로 주로 <b>네트워크 분야에서 참조</b>
- 5~7계층: 상위 계층(= 소프트웨어 계층)
  -  <span style="color:red">데이터 생성 계층</span>으로 주로 소프트웨어 개발 분야에서 참조

![상위 하위 계층](../assets/img/상위하위계층.png)

## 통신에 사용되는 주소
- 2,3,4계층에서 데이터 전달에 필요한 주소를 사용
- 4계층: 서비스 주소(Port 주소)
- 3계층: 논리적 주소(IP주소)
- 2계층: 물리적 주소(MAC 주소)

## 계층별 Network 장비

|Layer|장비|역할| 
| ------------------------------ | :--------------: | :----------------: |
|1계층|Cable|신호 전달|
|1계층|Repeater/Hub|신호 재생(거리연장)|
|2계층|Bridge/Switch|Switching<br> MAC 주소 구분|
|3계층|Router/L3 Switch|Routing<br> IP 주소 구분| 

## OSI 7 Reference Model(data 송신)

![osi 송신](../assets/img/osi 송신.png) 

## OSI 7 Reference Model(data 수신)

![osi 수신](../assets/img/osi 수신.png)

## Encapsulation
- 송신자 측에서 데이터를 전송할 때 상위계층에서 하위계층으로 내려오면서 순차적으로 데이터를 합쳐주는 과정

![encaqsulation](../assets/img/encapsulation.png)

## De-caqsulation
- 수신자 측에서 데이터를 전송 받은 후 하위계층부터 상위계층으로 올라오면서 순차적으로 데이터를 확인하며 떼어내는 과정

![decaqsulation](../assets/img/decapsulation.png)

## SDU(Service Data Unit)
- 상위 계층에서 내려온 데이터를 지칭
- 다른 말로 Payload 라고 부름

## PDU(Protocol Data Unit)
- 상위 계층에서 내려온 데이터에 해당 계층의 정보를 포함한 데이터를 지칭
- header + SDU + footer
- 계층별 PDU 명


| 계층 | PDU 명 |
| ------------------------------ | :--------------: | 
|Application| 
|Presentation|Message|
|Session|
|Transport|Segment| 
|Network|Packet|
|Data Link|Frame| 
|Physical|Bit| 

## OSI 7계층 정리

| ------------------------------ | :--------------: | :--------------: | :--------------: | :--------------: | 
|계층|기능|주소|Protocol|장비 
|7계층 Application<br>(응용 계층)|사용자 인터페이스 계층으로 사용자의 명령을 받으주는 계층(응용 프로그램)||HTTP, FTP, Telnet<br>SSH,DNS,DHCP,...||
|6계층 Presentation<br>(표현 계층)|상위계층에서 만들어진 데이터의 형태 표현<br>인코딩, 압축, 암호화 등에 대한 정보||||
|5계층 Session<br>(세션 계층)|특정 종류(연결이 필요한 종류)의 서비스를 받을 때만 사용<br>연결상태 제어|||| 
|4계층 Transport<br>(전송 계층)|데이터 전송방식 결정<br>서비스 구분(서비스 주소)<br>필요에 따라 단편화 작업 수행|Port 주소|TCP/UDP|L4 Switch|
|3계층 Network<br>(네트워크 계층)|출발지와 목적지의 주소 (논리적 주소 부여<br>-> 종단 간 연결 보장(end to end)|IP 주소|ICMP<br>IP<br>ARP,...|Router<br>L3 Switch| 
|2계층 Data Link<br>(데이터 링크 계층)|인접 장비에 접근하기 위한 정보(물리적 주소) 부여<br>->Node 간 연결 보장(node to node)<br>네트워크 환경에 맞는 정보 부여|MAC 주소|LAN: Ethernet<br>WAN: HDLC,PPP|Switch<br>Bridge|
|1계층 Physical<br>(물리 계층)|비트 형태의 신호를 패턴을 부여하여 전기적 신호로 변경하여 전송|||Cable, Connecter,<br>Hub,Repeater| 
