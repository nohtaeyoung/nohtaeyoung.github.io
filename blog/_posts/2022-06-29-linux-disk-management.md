---
layout: post
title: Linux disk management
subtitle: 리눅스에서 디스크 관리하는 방법
gh-repo: nohtaeyoung/nohtaeyoung.github.io
gh-badge: [star, fork, follow]
cover-img: /assets/img/security.jpg
tags: [Linux]
comments: true
---


{: .box-note}
블로그 내의 모든 예시와 실습은 VMware15.5버전(다른 버전도 가능)과 Centos7(Centos7 사용권장 "다른 리눅스나 버전에서도 가능")을 사용합니다.

<br>
## df

- disk free
- 파일 시스템에 할당된 전체 용량, 사용량, 사용 가능 용량, 사용률, 마운트 정보 등을 확인하는 명령어
- 관리자 계정이 아닌 일반 사용자도 사용이 가능하다.


## df 예 -h

- 디스크 용량을 MB(Mega Byte) 단위로 표시

![df 예 -h](../assets/img/df예 -h.png)


## du

- disk usage
- 파일 및 디렉터리의 용량을 확인한다.

## du 예1 -sh [디렉토리]
- 디렉토리 전체 사용량 확인

![du 예 1](../assets/img/du 예 1.png)

## du 예 -sh [디렉토리]/*
- 개별 디렉토리 사용량 확인

![du 예 2](../assets/img/du 예 2.png)

## fdisk
- file system disk
- 파티션 테이블을 생성, 수정, 삭제를 할 수 있다.

## fdisk 예 -l
- 현재 파일 시스템의 파티션 정보를 확인 하고 싶을 때

![fdisk 예 1](../assets/img/fdisk 예 1.png)

## fdisk 예 디스크 추가 확인
- 일단 사용중인 시스템을 종료  합니다.
- VMware에서 edit virtual setting을 클릭한다.
- 하단에 add를 클릭한다.
- Hard Disk를 클릭하고 Next -> SCSI -> Create a new virtual disk-> 40G 바꾸고 하단에 Store virtual disk as a single file -> finish -> OK
- 리눅스 시스템 로그인 후 시스템의 파티션 테이블을 확인 한다.(fdisk -l)

![fdisk 예 2](../assets/img/fdisk 예 2.png)

## fdisk 예 파티션 설정
- fdisk 관리 모드 설정 명령

  {: .box-note}
  a: 부팅 파티션을 설정<br>
  d: 파티션 삭제<br>
  l: 설정 가능한 파티션 타입 출력<br>
  m: 파티션 설정 도움말 출력<br>
  n: 새로운 파티션 생성<br>
  p: 현재 설정되어 있는 파티션 정보 출력<br>
  t: 파티션 타입 변경<br>
  q: fdisk 메뉴 빠져나가기<br>
  w: 작업 내용 저장

- fdisk /dev/sdb 입력

![fdisk 예 3](../assets/img/fdisk 예 3.png)

- 1번 파티션에  주 파티션 생성

![fdisk 예 3-1](../assets/img/fdisk 예 3-1.png)

- 2번 파티션에 확장 파티션 생성

![fdisk 예 3-2](../assets/img/fdisk 예 3-2.png)

- 확장 파티션에 논리 파티션 생성(2GB)

![fdisk 예 3-3](../assets/img/fdisk 예 3-3.png)

- 파티션 정보 확인

![fdisk 예 3-4](../assets/img/fdisk 예 3-4.png)

