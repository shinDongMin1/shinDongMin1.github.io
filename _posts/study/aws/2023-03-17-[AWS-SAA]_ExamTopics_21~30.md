---
layout: post
title: "[AWS-SAA] Examtopics 21~30"
subtitle: AWS
date: '2023-03-17 00:00:01 +0900'
category: study
tags: aws aws-saa
image:
  path: /assets/img/study_AWS/saa-co2_logo.png
---

SAA Examtopics 21~30번 문제를 풀어보자. <br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## Prob. 21

관리는 예산 계획 프로세스의 일부로 사용자별로 분류된 AWS 청구 항목 요약이 필요합니다. 부서에 대한 예산은 데이터를 사용하여 생성됩니다. 솔루션 설계자는 이 보고서 데이터를 얻는 가장 효과적인 방법을 확인해야 합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. Amazon Athena에서 쿼리를 실행하여 보고서를 생성합니다.

B. 비용 탐색기에서 보고서를 만들고 보고서를 다운로드합니다.

C. 청구 대시보드에서 청구서 세부 정보에 액세스하고 청구서를 다운로드합니다.

D. AWS Budgets에서 Amazon Simple Email Service(Amazon SES)를 사용하여 경고하도록 비용 예산을 수정합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

A -> Amazon Athena는 표준 SQL을 사용하여 Amazon S3(Amazon Simple Storage Service)에 있는 데이터를 직접 간편하게 분석할 수 있는 대화형 쿼리 서비스임.
관리할 필요 없이 Apache Spark를 사용함.

B -> 비용 탐색기(AWS Cost Explorer)는 비용 및 사용량을 보고 분석할 수 있게 해주는 도구로 기본 리포트를 제공하지만 리포트를 생성하는 데 사용되는 필터 및 제약 조건을 변경할 수도 있음.
비용 탐색기는 사용자가 만든 리포트를 저장하는 방법도 제공.
책갈피로 저장하거나 CSV 파일을 다운로드하거나 보고서로 저장할 수 있음.

C -> AWS Billing 콘솔의 대시보드 페이지를 사용하여 AWS 지출에 대한 일반적인 정보와 지출 추세를 확인.
세부 정보를 보려면, 왼쪽 탐색 창에서 청구 세부 정보(Billing details)를 선택.
Cost Explorer를 사용하지 않고도 AWS 비용을 볼 수 있음.

D -> AWS Budgets를 사용하면 사용자 지정 예산을 설정하여 비용 및 사용량을 추적하고, 임계값 초과 시 이메일 또는 SNS 알림에서 수신된 알림에 빠르게 대응할 수 있음.
하지만 문제에서는 AWS 청구 항목 요약 보고서가 필요해보임.

</div>
</details>

<hr/>

## Prob. 22

솔루션 설계자는 클라이언트 사례 파일을 보관하기 위한 시스템을 만들어야 합니다. 파일은 중요한 기업 자산입니다. 파일 수는 시간이 지남에 따라 증가합니다. Amazon EC2 인스턴스에서 실행되는 여러 애플리케이션 서버는 파일에 동시에 액세스할 수 있어야 합니다. 솔루션에는 기본 제공 중복성이 있어야 합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. Amazon EFS(Amazon Elastic File System)

B. 아마존 엘라스틱 블록 스토어 (Amazon EBS)

C. Amazon S3 Glacier Deep Archive

D. AWS 백업

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A (and B) 중복 정답

해설 : 

A -> Amazon Elastic File System(EFS)은 완전히 탄력적인 서버리스(온디맨드/오토스케일링) 파일 스토리지를 제공하며 파일을 추가하고 제거할 때 자동으로 확장되고 축소되며 관리 또는 프로비저닝이 필요하지 않음.
EFS는 동시성을 지원하여 파일 데이터를 공유되기 때문에 답은 A.

