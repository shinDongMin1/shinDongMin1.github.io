---
layout: post
title: "[AWS-SAA] Examtopics 41~50"
subtitle: AWS
date: '2023-03-19 00:00:01 +0900'
category: study
tags: aws aws-saa
image:
  path: /assets/img/study_AWS/saa-co2_logo.png
---

SAA Examtopics 41~50번 문제를 풀어보자.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## Prob. 41

실험과 민첩성을 촉진하기 위해 비즈니스에서는 개발자가 현재 IAM 정책을 기존 IAM 역할에 연결할 수 있습니다. 반면 보안 운영 팀은 개발자가 현재 관리자 정책을 첨부하여 다른 보안 규칙을 우회할 수 있다고 우려하고 있습니다.

솔루션 설계자는 이 문제를 처리할 때 어떤 접근 방식을 사용해야 합니까?

A. 개발자가 새 정책을 만들 때마다 알림을 보내는 Amazon SNS 항목을 만듭니다.

B. 서비스 제어 정책을 사용하여 조직 단위의 모든 계정에서 IAM 활동을 비활성화합니다.

C. 개발자가 정책을 첨부하지 못하도록 하고 모든 IAM 작업을 보안 운영 팀에 할당합니다.

D. 개발자 IAM 역할에 관리자 정책 연결을 명시적으로 거부하는 IAM 권한 경계를 설정합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

개발자가 현재 IAM 정책을 기존 IAM 역할에 연결하면 다른 보안 규칙을 우회 문제 요점.

**AWS Identity and Access Management(IAM)**은 `AWS 리소스에 대한 액세스`를 안전하게 **제어**할 수 있는 아마존 웹 서비스입니다.
`IAM을 사용하여` 리소스를 사용하도록 **인증(로그인)** 및 **권한 부여(권한 있음)**된 대상을 **제어**.
**누가 언제 어디서 무엇을 어떻게**를 `설정할 수 있고 제어`할 수 있는 서비스.

IAM은 `총 4가지의 요소`로 이루어져있다.

1. **사용자**
    * `실제 AWS를 사용`하는 **사람** 혹은 **애플리케이션**을 의미

2. **그룹**
    * `사용자의` **집합**
    * 그룹에 속한 사용자는 `그룹에 부여된 권한`을 행사

3. **정책(Policy)**
    * `사용자와 그룹, 역할`이 `무엇을 할 수 있는지에 관한 문서`
    * **JSON(JavaScript Object Notation)** 형식으로 정의

4. **역할(Role)**
    * **AWS 리소스**에 부여하여 `AWS 리소스가 무엇을 할 수 있는지를 정의`
    * 혹은 **다른 사용자**가 역할을 부여 받아 사용
    * 다른 자격에 대해서 신뢰관계를 구축 가능
    * 역할을 바꾸어 가며 서비스를 사용 가능

![IAM_Config](/assets/img/study_AWS/[AWS]_IAM_이해/IAM_config.png)

**SCP(서비스 제어 정책)**는 `조직의 권한을 관리`하는 데 사용할 수 있는 조직 정책 유형.
조직의 모든 계정에 사용 가능한 최대 권한을 중앙에서 제어합니다. SCP를 사용하면 조직의 액세스 제어 지침에 따라 계정을 유지.

A 탈락 -> 새 정책을 만드는 것에 대한 알림을 받기만 하고 대응이 없어 부적합.

B 탈락 -> SCP를 사용하여 조직의 IAM 활동을 비활성화하면 보안 규칙이 적용이 안되어 부적합.

C 탈락 -> 개발자가 어떤 정책도 첨부하지 못하게 하는 것은 실험과 민첩성을 촉진하지 못하여 부적합.

D 정답 -> **권한 경계**는 그룹이 아닌 `사용자 및 역할에만 할당`할 수 있으며 문제가 되는 관리자 정책만 명시적으로 거부시켜서 보안적과 비즈니스적으로 적합.

</div>
</details>

<hr/>

## Prob. 42

새로 형성된 회사는 3계층 웹 애플리케이션을 개발했습니다. 프런트 엔드는 완전히 정적 정보로 구성됩니다. 마이크로서비스는 애플리케이션 계층을 형성합니다. 사용자 데이터는 최소한의 지연으로 액세스할 수 있는 JSON 문서 형식으로 보관됩니다. 회사는 첫 해에 월별 트래픽 급증과 함께 최소한의 정규 트래픽을 예상합니다. 스타트업 팀의 운영 간접비는 최소한으로 유지되어야 합니다.

솔루션 설계자는 이를 달성하기 위한 수단으로 무엇을 제안해야 합니까?

A. 프런트 엔드를 저장하고 서비스하려면 Amazon S3 정적 웹 사이트 호스팅을 사용하십시오. 애플리케이션 계층에 AWS Elastic Beanstalk를 사용합니다. Amazon DynamoDB를 사용하여 사용자 데이터를 저장합니다.

