---
layout: post
title: "[AWS-SAA] Examtopics 161~170"
subtitle: AWS
date: '2023-03-26 00:00:01 +0900'
category: study
tags: aws aws-saa
image:
  path: /assets/img/study_AWS/saa-co2_logo.png
---

SAA Examtopics 161~170번 문제를 풀어보자.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## Prob. 161

비즈니스는 두 개의 Amazon EC2 인스턴스를 사용하여 동적 웹 애플리케이션을 실행합니다. 조직에는 각 인스턴스에서 SSL 종료를 완료하는 데 사용되는 자체 SSL 인증서가 있습니다. 최근 트래픽이 증가하고 있으며, 운영팀은 SSL 암호화 및 복호화로 인해 웹 서버의 컴퓨팅 용량이 한도를 초과한다는 결론을 내렸습니다.

솔루션 설계자는 애플리케이션의 성능을 최적화하기 위해 무엇을 해야 합니까?

A. AWS 인증서 관리자(ACM)를 사용하여 새 SSL 인증서를 생성합니다. 각 인스턴스에 ACM 인증서를 설치합니다.

B. Amazon S3 버킷을 생성합니다. SSL 인증서를 S3 버킷으로 마이그레이션합니다. SSL 종료를 위해 버킷을 참조하도록 EC2 인스턴스를 구성합니다.

C. 프록시 서버로 다른 EC2 인스턴스를 만듭니다. SSL 인증서를 새 인스턴스로 마이그레이션하고 기존 EC2 인스턴스에 직접 연결하도록 구성합니다.

D. SSL 인증서를 AWS Certificate Manager(ACM)로 가져옵니다. ACM의 SSL 인증서를 사용하는 HTTPS 수신기를 사용하여 애플리케이션 로드 밸런서를 생성합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

성능을 최적화 문제 요점.

각 인스턴스에서 SSL 종료를 완료하는 데 사용되는 자체 SSL 인증서.
최근 트래픽이 증가하고 있으며, 운영팀은 SSL 암호화 및 복호화로 인해 웹 서버의 컴퓨팅 용량이 한도를 초과.

결국 SSL을 EC2에서 관리하여 용량적이나 성능적으로 문제가 있으니 이것을 관리해줄 서비스가 필요.

**AWS Certificate Manager**
AWS 서비스 및 연결된 리소스를 통해 SSL/TLS 인증서를 프로비저닝하고 관리.
AWS Certificate Manager(ACM)를 사용하면 AWS 서비스 및 연결된 내부 리소스에 사용할 공인 및 사설 SSL/TLS 인증서를 프로비저닝, 관리 및 배포할 수 있습니다. ACM은 SSL/TLS 인증서를 구매, 업로드 및 갱신하는 데 드는 시간 소모적인 수동 프로세스를 대신 처리.
웹 사이트 보호 및 보안/내부 리소스 보호/가동 시간 향상.
AWS Private CA/ELB/CF/API GW/Nitro Enclaves/CloudWatch(EventBridge).

Private CA(Private Certificate Authority) - 온프레미스 CA를 운영하는 데 드는 투자 및 유지 관리 비용 없이 루트 및 하위 CA를 비롯한 사설 CA 계층을 생성.
Nitro Enclaves - EC2 인스턴스 내 매우 민감한 데이터의 보호를 강화하도록 추가 격리 생성.

인증서 획득 프로세스를 간소화.
ACM 통합 서비스를 통해 무료 인증서를 사용.
관리형 인증서를 갱신.
인증서에 키 관리를 사용.
자체/공인/사설 SSL을 AWS로 가져올 수 있음.

A 탈락 -> 인증서를 관리해줄 서비스에서 새로운 것을 만들어 EC2에 설치하면 성능적으로는 같기에 부적합.

B 탈락 -> 인증서를 그냥 S3에 저장하면 보안적으로 부적합.

C 탈락 -> 프록시, 프록시 서버, 웹 프록시라고하는 정방향 프록시는 요청을 가로채고 중개자처럼 해당 클라이언트를 대신하여 웹 서버와 통신하기에 기관의 검색 제한을 피하기 위해/특정 콘텐츠에 대한 액세스를 차단/온라인에서 자신의 신원을 보호 등 기능으로 사용하여 부적합.

