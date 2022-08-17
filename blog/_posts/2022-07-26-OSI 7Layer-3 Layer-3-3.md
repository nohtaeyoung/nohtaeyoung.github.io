---
layout: post
title: OSI 7Layer-3 Layer -3-
subtitle: VLSM, Classful, Classless
gh-repo: nohtaeyoung/nohtaeyoung.github.io
gh-badge: [star, fork, follow]
cover-img: /assets/img/security.jpg
tags: [OSI 7Layer,Network]
comments: true
---


<br>

## VLSM(Varialble Length Subnet Mask)
- 가변 길이 Subnet Mask
- 하나의 네트워크 영역을 <b style="color:red"> 서로 다른 크기로 Subnetting</b> 하는 기법이다.
- 일반 Subnetting 모두 같은 크기로 Subnet이 생성 됨 -> IP낭비 현상 발생
- 필요한 크기에 맞춰서 Sub network를 생성 함 -> Sub network마다 다양한 Subnet mask를 이용 함

![vlsm1](../assets/img/vlsm1.png)

## VLSM 순서
1. 개수 확인<br> - 영역별 필요한 IP 개수 확인
2. <b sytle=color:red>Subnetting 순서 정하기</b><br> - IP가 가장 많이 필요한 영역부터 적게 필요한 영역 순으로 Subnetting
3. Subnet mask 구하기<br> - 2번에서 정한 순서대로 영역별 Subnet Mask 구하기<br> - 일반 Subnetting(host기준) 방식과 동일 함
4. Network 영역 구하기
5. Network 주소, Broadcast 주소, 할당 가능한 IP 범위 구하기

## VLSM 예제
<h3>시나리오</h3>
  - 할당 받은 Network: C Class 200.200.200.0 255.255.255.0
  - A팀 -> 50대, B팀 -> 100대, C팀 -> 10대

- 개수 확인
  - A팀 -> 50개 + 2 = 52 -> 52를 포함하는 2의 거듭제곱 값 -> 52 = <b style="color:red">2^6</b> -> 지수 값 6(6비트 유지)
  - B팀 -> 100개 + 2 = 102 -> 102를 포함하는 2의 거듭제곱 값 -> 102 = <b style="color:red">2^7</b> -> 지수 값 7(7비트 유지)
  - A팀 -> 10개 + 2 = 12 -> 12를 포함하는 2의 거듭제곱 값 -> 12 = <b style="color:red">2^4</b> -> 지수 값 4(4비트 유지)

- Subnetting 순서 정하기
  - 1순위 : B팀
  - 2순위 : A팀
  - 3순위 : C팀

- Subnet mask 구하기
  - 첫번째 네트워크 구하기(B팀 -> 2^7)
    - 할당 받은 Subnet mask -> 255.255.255.0
    - <b style="color:red">host ID bit의 오른쪽부터 Host ID(0) 유지(고정)</b>
    - 기존의 Net ID와 유지되는 Host ID 사이의 bit를 1로 변환하고 Subnet ID로 지정
  
![vlsm2](../assets/img/vlsm2.png)

  - 두번째 네트워크 구하기(A팀 -> 2^6)
    - <b style="color:red">첫번째 네트워크의 다음 Sub network를 기준으로 계산</b> -> 200.200.200.128(255.255.255.128)
    - 할당 받은 Subnet mask -> 255.255.255.128
    - <b style="color:red">host ID bit의 오른쪽부터 Host ID(0) 유지(고정)</b>
    - 기존의 Net ID와 유지되는 Host ID 사이의 bit를 1로 변환하고 Subnet ID로 지정

![vlsm3](../assets/img/vlsm3.png)

  - 세번째 네트워크 구하기(C팀 -> 2^4)
    - <b style="color:red">두번째 네트워크의 다음 Sub network를 기준으로 계산</b> -> 200.200.200.192(255.255.255.192)
    - 할당 받은 Subnet mask → 255.255.255.128
    - <b style="color:red">host ID bit의 오른쪽부터 Host ID(0) 유지(고정)</b>
    - 기존의 Net ID와 유지되는 Host ID 사이의 bit를 1로 변환하고 Subnet ID로 지정

![vlsm4](../assets/img/vlsm4.png)

- Network 영역 구하기
  - 첫번째 네트워크 구하기(B팀)
    - 할당 받은 대표 IP → 200.200.200.0 / Subnet mask → 255.255.255.128

![vlsm5](../assets/img/vlsm5.png)

- Network 주소, Broadcast 주소, 할당 가능한 IP 범위 구하기
  - B팀의 Sub network 정보

![vlsm6](../assets/img/vlsm6.png)

- Network 영역 구하기
  - 첫번째 네트워크 구하기(A팀)
    - 할당 받은 대표 IP → 200.200.200.128 / Subnet mask → 255.255.255.192

![vlsm7](../assets/img/vlsm7.png)

- Network 주소, Broadcast 주소, 할당 가능한 IP 범위 구하기
  - A팀의 Sub network 정보

![vlsm8](../assets/img/vlsm8.png)

- Network 영역 구하기
  - 첫번째 네트워크 구하기(C팀)
    - 할당 받은 대표 IP → 200.200.200.192 / Subnet mask → 255.255.255.240

![vlsm9](../assets/img/vlsm9.png)

## Classless Network
- Class 개념을 없애버리고 전체 IP를 통합하여 필요한 개수만큼만 나눠서 할당 함
- Netmask를 가변적으로 이용하여 IP 주소에서 Net ID와 Host ID를 구분 함

![vlsm10](../assets/img/vlsm10.png)

## Classful
- IP주소를 규격화된 크기(Class)별로 구분하는 방식
- IP 주소의 첫 번째 옥텟으로 Class 구분
- Class별 Net ID 영역 확인 후 해당 Network 영역으로 전달
- 하나의 네트워크에 할당할 수 있는 Host 개수가 정해져 있기 때문에 낭비되는 IP가 많아진다.

## Classless
- Class를 사용하지 않고 Bit 단위로 IP 주소 범위를 가변적으로 구분하는 방식
- IP 주소 낭비를 해결하기 위한 대안
- Subnet Mask 정보를 이용하여 Net ID영역을 확인 후 해당 Network 영역으로 전달
- CIDR 기법

## CLDR(Classless Inter-Domain Routing)
- Classless 환경에서 IP정보와 Subnetmask 정보를 함께 라우팅하는 기법
- 라우터에서 라우팅 테이블을 좀 더 효율적으로 관리할 수 있도록 한다.
- 접두어를 이용한 주소지정 방식으로 라우팅 부담을 줄여준다.
- Supernetting → 분리된 주소를 다시 그룹화 한다.

## CLDR 표기법
- Subnet mask를 Prefix 형식으로 표기 한다.
- Prefix 형식 → /(subnetmask의 Net ID 개수)

![vlsm11](../assets/img/vlsm11.png)