B. Amazon S3 정적 웹 사이트 호스팅을 사용하여 프런트 엔드를 저장하고 제공합니다. 애플리케이션 계층에 Amazon Elastic Kubernetes Service(Amazon EKS)를 사용합니다. Amazon DynamoDB를 사용하여 사용자 데이터를 저장합니다.

C. Amazon S3 정적 웹 사이트 호스팅을 사용하여 프런트 엔드를 저장하고 제공합니다. 애플리케이션 계층에 Amazon API Gateway 및 AWS Lambda 함수를 사용합니다. Amazon DynamoDB를 사용하여 사용자 데이터를 저장합니다.

D. Amazon S3 정적 웹 사이트 호스팅을 사용하여 프런트 엔드를 저장하고 제공합니다. 애플리케이션 계층에 Amazon API Gateway 및 AWS Lambda 함수를 사용합니다. 읽기 복제본과 함께 Amazon RDS를 사용하여 사용자 데이터를 저장합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

JSON 문서 형식 보관 및 트래픽 급증에 대한 운영 간접비 최소화 문제 요점.

3계층(전송) 웹 애플리케이션의 프런트 엔드는 완전히 정적 정보로 구성 되어 S3 정적 웹사이트 호스팅을 해야함.

**Amazon S3를 사용하여 정적 웹 사이트 호스팅**
Amazon S3을 사용하여 정적 웹 사이트를 호스팅할 수 있습니다. 정적 웹 사이트에서 개별 웹 페이지는 정적 콘텐츠를 포함합니다. 클라이언트 측 스크립트를 포함.
이와는 대조적으로, 동적 웹 사이트는 PHP, JSP 또는 ASP.NET 등 서버 측 스크립트를 포함한 서버 측 처리에 의존.
Amazon S3은 서버 측 스크립팅을 지원하지 않지만 AWS에는 동적 웹 사이트를 호스팅하기 위한 다른 리소스(EC2).

Amazon S3 웹 사이트 엔드포인트는 HTTPS를 지원하지 않음.
HTTPS를 사용하려는 경우 Amazon CloudFront를 사용하여 Amazon S3에서 호스팅되는 정적 웹 사이트를 제공.

`AWS Amplify 콘솔`을 사용하여 단일 페이지 웹 앱을 호스팅할 수 있습니다. AWS Amplify 콘솔은 단일 페이지 앱 프레임워크(예: React JS, Vue JS, Angular JS 및 Nuxt)와 정적 사이트 생성기(예: Gatsby JS, React-static, Jekyll 및 Hugo)로 빌드된 단일 페이지 앱을 지원.

**Beanstalk/EKS/API Gateway + Lambda**
Amazon Elastic Beanstalk(EB) - 사용하면 애플리케이션을 실행하는 인프라에 대해 자세히 알지 못해도 AWS 클라우드에서 애플리케이션을 신속하게 배포하고 관리.
선택 또는 제어에 대한 제한 없이 관리 복잡성을 줄일 수 있습니다. 애플리케이션을 업로드하기만 하면 Elastic Beanstalk에서 용량 프로비저닝, 로드 밸런싱, 조정, 애플리케이션 상태 모니터링에 대한 세부 정보를 자동으로 처리.

Amazon Elastic Kubernetes Service(EKS) - 자체 Kubernetes 컨트롤 플레인 또는 노드를 설치, 운영 및 유지 관리할 필요 없이 AWS의 Kubernetes 실행에 사용할 수 있는 관리형 서비스입니다. Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장, 관리를 자동화하기 위한 오픈 소스 시스템.

Amazon API Gateway에서 Lambda 사용 - 사용하여 웹 API와 Lambda 함수의 HTTP 엔드포인트를 생성할 수 있습니다. API Gateway는 HTTP 요청을 Lambda 함수로 라우팅하는 웹 API를 생성하고 문서화하는 도구를 제공합니다. AWS Identity and Access Management(IAM) 및 Amazon Cognito을 사용하여 인증 및 승인 제어를 통해 API에 대한 액세스를 보호할 수 있습니다. API는 인터넷을 통해 트래픽을 처리하거나 VPC 내에서만 액세스 가능함.

![1](/assets/img/study_AWS/[SAA]_ExamTopics_41~50/1.png)

최소 운영 오버헤드 지출 => Beanstalk 또는 EKS 대신 람다 및 API 게이트웨이.
API Gateway + Lambda는 "마이크로서비스"에 가장 적합.

**RDS와 DynamoDB**
RDS - RDBMS를 사용하여 구조화(스키마)된 데이터를 저장하고 쉽게 설정, 운영 및 확장하는 완전 관리형 서비스.

Aurora - RDBMS를 사용(MySQL 및 PostgreSQL 호환 관계형 데이터베이스)하여 성능, 보안, 안전성, 가용성, 간편성과 비용 효율성을 결합여 클라우드를 위해 구축되어 시간 소모적인 관리 작업을 자동화(하드웨어 프로비저닝/데이터베이스 설정/패치 및 백업)하는 EBS기반으로 기존의 RDS와는 다른 아키텍쳐를 갖고 있음(Single-Master/Multi-Master).