역방향 프록시는 웹 서버 앞에 위치하여 클라이언트 요청을 해당 웹 서버에 전달하고 부하 분산/전역 서버 부하 분산/공격으로부터 보호/캐싱/SSL 암호화 등의 기능으로 보안, 성능, 안정성을 향상.

D 정답 -> 자체 SSL 인증서를 ACM으로 이전하여 관리하며 이것을 사용하는 HTTPS 수신로 ALB를 사용하여 적합.

</div>
</details>

<hr/>

## Prob. 162

한 기업이 AWS Well-Architected 프레임워크를 사용하여 AWS에 배치된 기존 워크로드를 평가하고 있습니다. 평가 결과 다른 AWS 서비스를 지원하기 위해 새로 설치된 Microsoft Active Directory 도메인 컨트롤러와 동일한 Amazon EC2 인스턴스에서 작동하는 공개 웹 사이트를 발견했습니다. ( The evaluation discovered a public-facing website operating on the same Amazon EC2 instance as a freshly installed Microsoft Active Directory domain controller to support other AWS services.) 솔루션 설계자는 아키텍처의 보안을 강화하고 IT 작업자의 관리 부담을 줄이는 새로운 설계를 제공해야 합니다.

솔루션 설계자는 어떤 권장 사항을 제시해야 합니까?

A. AWS 디렉토리 서비스를 사용하여 관리되는 Active Directory를 생성합니다. 현재 EC2 인스턴스에서 Active Directory를 제거합니다.

B. 동일한 서브넷에 다른 EC2 인스턴스를 만들고 해당 인스턴스에 Active Directory를 다시 설치합니다. Active Directory를 제거합니다.

C. AWS 디렉터리 서비스를 사용하여 Active Directory 커넥터를 생성합니다. Proxy Active Directory는 현재 EC2 인스턴스에서 실행되고 있는 Active domain contorller에 요청합니다.

D. 현재 Active Directory 컨트롤러와 SAML(Security Assertion Markup Language) 2.0 연합을 사용하여 AWS SSO(Single Sign-On)를 사용하도록 설정합니다. EC2 인스턴스의 보안 그룹을 수정하여 Active Directory에 대한 공용 액세스를 거부합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

보안을 강화하고 IT 작업자의 관리 부담을 줄임 문제 요점.

AWS Well-Architected 프레임워크를 사용하여 AWS에 배치된 기존 워크로드를 평가.
새로 설치된 Microsoft Active Directory 도메인 컨트롤러와 공개 웹 사이트가 같은 EC2에서 작동하는 것을 발견.

**AWS Well-Architected Framework**
AWS Well-Architected Framework를 활용하면 AWS에서 시스템을 구축하면서 내리게 되는 결정의 장단점을 이해할 수 있습니다. 이 프레임워크를 통해 클라우드상의 안정적이고 안전하며 효율적이고 경제적인 시스템을 설계하고 운영하기 위한 설계 모범 사례.
아키텍처 관련 모범 사례를 사용해 학습, 측정 및 구축.
클라우드 설계자가 다양한 애플리케이션 및 워크로드를 위한 안전하고 고성능의 탄력적이며 효율적인 인프라를 구축할 수 있도록 지원.
운영 우수성, 보안, 안정성, 성능 효율성, 비용 최적화, 지속 가능성이라는 6가지 원칙을 중심으로 구축된 AWS Well-Architected는 고객과 파트너가 아키텍처를 평가하고 확장 가능한 설계를 구현할 수 있도록 일관된 접근 방식을 제공.
도메인별 렌즈, 핸즈온랩 및 AWS Well-Architected Tool이 포함.

**액티브 디렉토리(Active Directory, 이하 AD)**
마이크로소프트가 윈도우용 환경에서 사용하기 위해 개발한 LDAP 디렉터리 서비스의 기능.
기본적으로 AD는 사용자가 마이크로소프트 IT 환경에서 업무를 수행하는 데 도움을 주는 데이터베이스이자 서비스 집합.
LDAP -  사용자가 조직, 구성원 등에 대한 데이터를 찾는 데 도움이 되는 프로토콜입니다. LDAP는 LDAP 디렉터리에 데이터를 저장하고 사용자가 디렉터리에 액세스할 수 있도록 인증하기 위해 주로 사용.

