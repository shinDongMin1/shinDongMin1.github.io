---
layout: post
title: "[AWS-SAA] Examtopics 261~270"
subtitle: AWS
date: '2023-03-30 00:00:01 +0900'
category: study
tags: aws aws-saa
image:
  path: /assets/img/study_AWS/saa-co2_logo.png
---

SAA Examtopics 261~270번 문제를 풀어보자.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## Prob. 261

비즈니스는 매일 데이터를 처리합니다. 프로세스의 출력은 Amazon S3 버킷에 보관되어 일주일 동안 매일 검사한 다음 임시 검사(adhoc)를 위해 즉시 사용할 수 있어야 합니다.

기존 구성에 대한 가장 비용 효율적인 대안은 무엇입니까?

A. 30일 후에 개체를 삭제하도록 수명 주기 정책을 구성합니다.

B. 수명 주기 정책을 구성하여 30일 후에 개체를 Amazon S3 Glacier로 전환합니다.

C. 수명 주기 정책을 구성하여 30일 후에 개체를 Amazon S3 Standard-Infrequent Access(S3 Standard-IA)로 전환합니다.

D. 30일 후 개체를 Amazon S3 One Zone-Infrequent Access(S3 One Zone-IA)로 전환하는 수명 주기 정책을 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

기존 구성에 대한 가장 비용 효율적인 대안 문제 요점.

adhoc = 검사를 위해서 <br>
Standard iA와 One Zone IA에서 갈리는데 가장 비용 효율적인 것은 원 존임.

A 탈락 -> 삭제가 되면 임시 검사를 못하여 부적합.

B 탈락 -> 글래시어는 보관용으로 임시 검사가 진행되기에 부적합.

C 탈락 -> 스탠다드도 괜찮은 대안이지만 가격은 DR를 위해 3개의 영역에 복제본이 있어서 상대적으로 비싸기에 부적합.

D 정답 -> 원 존은 단일 스토리지에 저장되어 DR은 떨어지나 싸서 적합.

</div>
</details>

<hr/>

## Prob. 262

비즈니스에서 애플리케이션을 개발 중입니다. 이 프로그램은 Amazon API Gateway를 통해 데이터를 수신하고 AWS Lambda 함수를 사용하여 Amazon Aurora PostgreSQL 데이터베이스에 저장합니다.
개념 증명 단계에서 회사는 데이터베이스에 로드해야 하는 많은 양의 데이터를 관리하기 위해 Lambda 할당량을 대폭 늘려야 합니다. 솔루션 설계자는 확장성을 최대화하고 설정 노력을 줄이는 새로운 설계에 대한 권장 사항을 제공해야 합니다.

어떤 솔루션이 이러한 기준을 충족할까요?

A. 람다 함수 코드를 Amazon EC2 인스턴스에서 실행되는 Apache Tomcat 코드로 리팩터링합니다. 기본 Java 데이터베이스 연결(JDBC) 드라이버를 사용하여 데이터베이스를 연결합니다.

B. 플랫폼을 Aurora에서 Amazon DynamoDB로 변경합니다. DAX(DynamoDB Accelerator) 클러스터를 프로비저닝합니다. DAX 클라이언트 SDK를 사용하여 DAX 클러스터에서 기존 DynamoDB API 호출을 가리킵니다.

C. 두 개의 람다 기능을 설정합니다. 정보를 수신하도록 하나의 기능을 구성합니다. 데이터베이스에 정보를 로드하도록 다른 함수를 구성합니다. Amazon Simple Notification Service(Amazon SNS)를 사용하여 람다 함수를 통합합니다.

D. 두 개의 람다 기능을 설정합니다. 정보를 수신하도록 하나의 기능을 구성합니다. 데이터베이스에 정보를 로드하도록 다른 함수를 구성합니다. Amazon Simple Queue Service(Amazon SQS) 큐를 사용하여 람다 함수를 통합합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

