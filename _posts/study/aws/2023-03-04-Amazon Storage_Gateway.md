---
layout: post
title: "[AWS] Storage Gateway"
subtitle: AWS
date: '2023-03-04 00:00:02 +0900'
category: study
tags: aws aws-base
image:
  path: /assets/img/study_AWS/aws_logo.png
---

# AWS Storage Gateway 이해
AWS에서 제공하는 **AWS Storage Gateway**를 이해해보자.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## AWS Storage Gateway 개요

AWS에서 소개하는 `Storage Gateway 설명`을 보면
> **AWS Storage Gateway**는 `사실상 무제한의 클라우드 스토리지`에 대한 `온프레미스에게 액세스 권한을 제공`하는 **하이브리드 클라우드 스토리지 서비스**입니다. Storage Gateway를 사용하는 고객은 하이브리드 클라우드 스토리지의 주요 사용 사례인 `스토리지 관리 간소화 및 비용 절감 효과`를 얻을 수 있습니다. 여기에는 `테이프 백업을 클라우드로 이동`하고, `클라우드 백업 파일 공유`를 통해 `온프레미스 스토리지를 최소화`하고, `온프레미스` 애플리케이션의 `AWS 데이터(클라우드)`에 대한 `짧은 지연 시간의 액세스 권한`을 제공하는 기능과 함께 `다양한 마이그레이션, 아카이빙, 프로세싱, 재해 복구 사용` 사례가 포함됩니다. <br>
> 이러한 사용 사례를 지원하기 위해 **테이프 게이트웨이**, **파일 게이트웨이 및 볼륨 게이트웨이**와 같은 3가지 유형의 게이트웨이를 제공합니다. 이러한 게이트웨이는 온프레미스 애플리케이션을 클라우드 스토리지에 원활하게 연결하여 짧은 지연 시간의 액세스를 위해 **로컬에서 데이터를 캐싱**합니다. 애플리케이션은 **NFS**, **SMB 및 iSCSI**와 같은 `표준 스토리지 프로토콜`을 사용하는 `하드웨어 게이트웨이 어플라이언스(가상 머신)`를 통해 이 `서비스에 연결`됩니다. 이 게이트웨이는 **Amazon S3**, **Amazon S3 Glacier**, **Amazon S3 Glacier Deep Archive**, **Amazon EBS**, **AWS Backup**과 같은 **AWS 스토리지 서비스에 연결**하여 AWS에서 `파일, 볼륨, 스냅샷 및 가상 테이프용 스토리지를 제공`합니다. 이 서비스에는 `대역폭 관리`, `자동화된 네트워크 복원력` 및 `효율적인 데이터 전송`과 같은 고도로 **최적화된 데이터 전송 매커니즘**이 포함됩니다.

간단히 말하면, `Storage Gateway`는 **백업 툴**이며 AWS에서 `기존의 온프레미스 환경의 데이터센터`를 운영하고 있는 고객을 대상으로 `백업 전용 게이트웨이를 사용`할 수 있도록 만든 서비스

아래는 Storage Gateway의 `간단한 사용 구조도`로

![archi](/assets/img/study_AWS/[AWS]_Storage_Gateway_이해/archi.png)

이처럼 이미 운영중인 `데이터센터에 Appliance를 설치`하고 `Storage Gateway를 통해 S3에 백업`을 하고, `S3에 저장된 데이터로 분석`하는 등의 기능을 할 수 있습니다.

<hr/>

## AWS Storage Gateway 옵션

Storage Gateway는 총 `3가지의 옵션`으로 구성

### 1. File Gateway(NFS, SMB)

  * **NFS : Network File System**
    + `for Linux`
    + NFS를 제공하는 AWS 서비스 : `EFS`

  * **SMB : Server Message Block**
    + `for Windows`

  * `NFS, SMB 마운트 포인트로` 전송받은 `데이터를 S3에 저장`
    + 소유권, 퍼미션, 파일 생성 시간등의 `설정은 S3의 메타데이터로 저장`
    + `S3는 오브젝트 저장소`이기 때문에 `일반적인 하드웨어에서 읽는 파일과는 다르므로 NFS, SMB등을 통해 액세스 가능`

  * S3에 저장후에는 `S3의 모든 기능 활용 가능`
    + `이벤트 트리거`를 통한 다른 서비스(Lambda, Athena, 분석 서비스 등) 사용
    + 버저닝
    + 수명 주기 등등

### 2. Volume Gateway(iSCSI)

  * **Stored Volume : 모든 데이터를 로컬에 저장하고 비동기적으로 AWS에 백업**
    + 1GB ~ 16TB
  
  * **Cached Volume : 자주 사용되는 데이터만 로컬에 남겨두고 나머지는 모두 AWS에 백업**
    + 1GB ~ 32TB

  * `iSCSI 프로토콜`을 통해 전달받은 `데이터를 비동기적으로 EBS 스냅샷 형식으로 저장`
    + 스냅샷은 `증분식(Incremental)` -> 이전 스냅샷에서 바뀐 부분만 저장함
    + `주로 백업 용도`로 사용함

  * **Block Storage를 위해 사용 가능**

### 3. Tape Gateway(VTL, Virtual Tape Library)

  * `이미 존재하는 Tape 기반 백업` 애플리케이션을 위한 서비스

  * `iSCSI 디바이스로 백업`

  * NetBackup, Backup Exec 등등 기존의 `백업 애플리케이션 사용 가능`

<hr/>

## AWS Storage Gateway 개념

  * 하이브리드 환경으로 `온프레미스와 클라우드의 저장 서비스를 연동`하기 위한 서비스

  * **Storage Gateway Appliance 사용**
    + `가상머신(VM)으로 온프레미스 데이터센터에 설치`하여 데이터를 `수집 및 전송`
    + 또는 AWS로부터 하드웨어를 구매해 설치 가능
    + [DataSync]의 `Agent`와 비슷한 역할

<hr/>

* Ref
  - [Youtube](https://youtu.be/gjlRurFnYeg)