데이터베이스(또는 디렉토리)는 환경에 대한 중요한 정보를 담음 - 데이터베이스에는 100명의 사용자 계정을 각 사용자의 직책, 전화번호, 비밀번호와 같은 세부정보와 함께 리스팅할 수 있습니다. 또한, 각 사용자의 권한도 기록하여 모든 사용자가 회사 복지 정보를 읽도록 허용하고, 금융 문서는 소수의 사람들만 보거나 수정하도록 허용.

서비스는 IT 환경에서 일어나는 대부분의 활동을 제어 - 사용자 ID와 비밀번호를 확인하는 방법으로, 사용자가 주장하는 본인이 맞는지 검증하고(인증), 각기 허용된 데이터에만 액세스할 수 있도록 승인.

AD 서비스인 AD DS(Active Directory Domain Services)는 윈도우 서버 운영체제의 기능으로 컴퓨터는 AD 환경의 일부이고 도메인 컨트롤러(Domain Controller, DC)가 실행시키는 서비스임.
각 DC에는 전체 도메인의 디렉토리 복사본/최신 상태를 유지.

AD는 온프레미스 마이크로소프트 환경 전용으로 클라우드의 마이크로소프트 환경은 온프레미스 AD와 같은 용도로 AWS AD.
별개지만 조직에 온프레미스 IT 환경과 클라우드 IT 환경이 혼재된 경우 일정 부분 연계해서 사용.

**AWS 디렉토리 서비스**
AWS Directory Service는 다른 AWS 서비스에서 Microsoft Active Directory(AD)를 사용할 수 있는 몇 가지 방법을 제공.
디렉터리는 사용자, 그룹 및 디바이스에 대한 정보를 저장하고, 관리자는 이를 사용하여 정보 및 리소스에 대한 액세스를 관리.

AWS Directory Service는 클라우드에서 기존 Microsoft AD 또는 LDAP (Lightweight Directory Access Protocol) 인식 애플리케이션을 사용하려는 고객에게 다양한 디렉터리 선택 옵션을 제공.
권한을 관리하기 위해 디렉터리가 필요한 개발자에게도 동일한 선택 옵션을 제공.
관리형 서비스로 관리 작업을 간소화/디렉터리 인식 워크로드 마이그레이션/온프레미스 보안 인증 통합/디렉터리 글로벌 확장.

A 정답 -> AWS 디렉토리 서비스를 사용하여 관리되는 Active Directory를 생성하고 현재 인스턴스를 제거할 수 있고 관리형 서비스를 사용하면 IT 직원의 관리 요구도 줄어들어 적합.

B 탈락 -> 다른 EC2를 만들고 다시 설치하면 직원의 관리 수요를 증가하여 부적합.

C 탈락 -> 프록시로 실제보다 앞에서 관리해주며 DC에 요청하여 AD DS를 실행시켜 사용하지만 보안적으로 향상시키지 않아 부적합.

Active Directory 커넥터는 ON-PREAM AD 전용으로 이미 클라우드에 존재.

D 탈락 -> SAML을 사용하여 SSO서비스와 연동하고 EC2의 보안 그룹을 수정하는 직원의 관리 수요를 증가하여 부적합.

</div>
</details>

<hr/>

## Prob. 163

Amazon Aurora는 최근 회사의 전 세계 전자 상거래 플랫폼을 위한 데이터 리포지토리로 선택되었습니다. 개발자가 광범위한 보고서를 실행할 때 전자 상거래 애플리케이션의 성능이 좋지 않음을 발견합니다. 월별 보고서를 수행할 때 솔루션 설계자는 ReadIOPS 및 CPU Utilization 메트릭이 급증하는 것을 확인합니다.

어떤 접근 방식이 가장 비용 효율적입니까?

A. 월간 보고를 Amazon Redshift로 마이그레이션합니다.

B. 월간 보고를 Aurora Replica로 마이그레이션합니다.