- 파티션 타입 변경(5번 파티션을 Swap 타입으로 설정
 
![fdisk 예 3-5](../assets/img/fdisk 예 3-5.png)

-설정 정보 저장 후 디스크 관리모드 종료

![fdisk 예 3-6](../assets/img/fdisk 예 3-6.png)

## mkfs
- 파일 시스템 생성 명령어
## 사용법 및 옵션
- mkfs [옵션] [장치 이름]

{: .box-note}
-t[종류]: 파일 시스템의 종류 선택<br>
-c: 파일 시스템을 생성하기 전에 bad block을 검사 함<br>
-v: 작업 상태와 결과를 자세히 출력 함<br>

- 파일 시스템 생성(/dev/sdb1 장치에 ext4 파일 시스템 생성)

![file system 예 1](../assets/img/file system 예 1.png)

## 마운트(Mount)
- 운영체제가 물리적인 장치를 이용할 수 있도록 연결 한다.
- Linux OS는 모든 장치를 파일 단위로 관리하기 때문에 새로 추가된 장치는 임의의 디렉터리(mount point)에 연결 시켜서 사용해야 한다.

## 마운트 포인트
- 하드 디스크를 운영체제로 연결할 때 사용한 디렉터리
- 사용 중이던 디렉토리를 마운트 포인트로 이용할 경우 존재하던 파일과 디렉토리에 접근할 수 없게 되므로 마운트 포이트는 비어 있는 디렉토리를 사용(마운트 포인트 해제 시 기존의 파일 및 디렉토리에 접근 가능)

## mount 명령어
- 파일 시스템 마운트 명령

## 사용법 및 옵션
- mount [-t 파일시스템 유형][-o 옵션][장치 이름][마운트 포인트]

{: .box-note}
async: 마운트된 파일시스템에 비 동기 입출력을 사용<br>
auto: /etc/fstab에 지정된 파일시스템에 대해 부팅 시에 자동으로 마운트<br> 
defaults: rw,suid,dev,exec,auto, nouser, async를 종합적으로 사용<br>
dev: 해당 파일 시스템을 문자 디바이스나 블록 디바이스를 이용해 해석<br>
exec: 파일 시스템에 포함된 프로그램을 실행 할 수 있도록 함<br>
noauto: 자동 마운트가 되지 않도록 함<br>
noexec: 해당 파일 시스템의 프로그램이 실행되지 않도록 함, 특정 보안 목적을 위해 사용<br>
nosuid: 실행 파일에 존재하는 suid, sgid 비트의 기능 제한<br>
nouser: 루트(root) 외에 사용자가 파일 시스템을 마운트 하거나 언마운트 하는 것을 제한<br>
ro: 읽기 전용으로 마운트<br>
rw: 읽기와 쓰기가 가능하도록 마운트<br>
suid: 실행 파일의 존재하는 suid,sgid 비트의 기능을 사용<br>
sync: 마운트된 파일시스템에 동기식 입출력을 사용<br>
user: 일반 사용자의 파일시스템 마운트 허용<br>
users: 모든 일반 사용자가 파일시스템 마운트, 언마운트가 가능하도록 허용<br>
noatime: access time을 기록하지 않음, 자주 파일에 엑세스 할 경우 유용하다. 

## umount
- 마운트를 해제하는 명령어
- 즉 운영체제와 장치를 해제하는 명령어이다.

## 사용법
- umount [마운트 포인터]

## 파일 시스템 언마운트 예

![umount 예 1](../assets/img/umount 예제 1.png)

## 파일 시스템 마운트 관리 파일(/etc/fstab)
- 리눅스가 부팅되면서 파일 시스템을 어디에 자동으로 마운트하고, 외부 장치들에 대한 마운트를 어떻게 설
정하는지, 권한 및 복구 등의 옵션을 어떻게 이용할 지 지정하는 파일
- 시스템 부팅 시 /etc/fstab에 기록되어 있는 순서대로 파티션이 마운트 되어 한 개의 디렉토리 트리가 만들
어 짐

## 예시
![fstab 예 1](../assets/img/fstab 예 1.png)

## fstab 확인
- cat /etc/fstab
-  ①UUID=ec78d766-639a-4c6e-80a5-627449f11768 ②/ ③ext4 ④defaults ⑤1 ⑥1

![fstab 예 2](../assets/img/fstab 예 2.png)

## UUID(Universally Unique IDentifier)
- 16Byte(128Bit)로 이루어진 규격화된 숫자이다.
- 네트워크 상에서 서로 모르는 개체들을 식별하고 구별하기 위한 고유한 이름이다.
- 중앙 관리 시스템이 없는 분산 시스템에서 정보를 유일하게 식별하기 위한 값이다.

## UUID 확인
- blkid

![uuid 예 1](../assets/img/uuid 예 1.png)

## Disk 최종 실습(개인적으로 풀어보기)
- 20GB 크기를 가진 하드디스크 추가 장착
- 1번 파티션은 기본 파티션으로 8GB 용량으로 분할
- 2번 파티션은 확장 파티션으로 12GB 용량으로 분할 후 4GB를 가지는 논리 파티션 추가
- 각각 두 개의 파티션을 ext4 파일시스템 유형으로 포맷
- 기본 파티션은 /game에 마운트
- 논리 파티션은 /music에 마운트

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
