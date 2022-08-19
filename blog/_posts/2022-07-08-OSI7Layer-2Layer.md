---
layout: post
title: OSI 7Layer-2 Layer
subtitle: OSI 7계층-2계층
gh-repo: nohtaeyoung/nohtaeyoung.github.io
gh-badge: [star, fork, follow]
cover-img: /assets/img/security.jpg
tags: [Network]
comments: true
---


<br>
## OSI 7Layer 2Layer

- 우리가 친구에 카톡을 보낼 때 그 데이터들은 바로 친구한테 가는 것이 아니다..<br> 
다양한 근접 장비들을 통해 전달하고 또 전달해서 친구 카톡에 까지 전달 되는 것이다.<br>
우리가 소위 알고 있는 ip주소라는 것은 친구 휴대폰의 ip를 의미한다.<br>
그래서 통신에서는 바로 ip로 전달 되는 것이 아니기에 mac주소라는 것으로 전달하고<br>
그 장비들은 최적 경로를 통해 최종적으로 ip주소까지 절달된다.<br>
각 장비들을 우린 노드라 부르는데 그래서 2계층은 근접한 장비로 데이터를 보내준다 해서 node to node라 부른다.

![2계층](../assets/img/2계층.png)

## 그럼 mac 주소란 뭘까?
-  NIC(Network Interface Card)에 부여된 고유 식별 값이다.
-  조금 더 쉽게 말해 Network 통신에서 인접한 장비에 접근하기 위해 사용되는 장비의 고유 이름인 것이다.

## 데이터 전송방식
---------------------------------------------------------
# Unicast
- 단일(1:1) 장비로 데이터를 전송
- 원하는 대상에게만 데이터 전송 가능하다.
- 그렇기에 다른 장비에 부하를 주지 않는다.

![unicast](../assets/img/unicast.png)

# Broadcast
- 다수(1:N) 장비로 데이터를 전송
- 다수(1:N) 장비로 데이터를 전송
- 다수에게 보내다 보니 성능이 저하될 수 있는 단점이 있다.

![broadcast](../assets/img/broadcast.png)

# Multicast
- 특정그룹(1:특정그룹) 장비로 데이터를 전송
- 미리 약속된 그룹들이 있음 
- 이해가 안될 수 있으니 설명을 하면 아파트가 있다.<br>
근데 한 동에서 엘리베이터가 고장 났다. 그렇게 되면 굳이 브로드캐스트를 써서<br>
모든 주민들께 알려야 할까? 당연히 아니다. 그냥 고장난 동의 주민들에게만 알림 방송을 하면 된다.

![multicast](../assets/img/multicast.png)

## Ethernet Protocol
- 프토토콜은 약속이다. 그 계층간에 약속
- 2계층에서는 이더넷으로 약속하고 통신하기로 했다.

## 그럼 Ethernet은 뭐지?
- LAN을 위해 개발된 컴퓨터 네트워크 기술
- 네트워크에 연결된 각 기기들이 고유의 MAC 주소를 가지고, 이 주소를 이용해 상호간에 데이터를 주고 받
을 수 있도록 만들어진 기술
- 우리가 이더넷을 알아야하는 것은 현재 LAN의 90%가 이더넷을 사용하고 있다.

## Ethernet에 종류
- 이더넷에도 종류가 많지만 현재는 Ethernet v2와 IEEE802.3이 쓰인다.
- 이 중에서도 대부분 통신에서는 Ethernet v2가 쓰인다.

## 2계층의 장비
- 2계층의 장비도 여러개가 있지만 대표적으로 swich와 bridge가 있다.
---------------------------------------------------------------
# Bridge
- Full Duplex를 지원하며 신호 재생을 수행하는 장비이다.

![bridge](../assets/img/bridge.png)

# Switch(L2 Switch)
- Switching 동작을 수행할 수 있는 장비
- 2계층 프로토콜 정보를 해석하고 이용 가능한 장비
- MAC주소를 해석할 수 있기 때문에 목적지를 구별하여 데이터를 전달 한다.
- 즉 switch는 MAC 주소를 기반으로 통신을 하는 장비이다.