DynamoDB - 완전관리형 NoSQL(비정형) 데이터베이스로 자동으로 스토리지를 늘리고 클러스터를 확장하여 데이터를 분산.
어떠한 수준의 요청 트래픽도 일관적인 속도로 처리.
읽기/쓰기 처리량(Read/Write Throughput)을 직접 지정.
모니터링/고가용성과 데이터 내구성을 제공/암호화/보조 인덱스/SSD/온디맨드 백업/데이터 유지 시간(TTL).
DAX는 완전관리형인 메모리 cache로 자주 반복되는 쿼리 처리.
RDBMS 기반 데이터베이스는 서버 한 대에 저장하기가 어려우므로 샤딩(Shading)으로 분산 저장하는데 반면 DynamoDB는 자동으로 처리.
조인(Join)과 같은 복잡한 쿼리가 필요한 환경에는 부적합. 

JSON 문서와 같은 비구조화된 데이터는 RDS에 저장할 수 없음.

마이크로서비스 - 소프트웨어가 잘 정의된 API를 통해 통신하는 소규모의 독립적인 서비스로 구성되어 있는 경우의 소프트웨어 개발을 위한 아키텍처 및 조직적 접근 방식.
독립적인 소규모 팀에서 보유.

A, B 탈락 -> 마이크로서비스는 소규모로 API Gateway + Lambda 서비스보다 자동 배포하는 서비스들은 부적합.

C 정답 -> API Gateway + Lambda 서비스와 DynamoDB가 적합.

D 탈락 -> 비정형 데이터를 저장하기 위해 RDS를 사용하여 부적합.

</div>
</details>

<hr/>

## Prob. 43

Amazon Elastic Container Service(Amazon ECS) 컨테이너 인스턴스는 ALB(Application Load Balancer) 뒤에 전자 상거래 웹 사이트의 웹 애플리케이션을 설치하는 데 사용됩니다. 사용량이 많은 순간에는 웹 사이트 속도가 느려지고 가용성이 감소합니다. 솔루션 설계자는 Amazon CloudWatch 경보를 활용하여 가용성 문제가 발생할 때 알림을 받고 리소스를 확장할 수 있습니다. 비즈니스 경영진은 이러한 상황에 자동으로 대응하는 시스템을 원합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. ALB에 시간 초과가 있을 때 ECS 서비스를 확장하도록 AWS 자동 스케일링을 설정합니다. CPU 또는 메모리 예약이 너무 많을 경우 ECS 클러스터를 확장하도록 AWS 자동 스케일링을 설정합니다.

B. AWS 자동 스케일링을 설정하여 ALB CPU 사용률이 너무 높을 경우 ECS 서비스를 스케일아웃합니다. CPU 또는 메모리 예약이 너무 많을 때 ECS 클러스터를 확장하도록 AWS 자동 스케일링을 설정합니다.

C. 서비스의 CPU 활용도가 너무 높을 경우 ECS 서비스를 확장하도록 AWS 자동 스케일링을 설정합니다. CPU 또는 메모리 예약이 너무 많을 경우 ECS 클러스터를 확장하도록 AWS 자동 스케일링을 설정합니다.

D. AWS 자동 스케일링을 설정하여 ALB 대상 그룹의 CPU 사용률이 너무 높을 경우 ECS 서비스를 스케일아웃합니다. CPU 또는 메모리 예약이 너무 많을 경우 ECS 클러스터를 확장하도록 AWS 자동 스케일링을 설정합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C (or D?) // C가 유력

해설 : 

자동으로 스케일링 되는 대응 시스템 문제 요점.

스케일 아웃 - 동일한 서버를 여러 대 추가하여 시스템을 확장하는 방법
스케일 업 - 서버 하나의 성능을 업그레이드하여 시스템을 확장하는 방법

스케일 아웃 - 서버 용량 부족으로 자원을 늘리는 작업
스케일 인 - 서버 용량 부족으로 늘렸던 자원을 다시 회수 하는 작업

**Amazon Elastic Container Service(Amazon ECS)**
Amazon Elastic Container Service(Amazon ECS) 컨테이너 인스턴스 - 컨테이너화된 애플리케이션의 손쉬운 배포, 관리 및 크기 조정을 지원하는 완전관리형 컨테이너 오케스트레이션 서비스로 하이브리드 환경에 배포/배치 처리 지원(EC2, Fargate)/웹 애플리케이션 크기 조정.
Registry, Docker 등의 서드 파티 도구와 통합 이러한 통합을 통해 팀은 환경이 아닌 애플리케이션 구축에 더 쉽게 집중.

