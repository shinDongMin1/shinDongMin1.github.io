---
layout: post
title: "[AWS-SAA] Examtopics 131~140"
subtitle: AWS
date: '2023-03-23 00:00:01 +0900'
category: study
tags: aws aws-saa
image:
  path: /assets/img/study_AWS/saa-co2_logo.png
---

SAA Examtopics 131~140번 문제를 풀어보자.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## Prob. 131

사용자는 쿼리에서 최대 100밀리초의 지연을 예상하는 다양한 고객이 사용하는 MySQL 데이터베이스를 소유하고 있습니다. 항목이 데이터베이스에 기록되면 거의 수정되지 않습니다. 클라이언트는 한 번에 최대 하나의 레코드에 액세스할 수 있습니다.
증가하는 고객 요구로 인해 데이터베이스 액세스가 엄청나게 확장되었습니다. 결과적으로 결과 부하는 사용 가능한 가장 값비싼 하드웨어의 용량을 빠르게 능가합니다. 사용자는 AWS로 이동하기를 원하며 새로운 데이터베이스 시스템을 실험할 준비가 되어 있습니다.

데이터베이스 로드 문제를 해결하고 거의 무한한 미래 확장성을 제공하는 솔루션은 무엇입니까?

A. Amazon RDS

B. Amazon DynamoDB

C. Amazon Redshift

D. AWS Data Pipeline

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

데이터베이스 로드 문제를 해결하고 거의 무한한 미래 확장성을 제공 문제 요점.

로드 -> 처리량 <br>
트래픽 -> 요청

**AWS RDS VS AWS Aurora** <br>
기존 데이터베이스 아키텍처를 중심으로 완전히 관리되는 추상화 계층을 제공. <br>
EC2에서 수동으로 수행하는 것처럼 구축. <br>
EC2인스턴스는 적절한 Amazon Machine Image (AMI)에서 프로비저닝 되고, EBS(Elastic Block Store)스토리지는 프로비저닝된 인스턴스에 연결 그리고 적절한 서브넷 그룹과 보안그룹이 인스턴스에 연결되는 구조. <br>
RDS는 백업/복원 및 패치가 모두 자동.
* 트랜잭션 로그 및 데이터베이스 데이터 파일은 로컬 EBS 스토리지 볼륨 사용.
* 데이터베이스의 모든 커밋된 트랜잭션 I/O 는 WAL(Write-Ahead Log)이라고 하는 전후 이미지가 있는 로그 레코드를 생성한 후 지속가능한 스토리지로 저장.
* 체크포인트 작업은 수정된 페이지를 디스크로 플러시하여 수행
* EC2 인스턴스에 생성되기 때문에 I/O 대역폭 및 IOPS로 인해 성능이 제한됨.
* 튜닝에는 I/O 대역폭을 늘리거나 I/O 수를 줄여야 함.

기존 RDS의 모든 관리 기능 뿐만 아니라 데이터베이스에 최적화된 스토리지 하위 시스템을 제공하여 RDS 플랫폼을 확장한다. RDS에서 사용하는 EBS 스토리지 대신 NVMe SSD 드라이브 위에 구축되어 훨씬 빠른 성능 이점을 제공.
* 애플리케이션에 따라 자동으로 확장.
* 6개의 데이터 복사본을 만들어 여러 위치에 배포하고 Amazon S3에 지속적으로 백업.
* 99.99% 이상의 가용성 제공.
* 스토리지 장애로부터 투명하게 복구.
* 일반 적으로 30초 미만의 인스턴스 장애조치 허용.
* 이전 시점으로 빠르게 복구할 수 있는 기능 제공.

**Amazon DynamoDB** <br>
Amazon DynamoDB는 모든 규모에서 밀리초 단위의 단일 자릿수 성능을 제공하는 키 값 및 문서 데이터베이스입니다. <br>
이 데이터베이스는 인터넷 규모의 애플리케이션을 위한 내장형 보안, 백업 및 복원, 메모리 내 캐시을 통해 완벽하게 관리되는 다중 영역, 다중 활성 및 내구성이 뛰어난 데이터베이스입니다. <br>
DynamoDB는 매일 10조 개 이상의 요청을 처리할 수 있으며 초당 2,000만 개 이상의 요청을 지원할 수 있습니다. <br>
WORM - 쓰기 한번에 읽기 많이.

**AWS Data Pipeline** <br>
AWS Data Pipeline은 데이터의 이동과 변환을 자동화하는 데 사용할 수 있는 웹 서비스. <br>
데이터 중심 워크플로우를 정의할 수 있어 성공적으로 완료한 이전 작업을 바탕으로 작업을 수행할 수 있습니다. 데이터 변환의 파라미터를 정의하면 AWS Data Pipeline이 여러분이 설정한 로직을 실행.

A 탈락 -> RDS는 EBS기반으로 관계형 DB 기술로 EC2에서 수행하여 부적합.

B 정답 -> 위에서 말한 것처럼 DynamoDB는 NoSQL이지만 키-값으로 이루어진 JSON같은 파일로 레코드로 접근하는 것보다 처리속도가 빨라서 적합.