B -> 하지만 이 문제는 Amazon EBS Multi-Attach 가 업데이트되기 전에 나온 문제같다는 의견이 있음.

다음은 Multi-Attach에 대한 설명으로
    Amazon EBS Multi-Attach를 사용하면 동일한 가용성 영역에 있는 여러 인스턴스에 단일 Provisioned IOPS SSD(i1 또는 io2) 볼륨을 연결할 수 있습니다. 여러 다중 연결 사용 볼륨을 인스턴스 또는 인스턴스 집합에 연결할 수 있습니다. 볼륨이 연결된 각 인스턴스에는 공유 볼륨에 대한 전체 읽기 및 쓰기 권한이 있습니다. Multi-Attach를 사용하면 동시 쓰기 작업을 관리하는 클러스터된 리눅스 애플리케이션에서 애플리케이션 가용성을 높일 수 있습니다.

C, D -> 둘다 파일에 동시에 액세스에 대한 내용이 아님.

</div>
</details>

<hr/>

## Prob. 23

기업은 직원에게 기밀 및 민감한 데이터에 대한 보안 액세스를 제공해야 합니다. 회사는 승인된 개인만 데이터에 액세스할 수 있도록 보장하기를 원합니다. 데이터는 작업자의 장치에 안전하게 다운로드되어야 합니다. 파일은 온프레미스 Windows 파일 서버에 보관됩니다. 그러나 원격 트래픽이 증가함에 따라 파일 서버의 용량이 고갈되고 있습니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. 파일 서버를 공용 서브넷의 Amazon EC2 인스턴스로 마이그레이션합니다. 인바운드 트래픽을 직원의 IP 주소로 제한하도록 보안 그룹을 구성합니다.

B. 파일을 Amazon FSX for 윈도우즈 File Server 파일 시스템으로 마이그레이션합니다. Amazon FSX 파일 시스템을 사내 Active Directory와 통합합니다. AWS 클라이언트 VPN을 구성합니다.

C. 파일을 Amazon S3로 마이그레이션하고 전용 VPC 엔드포인트를 생성합니다. 서명된 URL을 만들어 다운로드를 허용합니다.

D. 파일을 Amazon S3로 마이그레이션하고 공용 VPC 엔드포인트를 생성합니다. 직원이 AWS Single Sign-On으로 로그온할 수 있도록 허용합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

A -> 인바운드 트래픽(inbound traffic)은 외부에서 가상서버 내부로 데이터가 유입될때 발생하는 트래픽으로 직원 IP 주소로 제한만 한다고 승인되지 않는 개인에 대한 보안이 불가능.

B -> Amazon FSx는 Microsoft Windows Server에 구축된 완전관리형 파일 스토리지를 통해 광범위한 엔터프라이즈 Windows 워크로드를 지원.
Windows 파일 시스템 기능을 기본적으로 지원하며 네트워크를 통해 파일 스토리지에 액세스할 수 있는 서버 메시지 블록(SMB) 프로토콜도 지원.
AWS 클라우드기본, Windows 호환성, 엔터프라이즈 성능 및 기능, 일관된 밀리초 미만의 지연 시간을 제공에 최적화.

    Windows 파일 서버가 온프레미스이므로 데이터를 클라우드에 복제할 수 있는 방법이 필요하므로 Windows 파일 서버용 AWS FSx만 선택할 수 있습니다. 또한, 정보는 기밀이므로 적절한 사용자가 안전한 방법으로 정보에 액세스할 수 있도록 하고 싶습니다.

Windows file server + AD => FSx
AD - LDAP(Lightweight Directory Access Protocol) 디렉터리 서비스의 기능이다. 주 목적은 윈도우 기반의 컴퓨터들을 위한 인증 서비스를 제공
LDAP - 사용자가 조직, 구성원 등에 대한 데이터를 찾는 데 도움이 되는 프로토콜