확장성을 최대화하고 설정 노력을 줄이는 새로운 설계 문제 요점.

클라이언트 -> API Gateway -> Lambda 함수 -> Aurora PostgreSQL. <br>
Lambda 할당량을 대폭 늘림. <br>
SQS = scalability(확장성)/데이터 캡쳐/장애 극복.

A 탈락 -> Lambda 함수 -> EC2(JDBC) -> DB로 연결하기로 리팩터링(재설계)해도 결국 람다의 양이 늘어난 것이라서 확장성/설정에 대한 노력만 들어서 부적합.

B 탈락 -> DB를 변경 RDS -> NoSQL로 코드 변경이 있으며 DAX는 메모리를 사용하여 읽기 로드 처리에 대한 것으로 부적합.

C 탈락 -> Lambda 함수에 대한 기능만 더 추가하며 SNS알림만으로는 부적합.

D 정답 -> 람다 -> SQS -> DB를 적용하여 SQS대기열에서 람다에 대한 부하를 보관하고 연결만하면 확장성있게 변경되어 적합.

</div>
</details>

<hr/>

## Prob. 263

기업에서 온프레미스 MySQL 데이터베이스를 Amazon Web Services(AWS)로 마이그레이션하려고 합니다. 클라이언트 대면 애플리케이션에서 정기적으로 가져오면 데이터베이스에서 엄청난 양의 쓰기 작업이 발생합니다. 조직은 트래픽 양이 애플리케이션의 성능에 영향을 미칠 수 있다고 우려하고 있습니다.

솔루션 설계자는 AWS 아키텍처 설계에 어떻게 접근해야 합니까?

A. 프로비저닝된 IOPS SSD 스토리지를 사용하여 MySQL DB 인스턴스용 Amazon RDS를 프로비저닝합니다. Amazon CloudWatch를 사용하여 쓰기 작업 메트릭을 모니터링합니다. 필요한 경우 프로비저닝된 IOPS를 조정합니다.

B. General Purpose SSD 스토리지를 사용하여 MySQL DB 인스턴스용 Amazon RDS를 프로비저닝합니다. Amazon ElastiCache 클러스터를 DB 인스턴스 앞에 배치합니다. 대신 ElastiCache를 쿼리하도록 애플리케이션을 구성합니다.

C. 메모리에 최적화된 인스턴스 유형을 사용하여 Amazon DocumentDB(MongoDB 호환성 포함) 인스턴스를 프로비저닝합니다. Amazon CloudWatch에서 성능 관련 문제를 모니터링합니다. 필요한 경우 인스턴스 클래스를 변경합니다.

D. 범용 성능 모드에서 Amazon EFS(Amazon Elastic File System) 파일 시스템을 프로비저닝합니다. Amazon CloudWatch의 IOPS 병목 현상 모니터링. 필요한 경우 프로비저닝된 처리량 성능 모드로 변경합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

트래픽 양이 애플리케이션의 성능에 영향 문제 요점.

온프레미스 MySQL 데이터베이스를 Amazon Web Services(AWS)로 마이그레이션. <br>
엄청난 양의 쓰기 작업이 발생.

엄청난 양의 처리가 필요하므로 Provisioned IOPS SSD가 가장 적절할것.

A 정답 -> 미리 준비된 입출력 처리량을 갖는 SSD 스토리지로 DB 성능을 올리고  CloudWatch로 메트릭 단위로 모니터링하여 조정하여 적합.

B 탈락 -> 범용 SSD 스토리지를 배치하는데 또 ElastiCache는 인-메모리여서 디스크 대신 사용하여 부적합.

C 탈락 -> MySQL인데 MongoDB기반의 DocumentDB를 사용하면 코드 변화가 생길 수도 있으며 CloudWatch로 성능에 대한 것들을 모니터링하여 클래스 자체를 변경하여 부적합.