C 탈락 -> Redshift는 데이터를 분석하는 기술이라 부적합.

D 탈락 -> Data Pipeline는 데이터 이동과 변환하는 기술이라 부적합.

</div>
</details>

<hr/>

## Prob. 132

Amazon DynamoDB는 엔터테인먼트 회사에서 미디어 메타데이터를 저장하는 데 사용하고 있습니다. 응용 프로그램은 광범위한 읽기가 필요하며 종종 지연이 발생합니다. 조직에는 추가 운영 비용을 관리하는 데 필요한 인력이 부족하고 애플리케이션을 변경하지 않고 DynamoDB의 성능 효율성을 높여야 합니다.

이 요구 사항을 충족하려면 어떤 솔루션 아키텍처 접근 방식을 권장해야 합니까?

A. Redis에는 Amazon ElastiCache를 사용합니다.

B. DAX(Amazon DynamoDB Accelerator)를 사용합니다.

C. DynamoDB 글로벌 테이블을 사용하여 데이터를 복제합니다.

D. Auto Discovery가 활성화된 Memcached에 Amazon ElastiCache를 사용합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

애플리케이션을 변경하지 않고 DynamoDB의 성능 효율성 문제 요점.

종종 지연이 발생. <br>
메타데이터는 데이터형식의 정보로 스키마 같은 것을 저장.

**Amazon ElastiCache** <br>
클라우드에서 분산된 인-메모리 데이터 스토어 또는 `캐시 환경을 손쉽게 설정, 관리 및 확장`할 수 있는 웹 서비스입니다. <br>
확장 가능/비용 효율적인 고성능 캐싱 솔루션을 제공. <br>
배포 및 관리와 관련된 복잡성을 해소.

인-메모리 캐시는 모든 데이터를 메모리(RAM)에만 올려놓고 사용하는 데이터베이스의 일종입니다. <br>
클라우드 환경에서 느린 디스크 기반 데이터베이스에 의존하는 것보다 더 빠른 인-메모리 데이터 스토어를 사용해 데이터 집약적 앱을 구축/기존 데이터베이스 성능을 강화함. <br>
하지만 응답 시간은 마이크로초 대기 시간을 일관되게 유지할 수 없습니다.

`두 가지` 오픈 소스 인-메모리 엔진을 지원.
* **Memcached**
* 널리 채택된 메모리 객체 캐싱 시스템.
* ElastiCache는 `Memcached와 프로토콜이 호환`되므로 기존 Memcached 환경에서 사용하는 주요 도구가 ElastiCache에서 거의 수정되지 않고 작동함.
* Memcached 클러스터는 리전의 가용 영역 별로 생성 가능.
* 클러스터 내에 노드를 추가할 수록 데이터 저장 공간이 늘어남.
* 스냅샷과 Read Replica를 지원하지 않음.
* MultiThreaded architecture. 여러개

* **Redis**
* 빠른 오픈 소스 인-메모리 데이터 스토어 및 캐시.
* 다양한 데이터 형식을 제공하는 키-값(Key-Value) 데이터 저장소.
* 스냅샷과 Read Replica를 지원함.
* 마스터 노드에 장애가 발생할 경우 자동으로 Read Replica를 마스터로 승격시키는 Failover 기능 지원.
* 클러스터 구성 불가, 따라서 노드를 추가해도 전체 메모리 용량이 늘어나지 않으므로 데이터 저장 용량은 각 캐시 노드의 메모리 용량에 한함.
* 캐시 노드의 메모리 용량을 넘어서는 데이터를 저장하기 위해서는 애플리케이션 레벨에서의 샤딩 구현 필요.
* 한 리전 안의 여러 가용 영역에 생성 가능.
* Redis용 ElastiCache는 확장 가능하고 안전한 완전관리형 서비스로서 웹, 모바일 앱, 게임, 광고 기술 및 IoT와 같은 고성능 사용 사례에 지원하는 데 적합한 서비스.
* MultiThreaded architecture가 아님. 단일

ElastiCache Redis/Memcached와 같은 `In-Memory Key/Value 저장소`를 활용하여 `세션 데이터를 관리하고 저장`할 수 있습니다. <br>
세션 데이터는 `애플리케이션 계층에서 관리`되기 때문에, `분산 캐시(distribued cache)가 사용`되어야 합니다.

**DAX** <br>
DynamoDB는 일관된 단일 자릿수 밀리초 대기 시간을 제공하지만, DynamoDB + DAX는 읽기 집약적인 워크로드에 대해 초당 수백만 건의 요청에 대한 응답 시간을 마이크로초 단위로 단축하여 성능을 한 단계 높입니다 10배 정도 더 빠름. <br>
DAX를 사용하면 인기 있는 이벤트나 뉴스 스토리가 전례 없는 요청 볼륨을 원하는 방향으로 유도하는 경우에도 애플리케이션이 빠르고 신속하게 응답할 수 있습니다. 튜닝이 필요하지 않습니다.

VPC안 : Amazon EC2 인스턴스(앱 + DAX 클라이언트) - DAX Cluster -> VPC밖 : Amazon DynamoDB