"Windows 파일 시스템"이 사용됩니다. Windows 파일 서버용 S3와 FSX 사이에서 FSX는 기존 on-prem 파일 시스템을 더 잘 대체합니다. --> A와 B로 제한
보안 그룹(A)을 통한 IP 화이트리스트는 직원 공용 IPv4가 변경되거나 디바이스가 손상될 수 있으므로 위험하여
보안 인증 시스템(B)을 사용하는 것이 더 안전함.

C, D -> VPC 엔드포인트를 통해 인터넷 게이트웨이, NAT 디바이스, VPN 연결 또는 AWS Direct Connect 연결이 필요 없이 Virtual Private Cloud(VPC)와 지원 서비스 간에 연결을 설정할 수 있음 따라서 VPC에서 연결할 수 있는 특정 API 엔드포인트, 사이트 및 서비스를 제어.
VPC 엔드포인트는 가상 디바이스입니다. 수평으로 확장된 고가용성 중복 VPC 구성 요소.(인터페이스/GLB/게이트웨이)

S3 Signed URL - 기본적으로 모든 S3 객체는 프라이빗입니다. 객체 소유자만 액세스 권한.
그러나 객체 소유자는 선택적으로 시간 제한 권한을 부여하기 위해 자체 보안 자격 증명을 사용하여 미리 서명된 URL 객체를 다운로드.
서명된 URL을 생성할 때 보안을 제공해야 해서 자격 증명을 지정한 다음 버킷 이름, 객체 키, HTTP 메서드(GET 객체 다운로드), 만료 날짜 및 시간을 입력해야지만 미리 서명된 URL만 유효함.

SSO - Single Sign-On(SSO)은 1회 사용자 인증으로 다수의 애플리케이션 및 웹사이트에 대한 사용자 로그인을 허용하는 인증 솔루션.


</div>
</details>

<hr/>

## Prob. 24

법률 회사는 대중과 소통해야 합니다. 수백 개의 파일에 공개적으로 액세스할 수 있어야 합니다. 누구든지 지정된 미래 날짜 이전에 파일을 수정하거나 삭제할 수 없습니다.

가능한 가장 안전한 방법으로 이러한 기준을 충족하는 솔루션은 무엇입니까?

A. 정적 웹 사이트 호스팅을 위해 구성된 Amazon S3 버킷에 모든 파일을 업로드합니다. 지정된 날짜까지 S3 버킷에 액세스하는 모든 AWS 주체에 읽기 전용 IAM 사용 권한을 부여합니다.

B. S3 Versioning을 사용하도록 설정된 새 Amazon S3 버킷을 생성합니다. S3 Object Lock을 지정된 날짜에 따라 보존 기간과 함께 사용합니다. 정적 웹 사이트 호스팅을 위해 S3 버킷을 구성합니다. 개체에 대한 읽기 전용 액세스를 허용하도록 S3 버킷 정책을 설정합니다.

C. S3 Versioning을 사용하도록 설정된 새 Amazon S3 버킷을 생성합니다. 개체 수정 또는 삭제 시 AWS 람다 기능을 실행하도록 이벤트 트리거를 구성합니다. 개체를 전용 S3 버킷의 원래 버전으로 바꾸도록 람다 기능을 구성합니다.

D. 정적 웹 사이트 호스팅을 위해 구성된 Amazon S3 버킷에 모든 파일을 업로드합니다. 파일이 들어 있는 폴더를 선택하십시오. S3 Object Lock은 지정된 날짜에 따라 보존 기간과 함께 사용합니다. S3 버킷에 액세스하는 모든 AWS 주체에 읽기 전용 IAM 사용 권한을 부여합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

S3 Versioning - Amazon S3의 버전 관리는 객체의 여러 변형을 동일한 버킷에 보관하는 수단.
S3 버전 관리 기능을 사용하여 모든 버전을 보존, 검색 및 복원.