C. Aurora 데이터베이스를 더 큰 인스턴스 클래스로 마이그레이션합니다.

D. Aurora 인스턴스에서 프로비저닝된 IOPS를 높입니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

가장 비용 효율적 문제 요점.

전 세계 전자 상거래 플랫폼을 위한 데이터 리포지토리로 선택.
광범위한 보고서를 실행할 때 애플리케이션의 성능이 좋지 않음.
월별 보고서를 수행할 때 Read IOPS 및 CPU Utilization 메트릭이 급증.

오로라 Replica에는 두 가지 주요 목적이 있습니다. 쿼리를 실행하여 응용 프로그램의 읽기 작업 크기를 조정할 수 있습니다. 일반적으로 클러스터의 판독기 엔드포인트에 연결하여 이 작업을 수행합니다. 이렇게 하면 Aurora는 읽기 전용 연결에 대한 로드를 클러스터에 있는 것만큼 많은 Aurora 복제본에 분산시킬 수 있습니다. 또한 Aurora Replica는 가용성을 높이는 데 도움이 됩니다. 클러스터에서 작성기 인스턴스를 사용할 수 없는 경우, Aurora는 자동으로 독서기 인스턴스 중 하나를 새 작성기로 승격합니다.

A 탈락 -> Amazon Redshift는 데이터 테이블에 있는 것을 분석하고 예측하고 공유하고 인텔리전스 최적화로 만들어주는 웨어하우징 기술로 S3의 데이터 레이크에 대해 쿼리할 수 있는 Spectrum기능과 QuickSight로 인텔리전스를 시각화하여 보여주는 것이라 부적합.

B 정답 -> 복제본으로 쿼리 성능과 가용성을 높여주는 기술로 싸고 적합.

C 탈락 -> 더 큰 클래스는 용량을 말하는 것 같은데 용량이 커져도 성능은 같아 부적합.

D 탈락 -> 프로비저닝된 IOPS를 높게 설정하는데 Read를 대상으로 하기에 Read 복제본이 더 적합하여 부적합.

</div>
</details>

<hr/>

## Prob. 164

기업의 백업 데이터는 총 700TB이며 데이터 센터의 NAS(Network Attached Storage)에 보관됩니다. 이 백업 데이터는 규제 관련 문의가 있을 경우 사용할 수 있어야 하며 7년 동안 보존해야 합니다. 조직은 백업 데이터를 온프레미스 데이터 센터에서 Amazon Web Services(AWS)로 재배치하기로 결정했습니다. 한 달 이내에 마이그레이션을 완료해야 합니다. 회사의 공용 인터넷 연결은 500Mbps의 데이터 전송 전용 용량을 제공합니다.

가장 낮은 비용으로 데이터를 마이그레이션하고 저장하기 위해 솔루션 설계자는 무엇을 해야 합니까?

A. AWS Snowball 장치를 주문하여 데이터를 전송합니다. 수명 주기 정책을 사용하여 파일을 Amazon S3 Glacier Deep Archive로 전환합니다.

B. 데이터 센터와 Amazon VPC 간에 VPN 연결을 배포합니다. AWS CLI를 사용하여 사내에서 Amazon S3 Glacier로 데이터를 복사합니다.

C. 500Mbps AWS Direct Connect 연결을 프로비저닝하고 데이터를 Amazon S3로 전송합니다. 수명 주기 정책을 사용하여 파일을 Amazon S3 Glacier Deep Archive로 전환합니다.

D. AWS DataSync를 사용하여 데이터를 전송하고 사내에서 DataSync 에이전트를 배포합니다. DataSync 작업을 통해 사내 NAS 스토리지에서 Amazon S3 Glacier로 파일을 복사할 수 있습니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

가장 낮은 비용으로 데이터를 마이그레이션하고 저장 문제 요점.

백업 데이터는 데이터 센터의 NAS에 보관.
규제 관련 문의가 있을 경우 사용할 수 있어야 하며 7년 동안 보존.
온프레미스 -> AWS 재배치하기로 결정.

VPN/Direct Connect/Transit GW - 온프레미스와 VPC를 연결 
Storage GW 연동 - 스토리지에 연결하여 해당 데이터를 사용.
DataSync 이동(마이그레이션) - 스토리지 자체를 옮김.