A 탈락 -> Redis는 읽기 복제본을 지원하여 읽기 로드 처리는 좋으나 앱 변경점이 있어 부적합.

B 정답 -> DynamoDB를 위한 가용성이 뛰어난 완전관리형인 메모리 cache로 적합.

C 탈락 -> 글로벌 테이블은 다양한 지역에서 빠르게 접근하기 위한 것이라 부적합.

D 탈락 -> Memcached는 읽기 복제본을 지원하지 않아 읽기 로드 처리도 별로고 앱 변경점이 있어 부적합.

</div>
</details>

<hr/>

## Prob. 133

지점 사무실에서 회사는 가상화된 컴퓨팅 리소스가 없는 작은 데이터 클로짓(small data closet with no virtualized compute resource)에서 애플리케이션을 실행합니다. 애플리케이션의 데이터는 NFS(네트워크 파일 시스템) 볼륨에 저장됩니다. 규정 준수 요구 사항에 따라 NFS 볼륨의 일일 오프사이트 백업이 필요합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. 데이터를 Amazon S3에 복제하려면 온프레미스에 AWS Storage Gateway 파일 게이트웨이를 설치합니다.

B. 데이터를 Amazon S3에 복제하려면 온프레미스에 AWS Storage Gateway 파일 게이트웨이 하드웨어 장치를 설치합니다.

C. 저장된 볼륨이 있는 AWS Storage Gateway 볼륨 게이트웨이를 온프레미스에 설치하여 데이터를 Amazon S3에 복제합니다.

D. 데이터를 Amazon S3에 복제하려면 온프레미스에서 캐시된 볼륨이 있는 AWS Storage Gateway 볼륨 게이트웨이를 설치합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

NFS 볼륨의 일일 오프사이트 백업이 필요 문제 요점.

일일 오프사이트 백업 - 하루마다 자동화 백업. <br>
가상화된 컴퓨팅 리소스가 없는 작은 데이터 클로짓 - 가상화된 컴퓨터 환경?

**AWS Storage Gateway** <br>
사실상 무제한의 클라우드 스토리지에 대한 온프레미스에게 액세스 권한을 제공하는 하이브리드 클라우드 스토리지 서비스. <br>
스토리지 관리 간소화 및 비용 절감 효과 - 테이프 백업을 클라우드로 이동/클라우드 백업 파일 공유/온프레미스 스토리지를 최소화/온프레미스 애플리케이션의 AWS 데이터(클라우드)에 대한 짧은 지연 시간의 액세스 권한/다양한 마이그레이션, 아카이빙, 프로세싱, 재해 복구 사용.

로컬에서 애플리케이션은 NFS, SMB 및 iSCSI와 같은 표준 스토리지 프로토콜로 데이터를 캐싱합니다. <br>
하드웨어 게이트웨이 어플라이언스(가상 머신)를 통해 이 서비스에 연결 - [DataSync]의 `Agent`와 비슷한 역할.

AWS 스토리지 서비스에 연결하여 AWS에서 `파일, 볼륨, 스냅샷 및 가상 테이프용 스토리지를 제공`합니다. 이 서비스에는 `대역폭 관리`, `자동화된 네트워크 복원력` 및 `효율적인 데이터 전송`과 같은 고도로 **최적화된 데이터 전송 매커니즘**이 포함.

**백업 툴**로 기존의 온프레미스 환경의 데이터센터에서 백업 전용 게이트웨이를 사용. <br>
데이터센터에 Appliance를 설치하고 Storage Gateway를 통해 S3에 백업을 하고, S3에 저장된 데이터로 분석하는 등의 기능.

* **File Gateway(NFS, SMB)**
  * NFS : Network File System
    + `for Linux`
    + NFS를 제공하는 AWS 서비스 : `EFS`

  * SMB : Server Message Block
    + `for Windows`

  * `NFS, SMB 마운트 포인트로` 전송받은 `데이터를 S3에 저장`
    + 소유권, 퍼미션, 파일 생성 시간등의 `설정은 S3의 메타데이터로 저장`
    + `S3는 오브젝트 저장소`이기 때문에 `일반적인 하드웨어에서 읽는 파일과는 다르므로 NFS, SMB등을 통해 액세스 가능`

  * S3에 저장후에는 `S3의 모든 기능 활용 가능`
    + `이벤트 트리거`를 통한 다른 서비스(Lambda, Athena, 분석 서비스 등) 사용
    + 버저닝
    + 수명 주기 등등

* **Volume Gateway(iSCSI)**
  * **Stored Volume : 모든 데이터를 로컬에 저장하고 비동기적으로 AWS에 백업**
    + 1GB ~ 16TB
  
  * **Cached Volume : 자주 사용되는 데이터만 로컬에 남겨두고 나머지는 모두 AWS에 백업**
    + 1GB ~ 32TB

  * `iSCSI 프로토콜`을 통해 전달받은 `데이터를 비동기적으로 EBS 스냅샷 형식으로 저장`
    + 스냅샷은 `증분식(Incremental)` -> 이전 스냅샷에서 바뀐 부분만 저장함
    + `주로 백업 용도`로 사용함

  * **Block Storage를 위해 사용 가능**

