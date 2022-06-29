---
layout: post
title: Linux disk managment
subtitle: 리눅스에서 디스크 관리하는 방법
gh-repo: seokho-son/seokho-son.github.io
#gh-badge: [star, fork, follow]
cover-img: /assets/img/cat-taesik-wide.jpg
tags: [Linux, disk, GitHub, managment, infosec_oh_nohoooooo_tae_young, taeyoung noh]
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

![df 예 -h](../assets/img/simple-guide.gif)


## du

- disk usage
- 파일 및 디렉터리의 용량을 확인한다.

## du 예1 -sh [디렉토리]
- 디렉토리 전체 사용량 확인

![du 예 1](../assets/img/simple-guide.gif)

## du 예 -sh [디렉토리]/*
- 개별 디렉토리 사용량 확인

![du 예 2](../assets/img/simple-guide.gif)

## fdisk
- file system disk
- 파티션 테이블을 생성, 수정, 삭제를 할 수 있다.

## fdisk 예 -l
- 현재 파일 시스템의 파티션 정보를 확인 하고 싶을 때
![fdisk 예 1](../assets/img/simple-guide.gif)

## fdisk 예 디스크 추가 확인
- 일단 사용중인 시스템을 종료  합니다.
- VMware에서 edit virtual setting을 클릭한다.
- 하단에 add를 클릭한다.
- Hard Disk를 클릭하고 Next -> SCSI -> Create a new virtual disk-> 40G 바꾸고 하단에 Store virtual disk as a single file -> finish -> OK
- 리눅스 시스템 로그인 후 시스템의 파티션 테이블을 확인 한다.(fdisk -l)
![fdisk 예 2](../assets/img/simple-guide.gif)

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
![fdisk 예 3](../assets/img/simple-guide.gif)
- 1번 파티션에  주 파티션 생성
![fdisk 예 2-1](../assets/img/simple-guide.gif)
- 2번 파티션에 확장 파티션 생성
![fdisk 예 2-2](../assets/img/simple-guide.gif)
- 확장 파티션에 논리 파티션 생성(2GB)
![fdisk 예 2-3](../assets/img/simple-guide.gif)
- 파티션 정보 확인
![fdisk 예 2-4](../assets/img/simple-guide.gif)
- 파티션 타입 변경(5번 파티션을 Swap 타입으로 설정
![fdisk 예 2-5](../assets/img/simple-guide.gif)
-설정 정보 저장 후 디스크 관리모드 종료
![fdisk 예 2-6](../assets/img/simple-guide.gif)

## mkfs
- 파일 시스템 생성 명령어
## 사용법 및 옵션
- # mkfs [옵션] [장치 이름

{: .box-note}
-t[종류]: 파일 시스템의 종류 선택
-c: 파일 시스템을 생성하기 전에 bad block을 검사 함
-v: 작업 상태와 결과를 자세히 출력 함

- 파일 시스템 생성(/dev/sdb1 장치에 ext4 파일 시스템 생성)
![file system 예 1](../assets/img/simple-guide.gif)

## 마운트(Mount)
- 운영체제가 물리적인 장치를 이용할 수 있도록 연결 한다.
- Linux OS는 모든 장치를 파일 단위로 관리하기 때문에 새로 추가된 장치는 임의의 디렉터리(mount point)에 연결 시켜서 사용해야 한다.

## 마운트 포인트
- 하드 디스크를 운영체제로 연결할 때 사용한 디렉터리
- 사용 중이던 디렉토리를 마운트 포인트로 이용할 경우 존재하던 파일과 디렉토리에 접근할 수 없게 되므로 마운트 포이트는 비어 있는 디렉토리를 사용(마운트 포인트 해제 시 기존의 파일 및 디렉토리에 접근 가능)

## mount 명령어
- 파일 시스템 마운트 명령

## 사용법 및 옵션
- # mount [-t 파일시스템 유형][-o 옵션][장치 이름][마운트 포인트]

{: .box-note}
async: 마운트된 파일시스템에 비 동기 입출력을 사용<br>
auto: /etc/fstab에 지정된 파일시스템에 대해 부팅 시에 자동으로 마운트<br> 
defaults: rw,suid,dev,exec,auto, nouser, async를 종합적으로 사용<br>
dev: 해당 파일 시스템을 문자 디바이스나 블록 디바이스를 이용해 해석<br>
exec: 파일 시스템에 포함된 프로그램을 실행 할 수 있도록 함<br>
noauto: 자동 마운트가 되지 않도록 함<br>
noexec: 해당 파일 시스템의 프로그램이 실행되지 않도록 함, 특정 보안 목적을 위해 사용<br>
nosuid: 실행 파일에 존재하는 suid, sgid 비트의 기능 제한<br>
nouser: 루트(root) 외에 사용자가 파일 시스템을 마운트 하거나 언마운트 하는 것을 제한



### 동영상 가이드

[동영상 가이드: 약 10분](https://www.youtube.com/watch?v=UgPZXxL2jSw)

<iframe width="770" height="432" src="https://www.youtube.com/embed/UgPZXxL2jSw" frameborder="0" allowfullscreen></iframe>

<br>

### 간단 GIF 가이드

가이드를 19 단계의 애니메이션으로 표현

![간단 가이드](../assets/img/simple-guide.gif)

<br>

### 상세 설명

1. GitHub 계정이 없는 경우, GitHub 계정을 생성하고 이메일 인증을 수행합니다.

   1. GitHub 계정 생성
      ![GitHub 계정 생성](../assets/img/githubpage-guide/p1.jpg)

   1. GitHub 계정 이메일 인증
      ![GitHub 계정 이메일 인증](../assets/img/githubpage-guide/p2.jpg)

1. 웹사이트의 기본 소스를 제공하는 GitHub 저장소에 접속하고, `Fork` 를 통해 해당 저장소를 본인의 GitHub 계정으로 복제합니다.

    1. [https://github.com/seokho-son/seokho-son.github.io](https://github.com/seokho-son/seokho-son.github.io) 저장소에 접속
       ![GitHub 저장소 접속](../assets/img/githubpage-guide/g2.jpg)

    1. [https://seokho-son.github.io](https://seokho-son.github.io) 접속을 통해 데모 웹사이트 확인
       ![GitHub Page 접속](../assets/img/githubpage-guide/g1.jpg)

    1. GitHub의 `Fork` 기능을 통해 저장소를 본인의 GitHub 계정으로 복제
       ![GitHub 포크](../assets/img/githubpage-guide/g3.jpg)

       `Fork` 는 Git 저장소를 복제 및 기존 저장소와 연계시키는 기능 (보통 공동 작업을 위한 방법)

    1. 본인 계정에 복제된 저장소 확인
       ![GitHub 포크 확인](../assets/img/githubpage-guide/g5.jpg)

1. GitHub Page 활성화를 위해 저장소 명칭 변경

    1. `Settings` 탭을 선택하고 `Repository name` 을 `계정이름.github.io` 로 변경
        ![저장소 이름 변경](../assets/img/githubpage-guide/g7.jpg)

    GitHub는 `계정이름.github.io` 인 저장소에 대해 자동으로 소스코드 빌드 및 호스팅을 수행함

    1. 자동 생성된 웹사이트 확인
        ![자동 생성 웹사이트 확인](../assets/img/githubpage-guide/g8.jpg)


1. 자신의 웹사이트로 내용 커스터마이징

    1. `_config.yml` 파일을 선택하여 내용 수정 및 저장소에 수정 사항 반영

        `_config.yml` 파일은 웹사이트의 설정 정보가 포함되어 있음. `수정필요` 로 코멘트된 사항에 대해 커스터마이징 진행.

        ![컨피그 확인](../assets/img/githubpage-guide/g9.jpg)

        ![컨피그 수정](../assets/img/githubpage-guide/g10.jpg)

        ![컨피그 수정2](../assets/img/githubpage-guide/g11.jpg)

        ![컨피그 커밋](../assets/img/githubpage-guide/g12.jpg)

        `Commit` (`git commit`)은 어려가지 변경 사항에 대한 스넵샷을 제공하는 기능임. 수정 사항을 저장소에 반영하기 위해서는 `Commit` 이라는 행위를 필수적으로 수행해야 함.

    1. `index.md` 파일을 선택하여 내용 수정 및 저장소에 수정 사항 반영

        ![인덱스 확인](../assets/img/githubpage-guide/g13.jpg)

        ![인덱스 수정](../assets/img/githubpage-guide/g14.jpg)

        ![인덱스 커밋](../assets/img/githubpage-guide/g15.jpg)

        `index.md` 는 웹사이트에서 첫 페이지(`home`)의 소스 파일임. 커스터마이징 진행.

        `.md` 파일은 [마크다운 언어](https://ko.wikipedia.org/wiki/마크다운)으로 작성되는 것을 의미함.

    1. `carrer.md` , `publication.md` 등 `*.md` 에 대해서도 커스터마이징 진행


1. 내용이 업데이트된 웹사이트 최종 확인
    ![업데이트된 웹사이트](../assets/img/githubpage-guide/g17.jpg)

끝.