A 정답 -> Snowball 장치를 받아 데이터를 수집하고 AWS에 다시 보내어 7년 동안 보관해야하기에 글래시어 딥 아카이브가 적합.

B 탈락 -> VPN 연결은 온프레미스와 클라우드와 연동하는 기술로 부적합.

C 탈락 -> Direct Connect 연결은 온프레미스와 클라우드와 연동하는 기술로 부적합.

D 탈락 -> DataSync는 이동에 대한 서비스이지만 S3 Glacier로 부적합.

</div>
</details>

<hr/>

## Prob. 165

기업의 주요 데이터 센터와 보조 데이터 센터는 500마일(804.7km) 떨어져 있으며 고속 광섬유 케이블로 연결되어 있습니다. 미션 크리티컬 워크로드의 경우 조직은 데이터 센터와 AWS VPC 간에 가용성이 높고 안전한 네트워크 링크가 필요합니다. 솔루션 설계자는 최대한 탄력적인 연결 솔루션을 선택해야 합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. 기본 데이터 센터에서 두 개의 AWS Direct Connect 연결이 두 개의 개별 장치에서 두 개의 Direct Connect 위치에서 종료됩니다.

B. 기본 및 보조 데이터 센터의 단일 AWS Direct Connect 연결이 동일한 디바이스의 한 Direct Connect 위치에서 종료됩니다.

C. 기본 및 보조 데이터 센터 각각에서 두 개의 AWS Direct Connect 연결이 두 개의 개별 장치에서 두 개의 Direct Connect 위치에서 종료됩니다.

D. 각 기본 및 보조 데이터 센터의 단일 AWS Direct Connect 연결이 두 개의 개별 장치에 있는 하나의 Direct Connect 위치에서 종료됩니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

최대한 탄력적인 연결 솔루션 문제 요점.

주요 데이터 센터와 보조 데이터 센터가 고속 광섬유 케이블로 연결.
데이터 센터와 AWS VPC 간에 가용성이 높고 안전한 네트워크 링크가 필요.

토폴로지 - 컴퓨터 네트워크의 요소들(링크, 노드 등)을 물리적으로 연결해 놓은 것, 또는 그 연결 방식.

둘 이상의 위치에 있는 개별 장치에서 종료되는 개별 연결을 통해 최대 복원력을 얻을 수 있습니다. 이 구성은 고객에게 장애에 대한 최대 복원력을 제공합니다. 위 그림에서 보듯이 이러한 토폴로지는 장치 장애, 연결 장애 및 전체 위치 장애에 대한 복원력을 제공합니다. AWS Direct Connect 게이트웨이를 사용하여 AWS Direct Connect 위치에서 AWS 지역(중국의 AWS 지역 제외)에 액세스할 수 있습니다.

A 탈락 -> 두 장치에 기본 데이터 센터에만 두 개의 연결을 하여 부적합.

B 탈락 -> 단일 장치에 각각 데이터 센터가 단일 연결을 하여 부적합.

C 정답 -> 두 장치에 각각 데이터 센터에 두 개의 연결 하여 복원력 있어 적합.

D 탈락 -> 두 장치에 각각 데이터 센터에 단일 연결을 하여 부적합.

</div>
</details>

<hr/>

## Prob. 166

비즈니스의 동적 웹 사이트는 미국 내에서 호스팅됩니다. 이 회사는 유럽 전역으로 확장하고 있으며 새로운 유럽 방문자를 위해 사이트 로딩 속도를 줄이기를 원합니다. 웹사이트의 백본은 미국에 있어야 합니다. 이제 며칠 후면 제품이 출시될 예정인데, 즉석 답변이 필요합니다.

솔루션 설계자는 어떤 권장 사항을 제시해야 합니까?

A. us-east-1에서 Amazon EC2 인스턴스를 시작하고 해당 인스턴스로 사이트를 마이그레이션합니다.

B. Amazon S3로 웹 사이트를 이동합니다. 영역 간에 교차 영역 복제를 사용합니다.