S3 Object Lock - S3 객체 잠금을 사용하면 write-once-read-many(WORM) 모델을 사용하여 객체를 저장.
객체 잠금은 고정된 시간 동안 또는 무기한으로 객체의 삭제 또는 덮어쓰기를 방지하는 데 도움.

A, D -> 다수를 위한 읽기 전용 액세스는 버킷 정책으로 구현해야 함.
버킷을 생성하는 동안 개체 잠금이 사용하도록 설정된 새 버킷을 생성해야 함.
기존 버킷(옵션 D의 경우처럼)에 대해 개체 잠금을 사용할 수 없음.

또한 Object lock이 활성화된 상태에서 새 버킷을 생성하려고 했는데 다음 메시지가 표시.
"개체 잠금이 활성화되어 있으면 버킷 버전 관리를 비활성화할 수 없습니다."
즉, 새 버킷을 생성해야 합니다(버전링이 자동으로 활성화됨).

또한 IAM 권한이 아니라 버킷 정책일 수 있으므로 제외.

B -> S3 Versioning로 설정된 S3 생성 후 Object Lock으로 객체를 관리해주며 버킷 정책으로 객체는 읽기만 가능해서 조건을 안전하게 충족함.

C -> B와 같이 S3를 생성하지만 AWS 람다 기능으로 변경되면 버전 관리함.

</div>
</details>

<hr/>

## Prob. 25

기업은 10Gbps AWS Direct Connect 연결을 통해 온프레미스 서버를 AWS에 연결합니다. 연결의 작업 부하가 중요합니다. 조직에는 기존 연결 대역폭을 최소화하면서 최대한 탄력적인 재해 복구 접근 방식이 필요합니다.

솔루션 설계자는 어떤 권장 사항을 제시해야 합니까?

A. 다른 AWS 영역에 새 Direct Connect 연결을 설정합니다.

B. 다른 AWS 영역에 새 AWS 관리 VPN 연결을 설정합니다.

C. 두 개의 새 직접 연결(현재 AWS 영역과 다른 영역에 하나씩)을 설정합니다.

D. AWS 관리 VPN 연결 두 개를 새로 설정합니다. 하나는 현재 AWS 영역에 있고 다른 하나는 다른 영역에 있습니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

두 가지 키워드는 "대역폭"과 "재해 복구"입니다. 
한 영역에 2개의 서로 다른 연결이 있으면 최대 탄력성(maximum resiliency)이 보장.
서로 다른 영역에 연결하면 재해 복구가 포함.
동일한 영역에 새 연결이 있으면 연결 로드를 공유하므로 기존 연결에서 "트래픽 대역폭"이 감소.

A -> 재해 복구 가능 / 트래픽 대역폭 감소 2
B -> 재해 복구 가능 / 트래픽 대역폭 감소 1
C -> 재해 복구 가능 / 트래픽 대역폭 감소 3
D -> 재해 복구 가능 / 트래픽 대역폭 감소 1 / 최대 탄력성

</div>
</details>

<hr/>

## Prob. 26

기업에는 관리 및 프로덕션(운영)이라는 레이블이 붙은 두 개의 가상 사설 클라우드(VPC)가 있습니다. 관리 VPC는 ​​고객 게이트웨이를 통해 VPN을 사용하여 데이터 센터의 단일 장치에 연결합니다. 프로덕션 VPC는 ​​가상 프라이빗 게이트웨이를 통해 두 개의 AWS Direct Connect 연결을 통해 AWS에 연결됩니다. 관리 및 프로덕션 VPC는 ​​모두 단일 VPC 피어링 연결을 통해 서로 통신합니다.

아키텍처의 단일 실패 지점을 최소화하기 위해 솔루션 설계자는 무엇을 해야 합니까?

A. 관리 VPC와 운영 VPC 사이에 VPN 집합을 추가합니다.

B. 두 번째 가상 프라이빗 게이트웨이를 추가하고 관리 VPC에 연결합니다.