* **Tape Gateway(VTL, Virtual Tape Library)**
  * `이미 존재하는 Tape 기반 백업` 애플리케이션을 위한 서비스
  
  * `iSCSI 디바이스로 백업`
  
  * NetBackup, Backup Exec 등등 기존의 `백업 애플리케이션 사용 가능`

A 탈락 -> AWS에 Storage Gateway 파일 게이트웨이로 파일/데이터을 전송받아 백업하는 것이라 부적합.

B 정답 -> 온프레미스에서 하드웨어 장치를 설치하여 데이터를 캐싱하고 클라우드에 Storage Gateway로 보내어 백업하여 적합.

C 탈락 -> AWS에 Storage Gateway 저장된 볼륨 게이트웨이로 모든 데이터를 로컬에 저장하고 전송받아 백업하는 것이라 부적합.

D 탈락 -> AWS에 Storage Gateway 캐시된 볼륨 게이트웨이로 자주 사용되는 데이터만 로컬에 남겨두고 전송받아 백업하는 것이라 부적합.

</div>
</details>

<hr/>

## Prob. 134

한 비즈니스에서 AWS를 사용하여 전 세계 소비자를 위한 선거 보고 웹 사이트를 호스팅하고 있습니다. 웹 사이트는 웹 및 애플리케이션 계층용 Application Load Balancer가 있는 Auto Scaling 그룹의 Amazon EC2 인스턴스를 사용합니다. 데이터베이스 계층은 MySQL용 Amazon RDS로 구동됩니다. 웹사이트는 선거 결과로 한 시간에 한 번씩 업데이트되며 이전에는 수백 명의 개인이 데이터를 확인하는 것을 보았습니다.
이 회사는 많은 국가에서 임박한 선거의 결과로 앞으로 몇 달 동안 수요가 크게 증가할 것으로 예상합니다. 솔루션 설계자의 목표는 더 많은 EC2 인스턴스에 대한 요구 사항을 제한하면서 증가하는 수요를 관리할 수 있는 웹 사이트의 용량을 늘리는 것입니다.

어떤 솔루션이 이러한 기준을 충족할까요?

A. Amazon ElastiCache 클러스터를 시작하여 일반 데이터베이스 쿼리를 캐시합니다.

B. Amazon CloudFront 웹 배포를 시작하여 일반적으로 요청되는 웹 사이트 콘텐츠를 캐시합니다.

C. EC2 인스턴스에서 디스크 기반 캐싱을 활성화하여 일반적으로 요청된 웹 사이트 콘텐츠를 캐시합니다.

D. 일반적으로 요청된 웹 사이트 콘텐츠에 대해 캐싱이 활성화된 EC2 인스턴스를 사용하여 설계에 역방향 프록시를 배포합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

EC2 인스턴스에 대한 요구 사항을 제한하면서 증가하는 수요를 관리할 수 있는 웹 사이트의 용량 문제 요점.

**역방향 프록시** <br>
역방향 프록시는 웹 서버 앞에 위치하여 클라이언트(예:웹 브라우저) 요청을 해당 웹 서버에 전달합니다.역방향 프록시는 일반적으로 보안, 성능, 안정성을 향상하기 위해 구현.

사용자 디바이스 -> 인터넷 -> 역방향 프록시 -> 서버 <br>
부하 분산/전역 서버 부하 분산. <br>
공격으로부터 보호. <br>
캐싱/SSL 암호화.

프록시, 프록시 서버, 웹 프록시라고도 하는 정방향 프록시는 클라이언트 시스템 그룹 앞에 위치하는 서버입니다. 이러한 컴퓨터가 인터넷의 사이트 및 서비스에 요청하면 프록시 서버가 이러한 요청을 가로채고 중개자처럼 해당 클라이언트를 대신하여 웹 서버와 통신.

사용자 디바이스 -> 정방향 프록시 -> 인터넷 -> 서버 <br>
주 당국 또는 기관의 검색 제한을 피하기 위해. <br>
특정 콘텐츠에 대한 액세스를 차단하려면. <br>
온라인에서 자신의 신원을 보호하기 위해.

전세계 대상 = CloudFront <br>
EC2에 대한 요구사항 제한 -> ElastiCache 탈락

A 탈락 -> RDS는 EC2안에 있어 요구사항 제한으로 부적합.

B 정답 -> 전세계에 엣지 로케이션에 캐싱하며 개인 데이터마다 처리하여 적합.

C 탈락 -> EC2안에 있어 요구사항 제한으로 부적합.

D 탈락 -> 관리한는 것보단 보호/분산하는 것이라 부적합.

</div>
</details>

<hr/>

## Prob. 135 유념