C. 온프레미스 서버를 가리키는 사용자 지정 오리진에서 Amazon CloudFront를 사용합니다.

D. 온프레미스 서버를 가리키는 Amazon Route 53 지역근접 라우팅 정책을 사용합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 :

새로운 유럽 방문자를 위해 사이트 로딩 속도를 줄이기를 원함 문제 요점.

동적 웹 사이트는 미국 내에서 호스팅.
유럽 전역으로 확장.
백본은 미국에 있어야 함(이동 불가).

Amazon CloudFront는 정적 및 동적 컨텐츠의 원래 최종 버전을 보관하는 모든 오리진 서버와 함께 작동합니다. 커스텀 오리진 이용 시 추가 요금이 부과되지 않습니다.

**Amazon S3 CRR(교차 리전 복제)**
S3 CRR(교차 리전 복제)을 사용하면 객체(객체의 메타데이터와 객체 태그 포함)를 다른 AWS 리전에 복제할 수 있으므로, 지연 시간 최소화, 규정 준수, 보안, 재해 복구 및 기타 용도로 사용.

**라우팅 정책**
* 단순 라우팅 정책(Simple routing policy) - 도메인에 대해 특정 기능을 수행하는 하나의 리소스만 있는 경우 사용.
* 장애 조치 라우팅 정책(Failover routing policy) - 액티브-패시브 장애 조치를 구성하려는 경우에 사용.
* 지리 위치 라우팅 정책(Geolocation routing policy) - 사용자의 위치에 기반하여 트래픽을 라우팅.
* 지리 근접 라우팅 정책(Geoproximity routing policy) - 리소스의 위치를 기반으로 트래픽을 라우팅.
* 지연 시간 라우팅 정책 - 여러 AWS 리전에 리소스가 있고 최상의 지연 시간을 제공하는 리전으로 트래픽을 라우팅.
* IP 기반 라우팅 정책 - 사용자의 위치에 기반하여 트래픽을 라우팅하고 트래픽이 시작되는 IP 주소가 있는 경우.
* 다중 응답 라우팅 정책(Multivalue answer routing policy) -  Route 53이 DNS 쿼리에 무작위로 선택된 최대 8개의 정상 레코드로 응답하게 하려는 경우.
* 가중치 기반 라우팅 정책(Multivalue answer routing policy) - 사용자가 지정하는 비율에 따라 여러 리소스로 트래픽을 라우팅.

A 탈락 -> 마이그레이션은 데이터 자체 이동으로 부적합.

B 탈락 -> 지역 간에 교차 영역 복제로 단순히 복제만 한다고 끝나는게 아니고 추가 설정을해야 해서 부적합.

C 정답 -> 세계적으로 컨텐츠를 엣지 로케이션에 캐싱하여 속도를 줄여 적합.

D 탈락 -> 리소스의 위치를 기반으로 라우팅해주는 정책으로 유럽에 라우팅해주기 때문에 똑같아 부적합.

</div>
</details>

<hr/>

## Prob. 167

한 기업에서 AWS Direct Connect 연결을 사용하여 코로케이션 시설에서 us-east-1 리전의 Amazon S3 버킷으로 1PB의 데이터를 복사했습니다. 이제 비즈니스는 us-west-2 리전에 있는 다른 S3 버킷에 데이터를 복제하려고 합니다. AWS Snowball은 코로케이션 시설에서 허용되지 않습니다.

솔루션 설계자는 이를 달성하기 위한 수단으로 무엇을 제안해야 합니까?

A. Snowball Edge 장치를 주문하여 한 영역에서 다른 영역으로 데이터를 복사합니다.

B. S3 콘솔을 사용하여 소스 S3 버킷에서 대상 S3 버킷으로 콘텐츠를 전송합니다.

C. AWS S3 sync 명령을 사용하여 소스 버킷에서 대상 버킷으로 데이터를 복사합니다.

D. 영역 간 복제 구성을 추가하여 서로 다른 영역의 S3 버킷에 개체를 복사합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

us-west-2 리전에 있는 다른 S3 버킷에 데이터를 복제 문제 요점.

코로케이션 시설에서 us-east-1 리전의 Amazon S3 버킷으로 데이터를 복사.
AWS Snowball은 불가. 