C. 두 번째 고객 게이트웨이 디바이스에서 Management VPC에 두 번째 VPN 집합을 추가합니다.

D. 관리 VPC와 운영 VPC 사이에 두 번째 VPC 피어링 연결을 추가합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

단일 실패 지점을 최소화가 문제 요점.

A 탈락 -> VPC 피어링에 대해 "통신에 대한 단일 장애 지점 또는 대역폭 병목 현상이 없습니다." 따라서 VPC 피어링이 이미 설치되어 있으면 이중화 메커니즘을 생성할 필요가 없음.
https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html

B 탈락 -> "VPC에 가상 프라이빗 게이트웨이를 한 번에 하나씩 연결할 수 있습니다."
https://docs.aws.amazon.com/vpn/latest/s2svpn/vpn-limits.html

C 정답 -> "고객 게이트웨이 디바이스를 사용할 수 없게 될 경우 연결이 끊어지는 것을 방지하기 위해 두 번째 고객 게이트웨이 디바이스를 사용하여 VPC 및 가상 프라이빗 게이트웨이에 대한 두 번째 사이트 간 VPN 연결을 설정할 수 있습니다."
https://docs.aws.amazon.com/vpn/latest/s2svpn/vpn-redundant-connection.html

D 탈락 -> VPC 한 쌍당 VPC 피어링을 하나만 가질 수 있음. "VPC 피어링 연결은 두 VPC 간의 일대일 관계입니다."
VPC https://docs.aws.amazon.com/vpc/latest/peering/vpc-peering-basics.html

</div>
</details>

<hr/>

## Prob. 27

AWS는 회사의 거의 실시간 스트리밍 애플리케이션을 호스팅합니다. 데이터가 수집되는 동안 완료하는 데 30분이 걸리는 작업이 수행됩니다. 방대한 양의 수신 데이터로 인해 워크로드는 정기적으로 상당한 대기 시간에 직면합니다. 성능을 최적화하기 위해 솔루션 설계자는 확장 가능한 서버리스 시스템을 구축해야 합니다.

솔루션 아키텍트는 어떤 조치를 취해야 합니까? (2개를 선택하세요.)

A. Amazon Kinesis Data Firehose를 사용하여 데이터를 수집합니다.

B. AWS Step Functions와 함께 AWS Lambda를 사용하여 데이터를 처리합니다.

C. AWS DMS(데이터베이스 마이그레이션 서비스)를 사용하여 데이터를 수집합니다.

D. Auto Scaling 그룹의 Amazon EC2 인스턴스를 사용하여 데이터를 처리합니다.

E. AWS Fargate with Amazon Elastic Container Service(Amazon ECS)를 사용하여 데이터를 처리합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A, E

해설 : 

확장 가능한 서버리스 시스템으로 개발자가 서버를 관리할 필요 없이 애플리케이션을 빌드하고 실행할 수 있도록 하는 클라우드 네이티브 개발 모델입니다. 서버리스 모델에도 서버가 존재하긴 하지만, 애플리케이션 개발에서와 달리 추상화(온디맨드/오토스케일링)
2개의 수집기(A, C)와 3개의 처리기(B, D, E)가 있습니다.

A 정답 -> Amazon Kinesis Data Firehose는 스트리밍 데이터를 안정적으로 캡처하고 전환하여 데이터 레이크, 데이터 스토어, 분석 서비스에 전달하는 추출, 전환, 적재(ETL) 서비스로 `거의 실시간(near realtime)`이므로 적합

C 탈락 -> AWS DMS(데이터베이스 마이그레이션 서비스)는 데이터베이스 및 분석 워크로드를 AWS로 빠르고 안전하게 이동하여 가동 중단 시간 및 데이터 손실을 방지하는 데 도움이 되는 관리형 마이그레이션 및 복제 서비스로 복제만 하는 것이라서 부적합