Amazon S3는 기업에서 날씨 기록을 저장하는 데 사용됩니다. 기록은 회사 웹사이트의 도메인 이름을 참조하는 URL을 통해 액세스됩니다. 구독을 통해 전 세계 사용자가 이 자료에 액세스할 수 있습니다. 조직의 핵심 도메인 이름은 타사 운영자가 호스팅하지만 이 회사는 최근 일부 서비스를 Amazon Route 53으로 이전했습니다. 회사는 계약을 통합하고, 사용자 지연 시간을 최소화하고, 구독자에게 애플리케이션을 제공하는 비용을 낮추기를 원합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. Amazon CloudFront에서 웹 배포를 생성하여 애플리케이션의 S3 콘텐츠를 제공합니다. CloudFront 배포를 가리키는 Route 53 호스트 영역에 CNAME 레코드를 생성하여 응용 프로그램의 URL 도메인 이름을 확인합니다.

B. Amazon CloudFront에서 웹 배포를 생성하여 애플리케이션의 S3 콘텐츠를 제공합니다. Amazon Route 53 호스트 영역에 CloudFront 배포를 가리키는 ALIAS 레코드를 생성하여 애플리케이션의 URL 도메인 이름을 확인합니다.

C. 응용 프로그램에 대한 Route 53 호스트 영역에 A 레코드를 만듭니다. 웹 응용 프로그램에 대한 Route 53 트래픽 정책을 생성하고 지리적 위치 규칙을 구성합니다. 엔드포인트의 상태를 확인하고 엔드포인트가 비정상인 경우 DNS 쿼리를 다른 엔드포인트로 라우팅하도록 상태 검사를 구성합니다.

D. 응용 프로그램에 대한 Route 53 호스트 영역에 A 레코드를 만듭니다. 웹 응용 프로그램에 대한 Route 53 트래픽 정책을 생성하고 지리적 근접성 규칙을 구성합니다. 엔드포인트의 상태를 확인하고 엔드포인트가 비정상인 경우 DNS 쿼리를 다른 엔드포인트로 라우팅하도록 상태 검사를 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

전 세계 사용자 지연 시간을 최소화하고, 도메인 이름을 참조하는 URL을 통해 액세스 문제 요점.

**Route 53** <br>
최종 사용자를 인터넷 애플리케이션으로 라우팅하는 안정적이고 비용 효율적인 방법으로 가용성과 확장성이 뛰어난 도메인 이름 시스템(DNS) 웹 서비스입니다. Route 53는 사용자 요청을 AWS 또는 온프레미스에서 실행되는 인터넷 애플리케이션에 연결.

**A 레코드**는 도메인을 `특정 IP로 연결`함.

캐노니컬 네임 레코드, 줄여서 **CNAME 레코드**는 하나의 도메인 네임을 `다른 이름으로 매핑시키는 도메인 네임 시스템`의 리소스 레코드의 일종이다. 하나의 IP 주소로부터 여러 개의 서비스를 실행할 때 편리함을 입증.

**별칭 레코드**는 DNS 기능에 대한 Route 53 전용 확장을 제공. <br>
별칭 레코드 트래픽을 CloudFront 배포 및 Amazon S3 버킷과 같은 선택한 `AWS 리소스로 라우팅`할 수 있음. <br>
호스팅 영역의 한 레코드에서 다른 레코드로 트래픽을 라우팅할 수 있음.

CNAME은 실제 DNS 서버를 위한 것입니다. <br>
ALIAS는 DNS이지만 특히 AWS용입니다. AWS용 특수 레코드입니다.

A 탈락 -> CNAME 레코드는 A 레코드 도메인을 다른 이름의 도메인으로 부르는 것이고 서버에 접근 하는 것이라 부적합.

B 정답 -> 별칭 레코드는 AWS 특수이며 AWS 리소스에 접근 가능하여 적합.

C, D 탈락 -> A 레코드는 도메인으로 IP에 접근 하는 것으로 트래픽 정책이나 지리적 위치/근접성 규칙과 상관없어 부적합.

</div>
</details>

<hr/>

## Prob. 136

기업은 인터넷을 통해 액세스할 수 있는 웹 응용 프로그램을 개발 중입니다. 애플리케이션은 Amazon RDS MySQL 다중 AZ DB 인스턴스를 활용하여 민감한 사용자 데이터를 저장하는 Linux 인스턴스용 Amazon EC2에서 호스팅됩니다. 퍼블릭 서브넷은 EC2 인스턴스에 사용되는 반면 프라이빗 서브넷은 RDS DB 인스턴스에 사용됩니다. 보안 팀은 데이터베이스 인스턴스에 대한 웹 기반 공격을 방지할 것을 요구했습니다.

솔루션 설계자는 어떤 권장 사항을 제시해야 합니까?

A. EC2 인스턴스가 자동 확장 그룹에 속해 있고 애플리케이션 로드 밸런서 뒤에 있는지 확인합니다. 의심스러운 웹 트래픽을 삭제하도록 EC2 인스턴스 iptables 규칙을 구성합니다. DB 인스턴스에 대한 Security Group을 생성합니다. 개별 EC2 인스턴스의 포트 3306 인바운드만 허용하도록 RDS 보안 그룹을 구성합니다.