코로케이션 - 고객님의 서버를 내부에서 관리하지 않고 데이터센터에 위탁하여 초고속인터넷 백본망에서 고객의 서버와 통신장비를 직접 연결하고 관리해 주는 서비스.

A 탈락 -> 코로케이션에서 Snowball는 사용 불가하여 부적합.

B 탈락 -> 전송할 것이면 DataSync를 사용하야하며 전송이 아니라 복제 해야하여 부적합.

C 탈락 -> Sync는 아주 큰 데이터의 전송(PB 단위)의 경우 타임아웃이 일어날 수 있어 부적합.

D 정답 -> Cross region replication은 일반적으로 새 버킷을 대상으로만 가능하나, AWS Support에 문의시 존재하는 버킷을 대상으로도 사용 가능하여 적합.

</div>
</details>

<hr/>

## Prob. 168

솔루션 설계자는 Amazon DynamoDB에 대한 API 요청이 VPC 내부의 Amazon EC2 인스턴스로부터의 인터넷을 통해 라우팅되지 않는지 확인해야 합니다.

이를 달성하기 위한 솔루션 설계자의 역할은 무엇입니까? (2개를 선택하세요.)

A. 엔드포인트에 대한 경로 테이블 엔트리를 만듭니다.

B. DynamoDB에 대한 게이트웨이 엔드포인트를 만듭니다.

C. 엔드포인트를 사용하는 새 DynamoDB 테이블을 만듭니다.

D. VPC의 각 서브넷에 엔드포인트에 대한 ENI를 생성합니다.

E. 기본 Security Group에 Security Group 항목을 만들어 액세스 권한을 제공합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A, B

해설 : 

인터넷을 통해 라우팅되지 않는지 확인 문제 요점.

Amazon DynamoDB에 대한 API 요청이 VPC 내부의 Amazon EC2 인스턴스.

Amazon DynamoDB 및 Amazon S3는 인터페이스 엔드포인트이 아닌 게이트웨이 엔드포인트을 지원합니다.<br>
게이트웨이 엔드포인트을 사용하여 VPC에 엔드포인트을 생성하고 서비스에 대한 액세스를 허용하는 정책을 연결합니다.<br>
그런 다음 경로 테이블 항목을 만들 경로 테이블을 지정하십시오.

A 정답 -> EC2에서 엔드포인트로 라우팅하게 라우트 테이블 엔트리 만듬 적합.

B 정답 -> 게이트웨이 엔드포인트로 인터넷보다 싸고 안전하게 연결 적합.

C 탈락 -> 이미 사용중인 DB에 연결할 수 있어서 새로운 것은 부적합.

D 탈락 -> 엔드포인트에 대한 ENI가 아니고 게이트웨이를 만들어야 해서 부적합.

ENI는 서로 다른 VPC간의 연결 인터페이스 엔드포인트 -> 사설 링크 -> 서비스.

E 탈락 -> 보안 그룹은 IP를 보호하는 것으로 상관없어 부적합.

</div>
</details>

<hr/>

## Prob. 169 

비즈니스 애플리케이션은 Elastic Load Balancer 뒤에 있는 Auto Scaling 그룹의 일부인 Amazon EC2 인스턴스에서 호스팅됩니다. 회사는 매년 애플리케이션 기록을 기반으로 휴일 동안 트래픽 증가를 예측합니다. 솔루션 설계자는 애플리케이션 사용자의 성능에 미치는 영향을 최소화하기 위해 Auto Scaling 그룹이 사전에 용량을 늘리도록 보장하는 계획을 개발해야 합니다.

어떤 솔루션이 이러한 기준을 충족할까요?

A. CPU 활용률이 90%를 초과할 경우 EC2 인스턴스를 확장하려면 Amazon CloudWatch 경보를 생성합니다.

B. 수요가 가장 많은 예상 기간 전에 자동 스케일링 그룹을 확장하는 반복 예약 작업(recurring scheduled action)을 만듭니다.

C. 최대 수요 기간 동안 자동 스케일링 그룹에서 EC2 인스턴스의 최소 및 최대 수를 늘립니다.