Amazon ECS 클러스터 Auto Scaling - Amazon ECS는 클러스터에 등록된 Amazon EC2 인스턴스의 크기 조정을 관리.
CloudWatch 지표와 오토 스케일링에 연결하는 대상 추적 조정 정책 생성.
태스크가 클러스터에 가하는 부하를 기반으로 오토 스케일링의 스케일 인 및 스케일 아웃 작업을 관리.

**ALB**
ALB - 애플리케이션 로드밸런서의 약자로, 웹 서비스에 걸리는 부하를 분산해주는 로드 밸런서로 다양한 소셜 네트워킹 서비스의 확장 및 여러 요인으로 인해 웹 애플리케이션 접속이 기하급수적으로 늘어남.
요소로 Load balancer > Listener(정책) > Target group(Health check)

지연 시간이 길어질 수 있는 원인은 
* 네트워크 연결 문제
* 백엔드 인스턴스의 메모리(RAM) 사용량 과다
* 백엔드 인스턴스의 높은 CPU 사용률
* 백엔드 인스턴스의 부적절한 웹 서버 구성
* 외부 데이터베이스 또는 Amazon Simple Storage Service(Amazon S3) 버킷 같은 백엔드 인스턴스에서 실행되는 웹 애플리케이션의 종속성 문제

A 탈락 -> ALB시간 초과가 발생했으면 이미 대응이 늦어진 것으로 부적합.

B, D 탈락 -> ALB의 CPU사용률과 ALB 대상 그룹의 CPU사용률에 대한 것이지만 별개로 스케일 아웃은 자원을 늘리는데 다시 회수하는 스케일 인이 없기 때문에 자동으로 대응하는 것에 부적합.

C 정답 -> 서비스(전자 상거래)의 CPU 활용도가 높으면 자동 스케일링을 적용하는 것이 적합.

</div>
</details>

<hr/>

## Prob. 44

기업은 Site-to-Site VPN 연결을 사용하여 온프레미스에서 AWS 클라우드 서비스에 안전하게 액세스할 수 있도록 합니다. Amazon EC2 인스턴스에 대한 VPN 연결을 통한 트래픽 증가로 인해 사용자가 VPN 연결 속도가 느려지고 있습니다.
어떤 접근 방식이 VPN 처리량을 증가시킬까요?

A. 동일한 네트워크에 대해 여러 고객 게이트웨이를 구현하여 처리량을 확장합니다.

B. 동일한 비용의 다중 경로 라우팅이 있는 중계(Transit) 게이트웨이를 사용하고 VPN 터널을 추가합니다.

C. 등가 비용 다중 경로 라우팅 및 다중 채널로 가상 사설 게이트웨이를 구성합니다.

D. VPN 구성의 터널 수를 늘려 기본 제한을 초과하여 처리량을 확장합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

VPN 처리량 문제 요점.

기본적으로 Amazon VPC로 시작하는 인스턴스는 자체(원격) 네트워크와 통신할 수 없습니다. AWS Site-to-Site VPN(Site-to-Site VPN) 연결을 생성하고 연결을 통해 트래픽을 전달하도록 라우팅을 구성하여 VPC에서 원격 네트워크에 대한 액세스를 활성화.

**Site-to-Site**
두 개의 네트워크 도메인이 가상의 사설 네트워크 연결을 사용하여 프라이빗 통신을 가능하게 하는 서비스로 표준 IPSec VPN만 지원.
VPN 연결은 VPC와 자체 온프레미스 네트워크 간의 연결을 의미합니다. Site-to-Site VPN은 인터넷 프로토콜 보안(IPsec) VPN 연결을 지원.

고객 게이트웨이 디바이스는 온프레미스 네트워크(Site-to-Site VPN 연결에서 사용자 측)에서 소유하거나 관리하는 물리적 또는 소프트웨어 어플라이언스.

고객 게이트웨이 (Customer Gateway, CGW) 온프레미스 네트워크의 고객 게이트웨이 디바이스를 나타내는 AWS에서 생성하는 리소스로 온프레미스의 장비 정보를 지정합니다.

가상 프라이빗 게이트웨이 (Virtual Private Gateway, VGW) Site-to-Site VPN 연결에서 아마존 측에 있는 Gateway로 VPC에 연결하는 데 사용되며 VPN 또는 Direct connect와 함께 작동할 수 있습니다.

전송 게이트 웨이 (Transit Gateway) 가상 프라이빗 클라우드(VPC)와 온프레미스 네트워크를 상호 연결하는 데 사용할 수 있는 전송 허브.
VPC나 온프레미스등의 네트워크를 단일 지점으로 연결할 수 있습니다.

**AWS Transit Gateway**
AWS Transit Gateway를 사용하면 여러 VPC 간의 연결을 간소화할 수 있으며 단일 VPN 연결로 AWS Transit Gateway에 연결된 모든 VPC에 연결할 수도 있다.<br>
또한 AWS Transit Gateway를 사용하면 여러 VPN 터널에서 ECMP(등비용 다중 경로) 라우팅 지원을 통해 IPsec VPN 처리량을 확장할 수 있다. <br>
단일 VPN 터널의 최대 처리량은 여전히 1.25Gbps이다. <br>
ECMP 사용 중계 게이트웨이에 대한 VPN 터널을 여러 개 설정하면 기본 제한인 1.25Gbps 이상으로 확장할 수 있습니다.