D 탈락 -> EFS 파일 시스템으로 동시성/확장성을 갖는데 CloudWatch로 IOPS 병목 현상 모니터링하여 문제가 생길 경우 그제야 프로비저닝하여 부적합.

</div>
</details>

<hr/>

## Prob. 264

한 회사에서 AWS를 사용하여 인스턴스 간에 짧은 지연 시간이 필요한 다중 인스턴스 애플리케이션을 만들고 있습니다.

솔루션 설계자는 어떤 권장 사항을 제시해야 합니까?

A. 자동 스케일링 그룹을 클러스터 배치 그룹과 함께 사용합니다.

B. 동일한 AWS 영역에 단일 가용성 영역이 있는 자동 스케일링 그룹을 사용합니다.

C. 동일한 AWS 영역에 여러 가용성 영역이 있는 자동 스케일링 그룹을 사용합니다.

D. 여러 Amazon EC2 전용 호스트가 있는 네트워크 로드 밸런서를 대상으로 사용합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

인스턴스 간에 짧은 지연 시간이 필요한 다중 인스턴스 문제 요점.

Cluster group은 지연 시간을 줄일 수 있다.

**Elastic Load Balancing** <br>
둘 이상의 가용 영역에서 EC2 인스턴스, 컨테이너, IP 주소 등 여러 대상에 걸쳐 수신되는 트래픽을 자동으로 분산. <br>
등록된 대상의 상태를 모니터링하면서 상태가 양호한 대상으로만 트래픽을 라우팅. <br>
수신 트래픽이 시간이 지남에 따라 변경됨에 따라 로드 밸런서를 확장.

**Network Load Balancer** <br>
로드 밸런서는 클라이언트에 대한 단일 접점 역할을 수행합니다. 로드 밸런서는 수신 트래픽을 Amazon EC2 인스턴스와 같은 여러 대상에 분산합니다. 이렇게 하면 애플리케이션의 가용성이 향상됩니다. 로드 밸런서에 하나 이상의 리스너를 추가 가능.

리스너는 사용자가 구성한 프로토콜과 포트를 사용하여 클라이언트의 연결 요청을 확인하고, 요청을 대상 그룹으로 전달.

각 대상 그룹은 지정한 TCP 프로토콜과 포트 번호를 사용하여 EC2 인스턴스 같은 하나 이상의 등록된 대상으로 요청을 라우팅. <br>
여러 대상 그룹에 대상을 등록할 수 있습니다. 대상 그룹 기준으로 상태 확인을 구성. <br>
대상에서 상태 검사가 수행.

A 정답 -> 다증 인스턴스를 하나의 클러스터/자동 스케일링 그룹으로 묶어 논리적으로 연결되어 지연 시간에 영향을 주어 적합.

B 탈락 -> 단일 가용성 영역을 자동 스케일링 그룹으로 묶어도 용량에 대해 영향을 받지만 서로간 지연 시간은 관련 없어 부적합.

C 탈락 -> 여러 가용성 영역을 자동 스케일링 그룹으로 묶어도 용량에 대해 영향을 받지만 서로간 지연 시간은 관련 없어 부적합.

D 탈락 -> NLB는 클라이언트와 EC2간에 요청을 분산하는 것으로 서로 인스턴스 간 성능이 아니라 부적합.

</div>
</details>

<hr/>

## Prob. 265

지난 15년 동안 기업은 온프레미스 데이터 센터에서 Oracle 관계형 데이터베이스를 사용하여 웹 애플리케이션을 운영해 왔습니다. 회사의 데이터베이스를 AWS로 마이그레이션해야 합니다. 기업은 애플리케이션의 코드를 수정하지 않고 운영 비용을 절감하기를 원합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. AWS DMS(AWS DMS)를 사용하여 데이터베이스 서버를 Amazon RDS로 마이그레이션합니다.

B. Amazon EC2 인스턴스를 사용하여 데이터베이스 서버를 마이그레이션하고 운영합니다.