B. EC2 인스턴스가 자동 확장 그룹에 속해 있고 애플리케이션 로드 밸런서 뒤에 있는지 확인합니다. DB 인스턴스를 EC2 인스턴스와 동일한 서브넷으로 이동합니다. DB 인스턴스에 대한 Security Group을 생성합니다. 개별 EC2 인스턴스의 포트 3306 인바운드만 허용하도록 RDS 보안 그룹을 구성합니다.

C. EC2 인스턴스가 자동 확장 그룹에 속해 있고 애플리케이션 로드 밸런서 뒤에 있는지 확인합니다. AWS WAF를 사용하여 인바운드 웹 트래픽에서 위협을 모니터링합니다. 웹 응용 프로그램 서버에 대한 Security Group과 DB 인스턴스에 대한 Security Group을 생성합니다. 웹 응용 프로그램 서버 보안 그룹에서 포트 3306 인바운드만 허용하도록 RDS 보안 그룹을 구성합니다.

D. EC2 인스턴스가 자동 확장 그룹에 속해 있고 애플리케이션 로드 밸런서 뒤에 있는지 확인합니다. AWS WAF를 사용하여 인바운드 웹 트래픽에서 위협을 모니터링합니다. 트래픽이 많은 경우 새 DB 인스턴스를 자동으로 생성하도록 자동 확장 그룹을 구성합니다. RDS DB 인스턴스에 대한 Security Group을 생성합니다. 포트 3306 인바운드만 허용하도록 RDS 보안 그룹을 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

데이터베이스 인스턴스에 대한 웹 기반 공격을 방지 문제 요점.

A 탈락 -> iptables를 사용하여 의심스러운 웹 트래픽을 "폐기"하는 방법으로 IP 주소를 지정해야 해서 부적합.

B 탈락 -> "DB 인스턴스를 EC2 인스턴스가 위치한 동일한 서브넷으로 이동"은 모든 것이 공용 서브넷에 있으며 이는 "중요한 사용자 데이터" 스토리지 원칙을 위반하여 부적합.

C 정답 -> 웹 앱 방화벽으로 1차로 트래픽 위협과 모니터링하여 보호하며 2차로 보안 그룹으로 IP와 TCP/UDP를 보호하여 적합.

D 탈락 -> "포트 3306 인바운드 허용(MySQL 전용 포트)"이 어느 리소스(EC2)에서 지정되지 않았으므로 부적합.

</div>
</details>

<hr/>

## Prob. 137

솔루션 설계자는 온프레미스에서 AWS로 영구 데이터베이스를 마이그레이션하기 위한 솔루션 설계를 담당합니다. 데이터베이스 관리자에 따르면 데이터베이스에는 64,000 IOPS가 필요합니다. 가능한 경우 데이터베이스 관리자는 단일 Amazon Elastic Block Store(Amazon EBS) 볼륨에서 데이터베이스 인스턴스를 호스팅하려고 합니다.

데이터베이스 관리자의 요구 사항을 가장 효과적으로 충족시키는 옵션은 무엇입니까?

A. I3 I/O 최적화 제품군의 인스턴스를 사용하고 로컬 사용 후 삭제 스토리지를 활용하여 IOPS 요구 사항을 충족합니다.

B. Amazon EBS(Elastic Block Store) Provisioned IOPS SSD(io1) 볼륨이 연결된 Nitro 기반 Amazon EC2 인스턴스를 생성합니다. 64,000 IOPS가 되도록 볼륨을 구성합니다.

C. Amazon EFS(Elastic File System) 볼륨을 생성하여 데이터베이스 인스턴스에 매핑하고 이 볼륨을 사용하여 데이터베이스에 필요한 IOPS를 달성합니다.

D. 두 볼륨을 프로비저닝하고 각각 32,000 IOPS를 할당합니다. 운영 체제 수준에서 논리적 볼륨을 생성하여 두 볼륨을 모두 집계하여 IOPS 요구 사항을 충족합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

IOPS와 EBS 볼륨에서 데이터베이스 인스턴스를 호스팅 문제 요점.

프로비저닝된 IOPS SSD 볼륨은 한 볼륨당 최대 64,000 IOPS 및 1,000MB/s의 처리량을 제공하도록 설계되었습니다.

EBS io1은 기본 32000 IOPS, Nitro 기반일 경우에만 64000 IOPS를 제공한다고 한다.

A 탈락 -> i3 인텔코어 I/O 최적화한다는데 볼륨에 대한 것이 없어 부적합.

B 정답 -> EBS기반의 프로비저닝된 볼륨으로 적합.

C 탈락 -> EFS 볼륨으로 부적합.

D 탈락 -> 두 볼륨으로 나누어 처리하는 것 같은데 명확한 답이 있어서 부적합.

</div>
</details>

<hr/>

## Prob. 138

솔루션 아키텍트는 AWS 클라우드에 배포할 새 애플리케이션에 대한 아키텍처를 생성하는 책임이 있습니다. Amazon EC2 온디맨드 인스턴스는 애플리케이션을 실행하는 데 사용되며 다른 가용 영역에서 자동으로 확장됩니다. 하루 종일 EC2 인스턴스는 주기적으로 확장 및 축소됩니다. 부하 분산은 ALB(Application Load Balancer)에서 처리합니다. 아키텍처는 분산된 세션 데이터를 관리할 수 있어야 합니다. 회사는 코드에 필요한 조정을 할 준비가 되어 있습니다.