A 탈락 -> 동일한 네트워크에 대해 온프레미스측 고객을 늘리면 속도가 더 느려져서 부적합.

B 정답 -> 1대 다수 연결이 가능하며 사용자 측에 VPN 터널을 추가하여 더 빨리 처리 가능하여 적합.

C 탈락 -> 다중 경로 및 다중 채널(기존 아날로그 지상파 1개 채널을 디지털 방식으로 전환해 복수의 채널인 티비/라디오/방송으로 활용)로 가상 사설 게이트웨이을 구성해도 다중 채널은 도움이 안되고 1대1 연결만 되는거 같아서 부적합.

D 탈락 -> 터널 수를 늘리면 도움이 되지만 기본 제한을 초과할 수 없어 부적합.

</div>
</details>

<hr/>

## Prob. 45

Amazon EC2 Linux 인스턴스에서 비즈니스는 웹 사이트를 호스팅합니다. 몇 가지 예가 오작동하고 있습니다. 문제 해결은 실패한 인스턴스에 스왑 공간이 부족함을 나타냅니다. 운영 팀의 리더는 이를 위한 모니터링 솔루션이 필요합니다.

솔루션 설계자는 어떤 권장 사항을 제시해야 합니까?

A. Amazon CloudWatch SwapUsage 메트릭을 구성합니다. CloudWatch의 EC2 메트릭에서 SwapUsage 메트릭을 모니터링합니다.

B. EC2 메타데이터를 사용하여 정보를 수집한 다음 Amazon CloudWatch 사용자 지정 메트릭에 게시합니다. CloudWatch에서 SwapUsage 메트릭을 모니터링합니다.

C. 인스턴스에 Amazon CloudWatch 에이전트를 설치합니다. 설정된 예약에 따라 적절한 스크립트를 실행합니다. CloudWatch에서 스왑 활용률 메트릭 모니터링

D. EC2 콘솔에서 상세 모니터링을 활성화합니다. Amazon CloudWatch 스왑 사용률 사용자 지정 메트릭을 생성합니다. CloudWatch에서 스왑 활용률 메트릭 모니터링

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

스왑 공간이 부족함에 대한 모니터링 문제 요점.

**Amazon CloudWatch**
네임스페이스/지표/측정기준/해결/통계/백분위수/경보 등의 리소스 상태를 볼 수 있습니다. 이메일 알림에 대한 Service Quotas가 있음.

Amazon CloudWatch 사용자 지정 메트릭은 AWS CLI 또는 API를 사용하여 CloudWatch에 자체 지표를 게시할 수 있습니다. AWS Management Console을 사용하여 게시된 지표의 통계 그래프를 볼 수 있음.

Cloudwatch 에이전트는 스왑, 메모리 사용률 모니터링을 위한 기능으로 기본적으로 사용 불가인데 사용자가 직접 지정해야 함.

상세 모니터링을 활성화는 기본 설정상 인스턴스는 기본 모니터링 기능이 활성화되어 있습니다. 세부 모니터링 활성화를 선택할 수 있습니다. 세부 모니터링을 활성화하면 Amazon EC2 콘솔에 인스턴스에 대한 1분 모니터링 그래프가 표시.

A 탈락 -> 스왑 사용률은 에이전트를 통해서만 제공되어 사용할 수 있어 부적합.

B 탈락 -> 수집한 데이터로 AWS CLI 또는 API를 사용하여 CloudWatch에 자체 지표를 게시되지만 스왑 사용률은 에이전트를 통해서만 제공되어 사용할 수 있어 부적합.

C 정답 -> 에이전트를 설치했으니 스왑/메모리 사용률을 알 수 있고 오작동 예를 스크립트 실행하여 모니터링하여 적합.

D 탈락 -> 세부 모니터링을 활성화하면 EC2 콘솔에 인스턴스에 대한 1분 모니터링 그래프가 표시되지만 스왑 사용률은 에이전트를 통해서만 제공되어 사용할 수 있어 부적합.

</div>
</details>

<hr/>

## Prob. 46

AWS는 기업에서 OLTP(온라인 트랜잭션 처리) 부담을 수행하는 데 사용됩니다. 이 워크로드는 암호화되지 않은 Amazon RDS 데이터베이스 인스턴스를 사용하여 다중 AZ 환경에 배포됩니다. 이 인스턴스의 데이터베이스는 매일 백업됩니다.

데이터베이스와 스냅샷이 지속적으로 암호화되도록 솔루션 설계자는 앞으로 무엇을 해야 합니까?

A. 최신 DB 스냅샷 복사본을 암호화합니다. 암호화된 스냅샷을 복원하여 기존 DB 인스턴스를 바꿉니다.