C. AWS DMS(데이터베이스 마이그레이션 서비스)를 사용하여 데이터베이스 서버를 Amazon DynamoDB로 마이그레이션합니다.

D. AWS Snowball Edge Storage Optimized 디바이스를 사용하여 Oracle에서 Amazon Aurora로 데이터를 마이그레이션합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

코드를 수정하지 않고 운영 비용을 절감 문제 요점.

온프레미스 데이터 센터에서 Oracle 관계형 데이터베이스를 사용하여 웹 애플리케이션을 운영. <br>
데이터베이스를 AWS로 마이그레이션.

A 정답 -> 데이터베이스 마이그레이션에 DMS를 사용할 수 있습니다(데이터베이스 간 마이그레이션도 지원) 그리고 RDS는 MySQL, PostgreSQL, 마이크로소프트 SQL 서버, 오라클를 지원하여 적합.

B 탈락 -> 마이그레이션에 대해 말하지 않고 EC2에 설치하는 것으로 부적합.

C 탈락 -> Dynamo DB는 NoSQL 데이터베이스이므로 코드를 완전히 변경해야 해서 부적합.

D 탈락 -> Snowball은 주로 S3로 데이터를 이동하는 것으며 Aurora는 MySQL, Postgre만을 지원하지 Oracle는 아니라 부적합.

</div>
</details>

<hr/>

## Prob. 266

개발 팀은 구성 파일에 Amazon RDS MySQL DB 인스턴스의 사용자 이름과 암호를 보관합니다. 구성 파일은 팀의 Amazon EC2 인스턴스 루트 디바이스 디스크에 일반 텍스트로 저장됩니다. 팀의 응용 프로그램이 데이터베이스에 연결해야 하는 경우 파일을 읽고 자격 증명이 코드에 로드됩니다. 팀은 프로그램만 해당 내용에 액세스할 수 있도록 구성 파일의 권한을 조정했습니다. 솔루션 설계자의 주요 책임은 더 나은 보안 시스템을 구축하는 것입니다.

이 요구 사항을 충족하기 위해 솔루션 설계자는 어떤 조치를 취해야 합니까?

A. 구성 파일을 Amazon S3에 저장합니다. 응용 프로그램에서 구성 파일을 읽을 수 있는 액세스 권한을 부여합니다.

B. 데이터베이스에 액세스할 수 있는 권한을 가진 IAM 역할을 만듭니다. 이 IAM 역할을 EC2 인스턴스에 연결합니다.

C. 데이터베이스 인스턴스에서 SSL 연결을 사용합니다. 로그인할 때 SSL을 요구하도록 데이터베이스 사용자를 변경합니다.

D. 구성 파일을 EC2 인스턴스 저장소로 이동하고 인스턴스의 AMI(Amazon 시스템 이미지)를 생성합니다. 이 AMI에서 새 인스턴스를 시작합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

더 나은 보안 시스템을 구축 문제 요점.

구성 파일에 Amazon RDS MySQL DB 인스턴스의 사용자 이름과 암호를 보관. <br>
Amazon EC2 인스턴스 루트 디바이스 디스크에 일반 텍스트로 저장. <br>
응용 프로그램 -> 구성 파일(자격 증명) -> 데이터베이스로 연결.

대체로 이런 문제들은 `IAM Role`이 정답이다.

A 탈락 -> EC2 루트 디바이스 디스크에서 S3로 옮기면 인터넷으로 접근하여 부적합.

B 정답 -> EC2의 경우 IAM 역할은 RDS를 연결하는 안전한 방법으로 적합.

C 탈락 -> SSL(시큐어 소켓 레이어)로 전송 암호화하여도 결국 EC2에서 파일을 읽는 것이라 부적합.

D 탈락 -> AMI는 컨테이너화로 시스템 구성을 하나의 이미지로 만들어서 재사용하는 것이라 부적합.

</div>
</details>