D. EC2_INSTANCE_LAUNCH 이벤트의 자동 확장이 있을 때 경고를 보내도록 Amazon Simple Notification Service(Amazon SNS) 알림을 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

Auto Scaling 그룹이 사전에 용량을 늘리도록 보장하는 계획 문제 요점.

ELB -> Auto Scaling 클러스터(그룹)의 일부 EC2에서 호스팅 -> 비즈니스 앱.
매년 애플리케이션 기록을 기반으로 휴일 동안 트래픽 증가를 예측.
애플리케이션 사용자의 성능에 미치는 영향을 최소화.

예정된 이벤트에 대한 사전 대처로는 반복 예약(scheduled) 작업이 적절하다.

조정 정책을 지정했다면 Amazon EC2 Auto Scaling에서는 애플리케이션의 늘어나거나 줄어드는 수요에 따라 인스턴스를 시작하거나 종료할 수 있습니다. 예를 들어, 다음 오토 스케일링의 경우 최소 인스턴스 수 1개, 원하는 인스턴스 용량 2개, 최대 인스턴스 수 4개가 됩니다.
Minimum size/Desired capacity/Scale out as needed = Maximum size

A 탈락 -> 확장하려면 경보를 하는게 아니고 Events(EventBridge)로 람다 함수를 호출해 자동 스케일링하게 해야하여 부적합.

B 정답 -> 휴일동안 다음주에 트래픽 증가를 예측하여 반복 예약 작업으로 확장하여 적합.

C 탈락 -> 자동 스케일링 그룹에서 EC2의 최소/최대수를 직접 늘려서 부적합.

D 탈락 -> 자동 확장이 있을 때 SNS로 알림을 받는다는 것은 주제와 상관없어 부적합.

</div>
</details>

<hr/>

## Prob. 170

비즈니스에서 라이브 데이터 세트를 온프레미스 NFS 서버에서 DOC-EXAMPLE-BUCKET이라는 Amazon S3 버킷으로 온라인으로 마이그레이션하려고 합니다. 데이터 무결성 검증은 전송 중과 전송 후에 모두 필수적입니다. 또한 데이터를 암호화해야 합니다.
솔루션 설계자가 AWS 솔루션을 사용하여 데이터를 마이그레이션하고 있습니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. AWS Storage Gateway file gateway

B. S3 Transfer Acceleration

C. AWS DataSync

D. AWS Snowball Edge Storage Optimized

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

데이터를 마이그레이션 문제 요점.

온프레미스 NFS 서버에서 라이브 데이터 세트를 Amazon S3 버킷으로 온라인으로 마이그레이션.
데이터 무결성 검증.
데이터를 암호화.

**Amazon S3 Transfer Acceleration**
Amazon S3 Transfer Acceleration은 클라이언트와 S3 버킷 간의 장거리 파일 전송을 파일을 빠르고 쉽고 안전하게 전송할 수 있는 버킷 수준 기능.
Transfer Acceleration은 전 세계에서 S3 버킷으로 전송 속도를 최적화하도록 설계.
Transfer Acceleration은 Amazon CloudFront에서 전 세계에 분산된 엣지 로케이션을 활용.
엣지 로케이션에 도착한 데이터는 최적화된 네트워크 경로를 통해 Amazon S3로 라우팅.
추가 데이터 전송 요금이 적용일수도.

DataSync는 마이그레이션용이고 Storage Gateway는 통합용입니다.

A 탈락 -> Storage Gateway는 온프레미스와 클라우드의 스토리지를 연동/통합용으로 백업용이라 부적합.

B 탈락 -> Transfer Acceleration는 데이터를 클라이언트에게 빨리 제공하기 위한 서비스이지 마이그레이션이 아니여서 부적합.

C 정답 -> DataSync는 데이터를 온프레미스에서 클라우드로 이동(마이그레이션)시키기 적합.

D 탈락 -> Snowball은 온라인이 아니고 오프라인으로 장치를 보내 그곳에 데이터를 담고 AWS로 보내어 마이그레이션하여 부적합.

</div>
</details>

<hr/>

* Ref
  - [ExamTopics](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate-saa-c02/view/17)