B. 암호화된 새 Amazon EBS(Amazon Elastic Block Store) 볼륨을 생성하고 여기에 스냅샷을 복사합니다. DB 인스턴스에서 암호화를 사용합니다.

C. 스냅샷을 복사하고 AWS KMS(키 관리 서비스)를 사용하여 암호화를 사용하도록 설정합니다. 암호화된 스냅샷을 기존 DB 인스턴스에 복원합니다.

D. AWS KMS(키 관리 서비스) 관리 키(SSE-KMS)를 사용하여 서버 측 암호화를 사용하여 암호화된 Amazon S3 버킷에 스냅샷을 복사합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

DB와 스냅샷이 지속적으로 암호화 문제 요점.

DB 스냅샷에서 기존 DB 인스턴스로 복원할 수 없습니다. 복원할 때 새 DB 인스턴스가 생성됩니다.

**AWS KMS**
AWS Key Management Service(AWS KMS)는 데이터를 보호하는 데 사용하는 암호화 키를 쉽게 생성하고 제어할 수 있게 해주는 관리형 서비스.
데이터를 암호화하는 대부분의 기타 AWS 서비스와 통합(다양한 암호화 서비스에 대한 키를 관리하는 곳인거 같음).
또한 감사, 규제 및 규정 준수 요구사항에 따라 KMS 키 사용을 기록하기 위해 AWS CloudTrail과 통합.
AWS KMS API를 사용하여 KMS 키와 사용자 지정 키 스토어 등의 특수 기능을 생성 및 관리하고, 암호화 작업에서 KMS 키를 사용할 수 있음.

A 정답 -> 처음부터 암호화가 되지 않은 DB는 도중에 암호화가 불가능하니 최신 DB 스냅샷을 암호화하여 새로 생성한 후에 그것을 기존 DB인스턴스와 교체하여 적합.

B 탈락 -> 암호화된 EBS 볼륨으로 스냅샷을 복사하는 것은 EBS기반 DB인 Aurora인 것 같고 이것으로 기존 DB인스턴스에 암호화는 불가능하여 부적합.

C 탈락 -> 암호화까지 좋았는데 마지막에 기존 DB 인스턴스에 복원하는 것이 아니고 교체해야 해서 부적합.

D 탈락 -> 갑자기 서버 측 암호화하고 그걸 암호화된 S3 버킷에 저장하는지 모르겠어서 부적합.

</div>
</details>

<hr/>

## Prob. 47

기업은 다양한 Amazon EC2 인스턴스를 통해 소비자로부터 데이터를 수집하는 애플리케이션을 운영합니다. 처리 후 데이터는 장기 저장을 위해 Amazon S3에 업로드됩니다. 애플리케이션 연구에 따르면 EC2 인스턴스가 장기간 비활성 상태인 것으로 나타났습니다. 솔루션 설계자는 비용을 최소화하면서 사용량을 최대화하는 시스템을 제공해야 합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. 온디맨드 인스턴스가 있는 오토 스케일링 그룹에서 Amazon EC2를 사용합니다.

B. 온디맨드 인스턴스와 함께 Amazon Lightsail을 사용하도록 애플리케이션을 구축합니다.

C. 작업이 없을 때 EC2 인스턴스를 자동으로 중지하는 Amazon CloudWatch cron 작업을 생성합니다.

D. Amazon SQS(Amazon Simple Queue Service) 및 AWS Lambda와 함께 이벤트 중심 설계를 사용하도록 응용 프로그램을 다시 설계하십시오.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A or D

해설 : 

장기간 비활성 상태 애플리케이션을 비용 최소화하고 사용량을 최대화 문제 요점.

D가 일반적인 답이지만, 재설계는 꺼려진다면 A가 답일 수 있음.<br>
또한 사용량을 최대화해야 하므로 람다 D가 아니라 A가 답이라는 사람이 있음.

스팟 인스턴스 < 예약 인스턴스 < 온디맨드 < 전용 호스트

**Amazon Lightsail**
사용하기 쉬운 가상 프라이빗 서버(VPS) 인스턴스, 컨테이너, 스토리지, 데이터베이스 등을 비용 효율적인 월별 가격으로 제공하여 저렴한 비용의 사전 구성된 클라우드 리소스를 통해 애플리케이션 및 웹 사이트를 빠르게 구축.

**Amazon CloudWatch cron**
lambda를 특정 시간에 자동 실행하기(cron 배치).
EventBridge(CloudWatch Events) 이벤트 트리거 추가.
이벤트 설정 cron(시간).

**Amazon SQS**
메시지 손실을 우려하거나 다른 서비스를 제공할 필요 없이 소프트웨어 구성 요소 간에 어떤 볼륨의 메시지든 전송, 저장 및 수신할 수 있음.
마이크로서비스, 분산 시스템 및 서버리스 애플리케이션을 위한 완전관리형 메시지 대기열.
애플리케이션 신뢰성 및 확장성 향상/마이크로서비스 분리 및 이벤트 기반 애플리케이션 처리/작업을 비용 효율적이고 정시에 완료하도록 보장/메시지 순서 유지 및 중복 제거.