<hr/>

## Prob. 267

비즈니스 애플리케이션이 VPC 내부에 포함된 Amazon EC2 인스턴스에서 작동하고 있습니다. 항목을 저장하고 검색하려면 앱 중 하나가 Amazon S3 API에 요청해야 합니다. 회사의 보안 규정은 프로그램이 인터넷에 연결된 트래픽을 보내는 것을 금지합니다.

보안을 유지하면서 이러한 요구를 충족할 조치는 무엇입니까?

A. S3 인터페이스 엔드포인트을 구성합니다.

B. S3 게이트웨이 엔드포인트을 구성합니다.

C. 개인 서브넷에 S3 버킷을 만듭니다.

D. EC2 인스턴스와 동일한 영역에 S3 버킷을 생성합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

인터넷에 연결된 트래픽을 보내는 것을 금지 문제 요점.

VPC 내부에 포함된 Amazon EC2 인스턴스에서 작동. <br>
저장하고 검색하려면 앱 중 하나가 Amazon S3 API에 요청.

인스턴스 -> 인터페이스 엔드포인트 -> PrivateLink -> AWS 서비스 -> 인스턴스. <br>
AWS 서비스가 DynamoDB 또는 S3인 경우 게이트웨이 엔드포인트을 사용합니다.<br>
다른 모든 작업에는 인터페이스 엔드포인트을 사용합니다.

A 탈락 -> 인터페이스 엔드포인트는 서로 다른 VPC간에 인스턴스끼리 프라이빗링크로 연결하는 것이라 부적합.

B 정답 -> 게이트웨이 엔드포인트로 VPC에서 외부 서비스에 대해 인터넷 회선 대신 값싼 연결을 하여 적합.

C 탈락 -> S3는 VPC 밖의 외부 서비스로 부적합.

D 탈락 -> 마찬가지로 VPC 밖의 외부 서비스로 부적합.

</div>
</details>

<hr/>

## Prob. 268

MySQL 데이터베이스는 기업의 주문 이행 서비스에서 사용됩니다. 데이터베이스는 많은 양의 동시 요청 및 트랜잭션을 처리할 수 있어야 합니다. 데이터베이스는 개발자에 의해 패치되고 조정됩니다. 이로 인해 새로운 제품 기능의 도입이 지연됩니다.
조직은 이 새로운 어려움을 해결하는 데 도움이 되도록 클라우드 기반 서비스를 사용하기를 원합니다. 솔루션은 개발자가 코드를 거의 또는 전혀 수정하지 않고 데이터베이스를 이동할 수 있도록 해야 하며 성능을 최대화해야 합니다.

이러한 요구 사항을 달성하려면 어떤 솔루션 설계자 서비스를 사용해야 합니까?

A. Amazon Aurora

B. Amazon DynamoDB

C. Amazon ElastiCache

D. MySQL on Amazon EC2

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

코드를 거의 또는 전혀 수정하지 않고 성능을 최대화 문제 요점.

MySQL 데이터베이스는 기업의 주문 이행 서비스. <br>
많은 양의 동시 요청 및 트랜잭션을 처리. <br>
개발자에 의해 패치되고 조정하여 새로운 제품 기능의 도입이 지연. <br>
클라우드 기반 서비스를 사용하기를 원함.

MySQL 데이터베이스를 Amazon Aurora와 같은 확장성이 뛰어난 서비스로 마이그레이션할 때 애플리케이션 다운타임을 최소화하고 기본 MySQL 백업 툴을 사용할 수 있습니다.

Amazon Aurora는 완전히 관리되는 DB이며 MySQL/PostgreSQL 데이터베이스를 지원합니다.

A 정답 -> Aurora는 MySQL/PostgreSQL를 지원하며 성능(확장성/가용성/자동)면에서 적합.

B 탈락 -> DynamoDB는 NoSQL로 RDMS의 DB에 대한 코드를 변경하여 부적합.

