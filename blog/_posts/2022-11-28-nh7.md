---
layout: post
title: DNS Spoofing
subtitle:Client Cache Poisoning
gh-repo: nohtaeyoung/nohtaeyoung.github.io
gh-badge: [star, fork, follow]
cover-img: /assets/img/security.jpg
tags: [Network Hacking]
comments: true
---

{: .box-note}
<b>블로그 내의 모든 예시와 실습은 VMware workstation16.2.3, Kali Linux 2022.03, Window XP, Window 2003을 활용 합니다.<br></b>

## DNS Attack
- 특정 Domain 주소로 전달되는 요청을 공격자가 원하는 목적지로 전달하게 한다.
- 주로 parming 공격을 수행하기 위해 준비한 서버로 유인하기 위한 목적으로 사용한다.
<br>

## DNS 취약점
- 질의에 대한 응답을 Cache에 저장한 후 Cache 저장된 정보를 재 사용 한다.
  - Cache가 한번 감염되면 지속적으로 공격이 수행 된다.
- UDP를 이용하여 일반적인 질의를 수행함 → 비 신뢰성, 비 연결성
- DNS 자체에 인증 메커니즘이 없다.
  - Transaction ID, Client Port의 일치 여부만 확인 한다.
<br>

## DNS Attack 분류
- DNS Spoofing → DNS Client의 Cache를 공격 → 한번의 공격으로 하나의 Client만 공격 한다.
- DNS Cache Poisoning → DNS Server의 Cache를 공격 → 한번의 공격으로 다수의 Client를 공격 한다.
<br>
## DNS Spoofing (Client)
- Client의 DNS Cache에 특정 도메인 주소에 해당하는 IP를 공격자가 원하는 IP로 변조하는 공격
- 한번만 DNS Cache를 감염시키면 DNS Cache Table이 만료되기 전까지 지속적인 공격이 가능 하다.
<br>

## DNS Client의 Domain 해석 순서
<h3 style="color:red">Domain 해석 요구 → → Hosts 파일 확인 DNS Cache 확인 → 질의(Query)</h3>
<br>

## DNS Spoofing(Client) 공격 조건
- DNS 자체의 인증 메커니즘은 없지만 요청과 응답을 연결하기 위한 <b style="color:red">Transaction ID</b>를 정확히 알아야 한다.
  -Sniffing공격으로 Client가 전송하는 요청을 획득하여 Transaction ID를 획득 해야 한다.
- UDP 자체의 인증 메커니즘은 없지만 요청과 응답을 연결하기 위한 <b style="color:red">Source Port</b>를 정확히 알아야 한다.
  - Sniffing공격으로 Client가 전송하는 요청을 획득하여 UDP의 Client port를 획득 해야 한다.
- DNS 질의에 대한 응답이 여러 개가 전달되는 경우 먼저 도착한 응답만 수용 한다.
  - 정상 DNS Server보다 <b style="color:red">응답을 먼저 전달</b>해야 한다.
<br>

## DNS Spoofing(Client) 공격 순서
- 공격 대상이 정상 DNS Server로 전달하는 DNS Query를 Sniffing 한다.
  - XID(Transaction ID), Source Port 획득
- 변조된 DNS응답을 전달할 Tool 동작 → dnsspoof
  - hosts 파일 형식으로 변조된 정보를 전달할 파일을 생성
  - 지정된 Domain 요청을 감지하면 지정된 IP로 DNS 응답을 피해자에게 전송 한다.
<br>

## DNS Spoofing 한계
- 클라이언트가 생성한 XID(Transaction ID)와 Source Port를 획득하기 위해 <b style="color:red">Sniffing 공격이 선행</b>되어야 한다.
- <b style="color:red">한 공격 당 하나의 대상</b>만 공격할 수 있다.
<br>

## Kali에서 fragrouter 실행

![dhcp spoofing1](../assets/img/dns_spoofing/dns_spoofing1.png)

## icmp redirect 공격 실행

![dhcp spoofing1](../assets/img/dns_spoofing/dns_spoofing2.png)

## xp 확인

![dhcp spoofing1](../assets/img/dns_spoofing/dns_spoofing3.png)

## Kali에서 spoof 에 응답할 파일을 작성(파일명:/root/dnsspoof.txt)

![dhcp spoofing1](../assets/img/dns_spoofing/dns_spoofing4.png)

## Kali에서 WireShark 실행 후 DNS Sfoof 공격

![dhcp spoofing1](../assets/img/dns_spoofing/dns_spoofing5.png)

## XP에서 Kali에서 등록한 주소로 접속

![dhcp spoofing1](../assets/img/dns_spoofing/dns_spoofing6.png)

## Wire Shark 확인

![dhcp spoofing1](../assets/img/dns_spoofing/dns_spoofing7.png)

![dhcp spoofing1](../assets/img/dns_spoofing/dns_spoofing8.png)

<b>203.248.252.2의 MAC주소가 Kali의 주소로 나온다.</b>

DNS Spoofing 공격은 항상 성공하는 것이 아니기 때문에 조심해야한다.