A 정답 -> 사용한 만큼 비용이 첨부되어 장기간 비활성 상태에 대해 비용 효율적이라고 생각하며 오토 스케일링으로 사용량을 최대화한다고 생각하는데 애매함.

B 탈락 -> 굳이 Amazon Lightsail 사용 이유가 없음 개발을 빠르게 하기 위한 것이라 부적합.

C 탈락 -> cron은 작업이 없을 때가 아닌 시간으로 자동 중지 시키는 것 같아 부적합.

D 정답 -> 작업을 비용 효율적이고 애플리케이션 신뢰성 및 확장성 향상하는데 애매함.

</div>
</details>

<hr/>

## Prob. 48

기업은 많은 독립적인 Amazon Web Services 계정에서 통합된 다중 계정 설계로 마이그레이션하려고 합니다. 조직은 사업부를 위해 많은 수의 새 AWS 계정을 생성할 계획입니다. 조직은 이러한 AWS 계정에 대한 액세스를 인증하기 위해 단일 회사 디렉터리 서비스를 사용해야 합니다.

이러한 요구 사항을 충족하기 위해 솔루션 설계자는 어떤 단계를 옹호해야 합니까? (2개를 선택하세요.)

A. 모든 기능이 설정된 상태에서 AWS 조직에 새 조직을 만듭니다. 조직에서 새 AWS 계정을 생성합니다.

B. Amazon Cognito ID 풀을 설정합니다. Amazon Cognito 인증을 허용하도록 AWS Single Sign-On을 구성합니다.

C. AWS 계정을 관리하도록 SCP(서비스 제어 정책)를 구성합니다. AWS 디렉토리 서비스에 AWS Single Sign-On을 추가합니다.

D. AWS 조직에 새 조직을 만듭니다. AWS 디렉터리 서비스를 직접 사용하도록 조직의 인증 메커니즘을 구성합니다.

E. 조직에 AWS SSO(Single Sign-On)를 설정합니다. AWS SSO를 구성하고 회사의 회사 디렉토리 서비스와 통합합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A, E

해설 : 

새 AWS 계정과 디렉터리 서비스 문제 요점.

[링크1](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-ad.html)

[링크2](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html)

새 AWS 계정 생서 - A, D
디렉토리 서비스 - B, C, E

**Amazon Cognito**
웹 및 모바일 앱에 대한 인증, 권한 부여 및 사용자 관리를 제공
타사를 통해 `소셜 로그인할 수 있습니다.`

**SCP(서비스 제어 정책)**
`조직의 권한을 관리`하는 데 사용할 수 있는 조직 정책 유형.

**AWS 디렉토리 서비스**
AWS Directory Service는 다른 AWS 서비스에서 Microsoft Active Directory(AD)를 사용할 수 있는 몇 가지 방법을 제공.
디렉터리는 사용자, 그룹 및 디바이스에 대한 정보를 저장하고, 관리자는 이를 사용하여 정보 및 리소스에 대한 액세스를 관리.
클라우드에서 기존 Microsoft AD 또는 LDAP (Lightweight Directory Access Protocol) 인식 애플리케이션을 사용하려는 고객에게 다양한 디렉터리 선택 옵션을 제공.

**AWS Single Sign-On**
Single Sign-On(SSO)은 1회 사용자 인증으로 다수의 애플리케이션 및 웹사이트에 대한 사용자 로그인을 허용하는 인증 솔루션.
한 번 자격 증명이 검증된 사용자에게는 반복되는 로그인 없이 모든 암호 보호 리소스에 액세스하도록 하여 보안과 사용자 경험을 모두 충족.

디렉토리 접속 -> SSO 인증 -> AWS 계정 액세스?

A 정답 -> D가 아니라서 A를 골랐지만 모든 기능이 설정된 상태의 그룹에서 시작해야 그룹 별로 각 보안을 변경해줄 수 있어 적합.

B 탈락 -> Cognito는 앱에 대한 인증/권한/사용자/소셜 로그인을 관리하는 것이라 부적합.

C 탈락 -> SCP는 조직 권한을 관리하지만 디렉토리 서비스에 SSO를 추가하는 것은 부적합.

D 탈락 -> 디렉토리 서비스와 새 조직을 통합하여 직접 사용하는 것은 부적합.

E 정답 -> 조직에 SSO를 설정하고 회사 디렉토리 서비스와 통합하여 보안성 있는 디렉토리 서비스에 적합.

</div>
</details>

<hr/>

## Prob. 49

솔루션 설계자는 완료하는 데 최대 2시간이 소요되는 일일 데이터 처리 작업을 개발하고 있습니다. 작업이 중지되면 처음부터 다시 시작해야 합니다.

솔루션 설계자가 이 문제를 해결하는 가장 비용 효율적인 방법은 무엇입니까?