![switch](../assets/img/switch.png)

## 그럼 Switching이란 무엇인가?
- 네트워크에서 노드와 노드 간 연결을 중개해주는 것을 뜻합니다.
- 노드와 노드 간 모든 연결을 직접 구축할 수 없기 때문에,<br>
 마치 예전 전화를 연결시켜주는 전화 교환원과 같은 역할을 한다고 생각하면 된다.
 
## 이제 Switch의 통신 방법을 사진으로 알아보자!
 
 ![통신방식1](../assets/img/통신방식1.png)
 
 1 Switch로 데이터가 들어오면 SMAC 주소를 MAC Table에서 확인<br>
  1-1 없으면 MAC Table에 SMAC(출발지 mac주소) 주소를 기록(Learning)

![통신방식2](../assets/img/통신방식2.png)

2 DMAC(도착지 mac주소) 주소를 MAC Table에서 확인<br>
 2-1  없으면 Flooding

![통신방식3](../assets/img/통신방식3.png)

3 데이터를 받은 장비에서 자신의 데이터가 아니면 폐기

![통신방식4](../assets/img/통신방식4.png)

4 수신자가 다시 응답 데이터를 전송할 때 SMAC을 MAC Table에서 확인<br>
 4-1 없으면 MAC Table에 SMAC 주소를 기록(Learning)

![통신방식5](../assets/img/통신방식5.png)

5 DMAC 주소를 MAC Table에서 확인<br>
 5-1 있으면 해당 Port로만 데이터 전송(Filtering/Forwarding)

![통신방식6](../assets/img/통신방식6.png)

6 MAC Table에 SMAC 주소가 있는 경우 학습하지 않음<br>
 6-1 MAC Table에 DMAC 주소가 있는 경우 Flooding 하지 않고 <b style="color:red;">해당 목적지로만 데이터 전송</b><br>
(Filtering/Forwarding)

![통신방식7](../assets/img/통신방식7.png)

## Switch 기본기능
- 스위치가 알아서 자동으로 동작하는 기능 들
- Address Learning : 2계층 주소(MAC주소)를 학습하여 Table에 저장하는 기능
- Filtering : MAC Table에 일치하지 않는 경로로의 전송을 막아주는 기능
- Forwarding : MAC Table에 일치하는 경로로 전송해 주는 기능
- Flooding : 모든 경로로 데이터를 전송해 주는 기능
  - MAC Table에 없는 MAC 주소를 받은 경우
  - Broadcast/Multicast 데이터를 받은 경우
  - MAC Table이 가득 찬 경우
- Aging
  - MAC Table을 관리하기 위한 기법
  - 한번 사용된 MAC주소가 일정 시간 사용되지 않으면 삭제
  - Aging Time 기본 300초(5분)
  - 다시 사용되면 Aging Time 초기화
- Loop avoidance : Loop를 회피할 수 있는 기능

 ## Switching의 작동 방식- Switch가 알아서 손실률을 보고 동적으로 방식을 변경 함
- Store and Forward
  - 프레임을 모두 전송 받아 검사한 후 전달
  - FCS부터 체크하기 때문에 안정성이 높아짐
  - 속도가 떨어짐
- Cut-Through
  - 가장 빨리 전달하는 것(스위치의 기본값)
  - 목적지 주소까지 확인한 후 바로 전달
  - 안정성이 떨어짐
  - 속도가 빠름
- Fragment-Free
  - 프레임을 최소사이즈 64byte까지만 검사한 후 전달
  - 프레임의 64byte를 검사해서 FCS 가 있으면 Store and Forward 방식
  - FCS 가 없으면 Cut-Through
 
 <script src="https://giscus.app/client.js"
        data-repo="nohtaeyoung/nohtaeyoung.github.io"
        data-repo-id="R_kgDOHixriA"
        data-category="General"
        data-category-id="DIC_kwDOHixriM4CQSxP"
        data-mapping="pathname"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="top"
        data-theme="light"
        data-lang="ko"
        crossorigin="anonymous"
        async>
</script>

