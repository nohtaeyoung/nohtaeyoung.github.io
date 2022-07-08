---
layout: post
title: OSI 7Layer-2 Layer
subtitle: OSI 7계층-2계층
gh-repo: nohtaeyoung/nohtaeyoung.github.io
gh-badge: [star, fork, follow]
cover-img: /assets/img/security.jpg
tags: [network, OSI7 Layer,GitHub, infosec_oh_nohoooooo_tae_young, taeyoung noh]
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
# Unicast
- 단일(1:1) 장비로 데이터를 전송
- 원하는 대상에게만 데이터 전송 가능하다.
- 그렇기에 다른 장비에 부하를 주지 않는다.

# Broadcast
- 다수(1:N) 장비로 데이터를 전송
- 다수(1:N) 장비로 데이터를 전송
- 다수에게 보내다 보니 성능이 저하될 수 있는 단점이 있다.

# Multicast
- 특정그룹(1:특정그룹) 장비로 데이터를 전송
- 미리 약속된 그룹들이 있음 
- 이해가 안될 수 있으니 설명을 하면 아파트가 있다.<br>
근데 한 동에서 엘리베이터가 고장 났다. 그렇게 되면 굳이 브로드캐스트를 써서<br>
모든 주민들께 알려야 할까? 당연히 아니다. 그냥 고장난 동의 주민들에게만 알림 방송을 하면 된다.

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
- 2계층의 장비도 여러개가 있지만 대표적으로 swich와 bridge가 있다..<br>
  이것을 사전적으로 말하면 네트워크에서 물리적으로 장비를 연결하는 매체<br>
  우리가 평소에 생각하던 케이블의 정의와 얼추 비슷할 것이다.

## Cable의 종류(간단하게 알아보자)
- 동축 케이블
  - 동축케이블은 TV신호나 안테나같이 손실이 적어야 하는 장비들에 사용된다.

![동축](../assets/img/동축.png)

- 꼬임쌍선 케이블
  - 현재 LAN 구성에서 일반적으로 사용되고 있다. (LAN은 나중에 자세히 알아보자)

![꼬임쌍선](../assets/img/꼬임쌍선.png)

-시리얼 케이블
  - 직렬포트로 서로 연결하여 통신한다는데
  - 요즘에는 자주 사용이 안된다.

![시리얼](../assets/img/시리얼.png)

- 광 케이블
  -빛 신호를 이용하여 데이터를 전달하는 케이블이다.
  
![광](../assets/img/광.png)
  
## Hub & Repeater
  
# Repeater
- 리피터는 단순하게 우리가 신호를 보낼 떄 각 케이블마다의 일정거리가 넘어가게 되면 감쇠현상이 일어난다.<br>
  그때 리피터를 연결하면 거리가 연장된다.
  
  ![repeater](../assets/img/repeater.png)
    
# Hub
- 한쪽 포트로 전달받은 신호를 재생시켜 나머지 포트에 모두 전달한다.(자세한 설명은 아래에서)

![hub](../assets/img/hub.png)

## Hub 통신 방법
- 허브에는 여러개의 포트가 있다.
- 근데 한 포트에서 신호가 왔다.
- 그럼 목적지에만 신호를 보내는것이 아니고 본인의 포트에게 다 신호를 보낸다.
- 이것을 <p style="clore:red;"Flooding</p> 이라고 한다.
- 그러면 만약에 해커가 허브 포트와 연결된 장비의 ip주소로 변조 했다면 어떻게 될까?
- 당연히 그 신호 즉 데이터를 해커도 받는다는 보안성에 단점이 있다.

![osi flooding](../assets/img/flooding.png)

## 신호 전달 방식
# Simplex
- 단 방향 신호 전달
- 한 방향으로만 신호를 전달한다.
- ex) 방송국, 일방통행 도로

![simplex](../assets/img/simplex.png)

# Half-Duplex
- 반 이중 신호전달 방식
- 양 쪽 전송이 가능하지만 한 순간에 한 방향으로만 전달이 가능하다.
- ex) 무전기

![halfduplex](../assets/img/halfduplex.png)

# Full-Duplex
- 전 이중 신호전달 방식
- 동시에 양 방향으로 전달할 수 있음
- ex) 전화기

![fullduplex](../assets/img/fullduplex.png)

여기서 지금 우리가 배우고 있는 Hub는 어디에 해당할까?

답은 Half-Duplex이다!

## 하지만 Hub에는 통신에 큰 문제점이 하나 있는데!
- 그것은 경쟁을 통해 매체를 이용하고 신호를 전달하는 Hub의 특성상 신호의 충동이 일어나게 된다.
- 이것을 Collision Domain이라 하고 그래서 그것을 방지하기 위해 나온 것은! CSMA/CD!

## Collision Domain
- <p style="clore:red;">신호 충돌이 발생 가능한 영역을 Collision Domain이라 한다.</P>

![collisiondomain](../assets/img/collisiondomain.png)

## CSMA/CD
- Collision Domain에서 매체 접근의 우선순위를 지정하여 충돌을 예방하고 충돌이 발생한 경우 해결방법을
제시하는 기법이다.
- CSMA(Carrier Sense Multiple Access - 매체 사용 감지)
  -  <p style="clore:red;">충돌 예방</p>
  -  매체 감지 신호를 통해 매체 사용 가능 여부를 확인하고 신호를 전달 한다.
  -  매체 사용(busy)을 감지하면 일정한 대기 시간 후 다시 확인하고 전달 한다.
- CD(Collision Detection - 충돌 감지)
  -  <p style="clore:red;">충돌이 감지된 경우 재 충돌을 방지</p>
  -  충돌을 감지한 장비에서 충돌 감지 신호(JAM신호)를 전달하여 호스트에게 데이터 전송 중지를 알린다.
  -  충돌 감지 신호(JAM 신호)를 전달받은 모든 장비는 임의의 대기 시간 후 순서에 따라 신호를 전달 한다.

##  CSMA/CD 동작 방식
- CSMA(매체사용감지)기법으로 네트워크에 전송중인 데이터가 있는지 검사한 후 데이터를 전송한다.
- CD(충돌감지) 기법으로 충돌을 감지한다.
  - 충돌 발생 시 충돌감지신호를 만들어서 Flooding으로 모든 Collision Domain에 전송한다.
  - 충돌감지신호가 들어오면 모든 컴퓨터에서 랜덤시간으로 대기한 후 데이터를 전송한다.
 