B 탈락 -> AWS Step Functions는 개발자가 AWS 서비스를 사용하여 분산 애플리케이션을 구축하고, 프로세스를 자동화하며, 마이크로서비스를 오케스트레이션하고, 데이터 및 기계 학습(ML) 파이프라인을 생성할 수 있도록 지원하는 시각적 워크플로 서비스.
람다는 최대 15분 동안 실행될 수 있고, 작업이 30분이기 때문에 람다는 쓸 수 없음.
https://aws.amazon.com/lambda/faqs/#:~:text=AWS%20Lambda%20functions%20can%20be,1%20second%20and%2015%20minutes.

D 탈락 -> 작동하지만 서버리스가 아님.

E 정답 -> AWS Fargate는 컨테이너에 적합한 서버리스 컴퓨팅으로 서버를 관리하지 않고도 애플리케이션 구축에 초점을 맞출 수 있도록 지원하는 종량제 서버리스 컴퓨팅 엔진임.
Amazon ECS/EKS와 호환.
https://aws.amazon.com/fargate/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc&fargate-blogs.sort-by=item.additionalFields.createdDate&fargate-blogs=derd=dateTime

</div>
</details>

<hr/>

## Prob. 28

Amazon Elastic Block Store(Amazon EBS) 볼륨은 미디어 조직에서 비디오 자료를 저장하는 데 사용합니다. 특정 비디오 파일이 인기를 얻었고 현재 전 세계에서 많은 사람들이 이 파일을 보고 있습니다. 결과적으로 비용이 증가했습니다.

사용자 접근성을 위태롭게 하지 않으면서 비용을 절감할 수 있는 단계는 무엇입니까?

A. EBS 볼륨을 프로비저닝된 IOPS(PIOPS)로 변경합니다.

B. 비디오를 Amazon S3 버킷에 저장하고 Amazon CloudFront 배포를 생성합니다.

C. 비디오를 여러 개의 작은 세그먼트로 분할하여 사용자가 요청된 비디오 세그먼트로만 라우트되도록 합니다.

D. 각 영역에서 Amazon S3 버킷을 지우고(Clear) 비디오를 업로드하여 사용자가 가장 가까운 S3 버킷으로 라우팅되도록 합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

접근성은 전 세계이며 비용을 절감하는 문제 요점.

A 탈락 -> 입출력 처리가 빨라져서 비용이 올라갈 것임.

B 정답 -> S3에 비디오를 저장하고 배포를 위해 Cloudfront를 사용.

C 탈락 -> 전보다 추가된 과정이 생겨서 적합하지 않은 것 같음.

D 탈락 -> B와 같은 효과를 기대하지만 비용은 더 많이 들거 같음.

</div>
</details>

<hr/>

## Prob. 29 

Amazon S3 버킷은 이미지 호스팅 회사에서 객체를 저장하는 데 사용합니다. 회사는 S3 버킷에 포함된 항목이 의도하지 않게 공개되는 것을 방지하고자 합니다. AWS 계정의 모든 S3 항목은 전체적으로 비공개로 유지되어야 합니다.

어떤 솔루션이 이러한 기준을 충족할까요?

A. Amazon GuardDuty를 사용하여 S3 버킷 정책을 모니터링합니다. AWS Lambda 함수를 사용하여 개체를 공개하는 변경 사항에 업데이트를 적용하는 자동 업데이트 적용 작업 규칙을 생성합니다.

B. AWS Trusted Advisor를 사용하여 공개적으로 액세스할 수 있는 S3 버킷을 찾습니다. 변경 사항이 감지되면 Trusted Advisor에서 이메일 알림을 구성합니다. 공개 액세스를 허용하는 경우 S3 버킷 정책을 수동으로 변경합니다.

C. AWS Resource Access Manager를 사용하여 공개적으로 액세스할 수 있는 S3 버킷을 찾습니다. 변경 사항이 감지되면 Amazon Simple Notification Service(Amazon SNS)를 사용하여 AWS Lambda 기능을 호출합니다. 변경 사항을 프로그래밍 방식으로 교정하는 람다 함수를 배포합니다.