설계에서 분산 세션 데이터 관리가 가능하도록 하는 솔루션 설계자의 책임은 무엇입니까?

A. Amazon ElastiCache를 사용하여 세션 데이터를 관리하고 저장합니다.

B. ALB의 세션 선호도(스틱 세션)를 사용하여 세션 데이터를 관리합니다.

C. AWS Systems Manager의 Session Manager를 사용하여 세션을 관리합니다.

D. GetSession을 사용합니다.AWS Security Token Service(AWS STS)에서 토큰 API 작업을 수행하여 세션을 관리합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

분산 세션 데이터 관리 문제 요점.

132문제에 ElastiCache 대한 설명이 있음.

**Distributed Session Management** <br>
주소 확장성을 해결하고 개별 웹 서버에서 액세스할 수 있는 세션에 대한 공유 데이터 저장소를 제공하기 위해 웹 서버 자체에서 HTTP 세션을 추상화할 수 있습니다. <br>
이를 위한 일반적인 솔루션은 Redis 및 Memcached와 같은 In-Memory Key/Value 저장소를 활용하는 것입니다.

A 정답 -> 세션 데이터는 애플리케이션 계층에서 관리되며 분산 캐시를 사용해야 적합.

B 탈락 -> 이는 개별 EC2 인스턴스를 세션 데이터에 밀접하게 결합하며 ALB에 추가 논리가 필요하다. 스케일 인이 발생하면 개별 EC2 인스턴스에 저장된 세션 데이터가 삭제하여 부적합.

C 탈락 -> 세션 관리자는 EC2 인스턴스 및 운영 중인 기타 장치, 서버 및 VM을 관리하기에 세션 정보를 저장하지 않아 부적합. <br>
[링크](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html)https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html