A. cron 작업에 의해 트리거된 Amazon EC2 예약된 인스턴스에서 로컬로 실행되는 스크립트를 생성합니다.

B. Amazon EventBridge(Amazon CloudWatch Events) 예약 이벤트로 트리거된 AWS Lambda 함수를 생성합니다.

C. Amazon EventBridge(Amazon CloudWatch Events) 스케줄링된 이벤트로 트리거된 Amazon ECS(Amazon Elastic Container Service) Fargate 작업을 사용합니다.

D. Amazon EventBridge(Amazon CloudWatch Events) 스케줄링된 이벤트로 트리거된 Amazon EC2에서 실행되는 Amazon Elastic Container Service(Amazon ECS) 작업을 사용합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

가장 비용 효율적인 문제 요점.

**Amazon ECS(Amazon Elastic Container Service) Fargate**
Fargate는 Amazon EC2 인스턴스의 서버나 클러스터를 관리할 필요 없이 컨테이너를 실행하기 위해 Amazon ECS에 사용할 수 있는 기술임.
AWS Fargate를 사용하면 더 이상 컨테이너를 실행하기 위해 가상 머신의 클러스터를 프로비저닝, 구성 또는 조정할 필요가 없습니다. 따라서 서버 유형을 선택하거나, 클러스터를 조정할 시점을 결정하거나, 클러스터 패킹을 최적화할 필요가 없음.
Fargate 시작 유형을 사용하여 태스크와 서비스를 실행할 때는 애플리케이션을 컨테이너에 패키징하고, CPU 및 메모리 요구 사항을 지정한 다음, 네트워킹 및 IAM 정책을 정의하고, 애플리케이션을 시작.
각 Fargate 태스크에는 자체 격리 경계가 있으며 다른 태스크와 기본 커널, CPU 리소스, 메모리 리소스 또는 탄력적 네트워크 인터페이스를 공유하지 않.

A 탈락 ->  "EC2 예약 인스턴스"는 서버리스에 비해 비용 효율적이지 않아서 부적합.

B 탈락 -> 람다는 최대 15분 동안 작동하여 부적합.

C 정답 -> Fargate는 다른 옵션에 비해 서버가 없고 비용 효율적이라 적합(RPA 같네).

D 탈락 -> "Amazon EC2에서 실행" 비용 효율적이지 않아서 부적합.

</div>
</details>

<hr/>

## Prob. 50

비즈니스에서 AWS를 사용하여 설문 조사 웹 사이트를 호스팅하려고 합니다. 회사는 많은 양의 트래픽을 예상했습니다. 이 트래픽의 결과로 데이터베이스는 비동기식으로 업데이트됩니다. 조직은 AWS에 보관된 데이터베이스에 대한 쓰기 누락을 방지하기를 원합니다. (The organization want to avoid dropping writes to the database housed on AWS.)
이러한 데이터베이스 요청을 처리하려면 비즈니스 애플리케이션을 어떻게 작성해야 합니까?

A. Amazon Simple Notification Service(Amazon SNS) 항목에 게시하도록 응용 프로그램을 구성합니다. SNS 항목에 데이터베이스를 등록합니다.

B. Amazon Simple Notification Service(Amazon SNS) 항목에 가입하도록 응용 프로그램을 구성합니다. 데이터베이스 업데이트를 SNS 항목에 게시합니다.

C. 데이터베이스에 데이터를 쓸 리소스가 있을 때까지 데이터베이스 연결을 대기하려면 Amazon SQS(Simple Queue Service) FIFO 대기열을 사용합니다.

D. 쓰기를 캡처하고 데이터베이스에 쓸 때마다 대기열을 배출하려면 Amazon SQS(Simple Queue Service) FIFO 대기열을 사용합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

쓰기 누락을 방지 문제 요점.

Amazon SQS는 비동기식으로 데이터를 캡처하는 데 사용됩니다.
SNS는 한번 메시지를 밀어내면 회복력이 없기 때문에 정확하지 않습니다.

왜 C가 아니고 D입니까? 왜냐하면 소비자가 말이 안 되는 연결을 소비한다면.

A 탈락 -> DB가 알림 받는 항목에 게시하는 것과 응용 프로그램에 대한 SNS를 해도 회복력이 없어 부적합.

B 탈락 -> 응용 프로그램이 알림 받는 항목에 게시하는 것과 DB 업데이트에 대한 SNS를 해도 회복력이 없어 부적합.

C 탈락 -> 아마도 DB에 용량이 있을 때까지 SQS를 사용한다는 것 같은데 SQS의 장점은 메시지 보관인데 중요할 때 사용하지 않으니 쓰기에 대한 누락이 있을 수 있어 부적합.

D 정답 -> SQS는 비동기식으로 데이터를 캡처하는데 유용하기에 적합.

</div>
</details>

<hr/>

* Ref
  - [ExamTopics](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate-saa-c02/view/5)