C 탈락 -> ElastiCach는 인-메모리로 디스크기반 스토리지(S3)보다 빠른 처리 성능 가지는 것으로 DB와는 부적합.

D 탈락 -> EC2는 완전 관리형 서비스가 아니라서 DB와 서버관리를 하여 부적합.

</div>
</details>

<hr/>

## Prob. 269

기업은 다중 지역 재해 복구를 위해 1초 RPO(복구 시점 목표) 및 1분 RTO(복구 시간 목표)를 사용하여 관계형 데이터베이스를 만들어야 합니다.

어떤 AWS 솔루션이 이 작업을 수행할 수 있습니까?

A. Amazon Aurora 글로벌 데이터베이스

B. Amazon DynamoDB 글로벌 테이블

C. Multi-AZ를 사용하는 MySQL용 Amazon RDS

D. 지역 간 스냅샷 복사본을 사용하는 MySQL용 Amazon RDS

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

다중 지역 재해 복구를 위해 1초 RPO(복구 시점 목표) 및 1분 RTO(복구 시간 목표)를 사용하여 관계형 데이터베이스 문제 요점.

Amazon Aurora Global Database 참조.

      1초의 RPO(Recovery Point Objective, 복구 목표 지점) - 1초 전까지의 데이터는 안전이 보장된다.
      1분 미만의 RTO(Recovery Time Objective, 복구 목표 시간) - 1분 내에 복구가 보장된다.

A 정답 -> Aurora 글로벌 데이터베이스는 다른 리전으로 계속 복제/쓰기 포워딩하여 맞추기 때문에 적합.

B 탈락 -> 관계형 DB가 아니라 부적합.

C 탈락 -> Multi-AZ는 장애 극복/읽기 성능에 영향을 받지만 하나의 지역에서만이라 부적합.

D 탈락 -> 지역 간 스냅샷 복사본은 복구하는데 오래 걸려서 부적합.

</div>
</details>

<hr/>

## Prob. 270

솔루션 설계자는 새로운 정적 웹사이트의 구현을 설계하는 책임을 맡습니다. 솔루션은 비용 효율적이어야 하며 최소 99%의 가용성을 유지해야 합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. 버전 관리를 사용하지 않도록 설정한 한 AWS 지역의 Amazon S3 버킷에 애플리케이션을 배포합니다.

B. 두 AWS 영역과 두 가용성 영역에서 실행되는 Amazon EC2 인스턴스에 애플리케이션을 배포합니다.

C. 버전 및 지역 간 복제를 사용하도록 설정한 Amazon S3 버킷에 애플리케이션을 배포합니다.

D. 하나의 AWS 영역과 하나의 가용성 영역에서 실행되는 Amazon EC2 인스턴스에 애플리케이션을 배포합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

비용 효율적이어야 하며 최소 99%의 가용성을 유지 문제 요점.

정적 웹사이트의 구현을 설계.

versioning은 recovery를 위한 기능이다. <br>
S3는 단일 리전에 있더라도 99.99%의 가용성을 보장한다. <br>
가용성(可用性, Availability)이란 서버와 네트워크, 프로그램 등의 정보 시스템이 정상적으로 사용 가능한 정도를 말한다. 가동률과 비슷한 의미.

A 정답 -> 값싼 S3에 정적 컨텐츠를 호스팅하고 버전 관리는 장애 극복으로 안해도 이미 가용성이 충분하기에 적합.

B 탈락 -> EC2는 동적 컨텐츠에 대해 지원하여 부적합.

C 탈락 -> 값싼 S3에 정적 컨텐츠를 호스팅하는데 버저닝/지역 간 복제를 하지 않아도 되어 부적합.

D 탈락 -> EC2는 동적 컨텐츠에 대해 지원하여 부적합.

</div>
</details>

<hr/>

* Ref
  - [ExamTopics](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate-saa-c02/view/27)