D 탈락 -> STS는 세션과 다른 개념으로 IAM 사용자에 대한 임시 자격 증명을 요청하여 부적합. <br>
[링크](https://docs.aws.amazon.com/STS/latest/APIReference/welcome.html)https://docs.aws.amazon.com/STS/latest/APIReference/welcome.html

</div>
</details>

<hr/>

## Prob. 139

여러 Amazon EC2 Linux 인스턴스는 계층적 디렉터리 구조가 필요한 애플리케이션을 실행하기 위해 VPC의 비즈니스에서 사용됩니다. 앱은 빠르고 동시에 공유 저장소에 액세스하고 쓸 수 있어야 합니다.

이것은 어떻게 이루어지나요?

A. Amazon EFS(Elastic File System) 파일 시스템을 만들고 각 EC2 인스턴스에서 마운트합니다.

B. Amazon S3 버킷을 생성하고 VPC의 모든 EC2 인스턴스에서 액세스를 허용합니다.

C. Amazon EBS(Amazon Elastic Block Store) Provisioned IOPS SSD(io1) 볼륨에 파일 시스템을 생성합니다. 볼륨을 모든 EC2 인스턴스에 연결합니다.

D. 각 EC2 인스턴스에 연결된 Amazon EBS(Amazon Elastic Block Store) 볼륨에 파일 시스템을 생성합니다. 여러 EC2 인스턴스에서 Amazon EBS(Amazon Elastic Block Store) 볼륨을 동기화합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

계층적 디렉터리 구조와 동시에 공유 저장소에 액세스 문제 요점.

S3와 EBS는 계층적 디렉토리 구조가 아님. <br>
S3는 버킷 내의 객체 구조. <br>
EBS는 Block-based 구조.

S3는 어디서나 원하는 양의 데이터를 저장하고 검색할 수 있도록 구축된 객체. <br>
내구성, 유연성, 가용성, 성능, 보안 및 거의 무제한의 확장성.

EFS는 동시성을 지원하며, Multi-attach EBS도 지원하긴 하지만 EFS는 Multi-AZ를 대상으로도 지원하는 반면 EBS는 단일 AZ를 대상으로만 지원. <br>
Multi-AZ은 장애 극복과 읽기 로드 처리 향상.

EFS는 1000명 이상의 클라이언트로부터 동시성을 지원하지만, EBS는 16정도이다.

A 정답 -> EFS는 계층적 디렉터리(상위/하위) 구조와 동시에 공유에 적합.

B 탈락 -> S3는 구조도 다르며 동시성이 없어 부적합.

C, D 탈락 -> EBS는 블록 구조이며 동시성에 제한이 있어 부적합.

</div>
</details>

<hr/>

## Prob. 140 유념

솔루션 설계자가 문서 관리 작업을 Amazon Web Services로 이전하는 중입니다. 워크로드는 공유 스토리지 파일 시스템 및 외부 데이터베이스에 7테라바이트의 계약 문서를 저장하고 추적합니다. 대부분의 기록은 보관되고 궁극적으로 나중에 참조할 수 있도록 복구됩니다. 마이그레이션 중에는 애플리케이션을 업데이트할 수 없으며 스토리지 솔루션은 고가용성이어야 합니다.
Amazon EC2의 Auto Scaling 그룹에 속한 웹 서버는 문서를 수집하고 저장합니다.(Web servers that are part of an Auto Scaling group on Amazon EC2 collect and store documents) Auto Scaling 그룹에는 최대 12개의 인스턴스가 있을 수 있습니다.

비용 효율성 측면에서 이러한 기준에 가장 적합한 옵션은 무엇입니까?

A. 공유 NFS 스토리지 시스템으로 작동하도록 네트워킹에 최적화된 향상된 EC2 인스턴스를 프로비저닝합니다.

B. S3 Standard-Infrequent Access(S3 Standard-IA) 스토리지 클래스를 사용하는 Amazon S3 버킷을 생성합니다. S3 버킷을 자동 스케일링 그룹의 EC2 인스턴스에 마운트합니다.

C. AWS Transfer for SFTP 및 Amazon S3 버킷을 사용하여 SFTP 서버 엔드포인트를 생성합니다. SFTP 서버에 연결하도록 자동 스케일링 그룹의 EC2 인스턴스를 구성합니다.

D. EFS Standard-Infrequent Access(EFS Standard-IA) 스토리지 클래스를 사용하는 Amazon EFS(Amazon Elastic File System) 파일 시스템을 만듭니다. 파일 시스템을 자동 스케일링 그룹의 EC2 인스턴스에 마운트합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

비용 효율성 문제 요점.

공유 스토리지 파일 시스템 및 외부 데이터베이스. <br>
궁극적으로 나중에 참조.

"Must be highly available" tells you need EFS across

    비즈니스 애플리케이션을 위한 많은 보고 시스템은 비즈니스 기능을 지원하기 위해 액세스 가능한 공유 파일 스토리지에 의존합니다. EFS Standard-IA 및 EFS OneZone-IA 스토리지 클래스를 사용하면 공유 파일 시스템에서 파일을 쉽고 경제적으로 저장하고 액세스할 수 있으므로 비용을 제어하기 위해 데이터를 관리할 필요가 없습니다. 나중에 보고서에 액세스하는 경우 EFS Intelligent-Tiering은 파일 시스템이 standard 또는 OneZone 스토리지 클래스를 사용하는지에 따라 액세스한 보고서를 EFS standard 또는 OneZone 원존 스토리지 클래스로 자동으로 이동할 수 있습니다.

나중에 참조하는 데이터가 많을 경우, Standard-IA 클래스를 사용해야함. <br>
공유 스토리지 파일 시스템은 EFS, EBS

**공유 NFS 스토리지** <br>
기기에 파일을 업로드하고 다른 위치로 이동하거나 기기를AWS 클라우드 반납할 때 사용하거나AWS OpsHub 파일을 전송하는AWS DataSync 데 사용.

Snow Family 디바이스를 NFS 파일 시스템으로 구성하고 네이티브 파일 시스템을 사용하여 디바이스의 파일을 관리할 수 있습니다. 온-프레미스 위치에서 디바이스로 파일을 업로드한 다음 파일을 다른 위치로AWS 전송하거나 다른 위치로 이동할 수 있습니다. AWS OpsHub 기본값을 사용하여 자동으로 NFS를 구성하거나 수동으로 직접 NFS를 구성.

**AWS Transfer for SFTP** <br>
AWS Transfer Family는 SFTP, FTPS, FTP 및 AS2 프로토콜을 사용하여 AWS 스토리지 서비스로의 반복적인 B2B 파일 전송을 안전하게 조정합니다. <br>
완전 관리형의 고가용성 SFTP 서비스. <br>
서버를 생성하고, 사용자 계정을 설정하고, 서버를 하나 이상의 S3 버킷에 연결하기만 하면 사용자 자격 증명, 권한 및 키를 세부적으로 제어 또한 IAM 정책을 사용하여 각 사용자에게 부여되는 액세스 레벨을 제어. <br>
기존 DNS 이름과 SSH 퍼블릭 키를 사용해 Transfer for SFTP로 손쉽게 마이그레이션 가능. <br>
SFTP 안에서 사용자를 생성하거나 기존 자격 증명 공급자를 사용. <br>
SFTP(Secure File Transfer Protocol)는 오랫동안 많은기업에서 데이터 처리 및 파트너 통합 워크플로에 사용되고 있습니다. 이러한 시스템은 "레거시"로 무시되기 쉽지만 실상은 유용한 용도로 사용되고 있으며 당분간은 계속해서 사용될 것입니다. AWS는 원활하고 중단 없는 방식으로 이러한 워크플로를 클라우드로 이동할 수 있는 기능을 제공.

A 탈락 -> 공유 NFS 스토리지로 동시성은 제어하는 것 같으나 데이터를 만족 못하여 부적합.

B 탈락 -> Standard-IA로 데이터 참조하지만 S3로는 동시성 만족 못하여 부적합.

C 탈락 -> 보안 관련이라 부적합.

D 정답 -> EFS로 동시성 지원하고 Standard-IA로 데이터 참조하여 적합.

</div>
</details>

<hr/>

* Ref
  - [ExamTopics](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate-saa-c02/view/14)