D. 계정 수준에서 S3 공용 액세스 차단 기능을 사용합니다. AWS 조직을 사용하여 IAM 사용자가 설정을 변경할 수 없도록 하는 SCP(서비스 제어 정책)를 만듭니다. SCP를 계정에 적용합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

AWS 계정의 모든 S3 항목이 비공개로 유지 문제 요점.

A 탈락 -> Amazon GuardDuty는 AWS 계정 및 워크로드에서 악의적 활동을 모니터링하고 상세한 보안 결과를 제공하여 가시성 및 해결을 촉진하는 위협 탐지 서비스.
모니터링하여 람다함수로 문제에 대해 자동 작업 규칙을 해도 이미 일어난 일을 대응하는 것이라 부적합.

B 탈락 -> AWS Trusted Advisor는 AWS 모범 사례를 따르는 데 도움이 되는 권장 사항을 제공하고 검사를 사용하여 계정을 평가하는 서비스.
공개적으로 액세스할 S3를 찾는 것부터해서 평가해주는 서비스라서 부적합.

C 탈락 -> AWS Resource Access Manager는 지원되는 리소스 유형에 대해 AWS 계정 전체에서, 조직 또는 조직 단위(OU) 내에서 IAM 역할 및 사용자와 안전하게 리소스를 공유하는 서비스.
위에 두 가지 사항과 같이 부적합.

D 정답 -> 항상 사전 예방적이어야 하며 솔루션에 사후 대응적이지 않아야 합니다. 따라서 D는 정보가 공개적으로 액세스될 가능성을 방지하기 위해 공개 액세스를 차단하며 IAM 사용자에 SCP를 적용하여 설정을 변경 못하게 막음.

</div>
</details>

<hr/>

## Prob. 30

회사 웹 사이트는 Amazon RDS MySQL 다중 AZ DB 인스턴스에 트랜잭션 데이터를 저장합니다. 다른 내부 시스템은 이 데이터베이스 인스턴스를 쿼리하여 일괄 처리를 위한 데이터를 가져옵니다. 내부 시스템이 RDS DB 인스턴스에서 데이터를 요청하면 RDS DB 인스턴스가 급격히 느려집니다. 이는 웹사이트의 읽기 및 쓰기 성능에 영향을 미치므로 사용자의 응답 시간이 느려집니다.

어떤 접근 방식이 웹사이트 성능을 향상시킬까요?

A. MySQL 데이터베이스 대신 RDS Postgre DB를 사용합니다.

B. Amazon ElastiCache를 사용하여 웹 사이트에 대한 쿼리 응답을 캐시합니다.

C. 현재 RDS MySQL Multi-AZ DB 인스턴스에 가용 영역을 추가합니다.

D. RDS DB 인스턴스에 Read Replica를 추가하고 읽기 복제본을 쿼리하도록 내부 시스템을 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

내부 시스템의 쿼리 성능 문제 요점.

Performance(성능) = Read Replicas
Disaster Recovery(재해 복구) = Multi-AZ

A 탈락 -> DB 엔진을 변경하는 것은 성능 향상에 도움이 되지 않아 부적합.
B 탈락 -> ElastiCache는 동일한 쿼리에서 데이터를 캐싱하는 데만 도움되 부적합.
C 탈락 -> Multi-AZ 데이터베이스가 2개의 AZ에 걸쳐 있고 고가용성이라 부적합.
D 정답 -> Read Replica는 읽기 쿼리를 처리할 영역을 만들기에 적합.

AWS Cloud > Region > VPC, 게이트웨이, ELB, 엔드포인트, 피어링, 커넥션 등 > AZ(Cluster) > 서브넷 > 디바이스

</div>
</details>

<hr/>

* Ref
  - [ExamTopics](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate-saa-c02/view/3)