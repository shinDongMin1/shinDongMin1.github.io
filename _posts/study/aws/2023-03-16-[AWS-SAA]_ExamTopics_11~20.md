---
layout: post
title: "[AWS-SAA] Examtopics 11~20"
subtitle: AWS
date: '2023-03-16 00:00:01 +0900'
category: study
tags: aws aws-saa
image:
  path: /assets/img/study_AWS/saa-co2_logo.png
---

SAA Examtopics 11~20번 문제를 풀어보자.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## Prob. 11

Amazon EC2 인스턴스에서 기업은 일시적인 트랜잭션 데이터를 생성하는 애플리케이션을 개발하고 있습니다. 
애플리케이션에는 조정 가능하고 일관된 IOPS를 제공할 수 있는 데이터 스토리지에 대한 액세스가 필요합니다.
솔루션 설계자는 어떤 권장 사항을 제시해야 합니까?

A. 처리량 최적화 HDD(st1) 루트 볼륨과 콜드 HDD(sc1) 데이터 볼륨을 사용하여 EC2 인스턴스를 프로비저닝합니다.

B. 루트 및 데이터 볼륨으로 사용할 처리량 최적화 HDD(st1) 볼륨을 사용하여 EC2 인스턴스를 프로비저닝합니다.

C. 범용 SSD(gp2) 루트 볼륨 및 프로비저닝된 IOPS SSD(io1) 데이터 볼륨을 사용하여 EC2 인스턴스를 프로비저닝합니다.

D. 범용 SSD(gp2) 루트 볼륨을 사용하여 EC2 인스턴스를 프로비저닝합니다. 데이터를 Amazon S3 버킷에 저장하도록 애플리케이션을 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

Amazon EBS(Elastic Block Store) 볼륨은 내구성이 뛰어난 블록 수준 스토리지 디바이스(인스턴스)이며 프로덕션 환경에서 실시간 구성 변경을 지원합니다. 
볼륨을 인스턴스에 연결한 후 물리적 볼륨을 사용하는 것으로 하드 디스크처럼 사용할 수 있습니다.
범용 SSD(gp2/gp3), 프로비저닝된 IOPS SSD(io1/io2), 처리량 최적화 HDD(st1) 볼륨 유형을 제공, 콜드 HDD (sc1) 및 마그네틱 (standard)는 성능 특성이 다릅니다. 
* 인스턴스 스토어 볼륨에서 제공하지 않는 이점을 제공
* EBS 볼륨을 생성하면 가용성 내에서 자동으로 복제
* EC2 인스턴스의 실행 수명과는 별개(DeleteOnTermination true/false)
* EBS 볼륨은 유연하고 유형, 동적으로 크기를 늘리고 프로비저닝된 IOPS 용량 및 라이브 프로덕션 볼륨의 볼륨 유형 변경 가능
* 자주 업데이트해야 하는 데이터의 기본 스토리지로 사용
  + 시스템 드라이브
  + 데이터베이스 응용 프로그램
  + 지속적인 디스크 검사를 수행하는 처리량 집약적인 응용 프로그램
* 동일한 가용 영역, 볼륨에 따라 인스턴스 유형, 다중 연결을 사용하여 탑재
* 스냅샷(증분식), 데이터 암호화, 모니터링

사용자는 Amazon EC2 인스턴스 스토어(Amazon S3에 저장된 템플릿으로부터 생성된)가 지원하는 AMI와 Amazon EBS에서 지원하는 AMI 중에서 선택할 수 있습니다. 시작 속도가 더 빠르고 영구 스토리지를 사용하는 Amazon EBS 지원 AMI를 사용하는 것이 좋음
루트 볼륨 - 인스턴스 부팅에 사용된 이미지를 저장
데이터 볼륨 - 데이터를 저장

C -> 오직 gp3, io1, or io2 볼륨만 configurable IOPS가 있음 <br>
[링크](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes.html)

</div>
</details>

<hr/>

## Prob. 12

새로운 워크로드를 구현하기 전에 솔루션 설계자는 회사의 현재 IAM 규칙을 검토하고 업데이트해야 합니다. 솔루션 설계자가 작성한 정책은 다음과 같습니다:

![prob_12](/assets/img/study_AWS/[SAA]_ExamTopics_11~20/prob_12.png)

그 정책의 순효과는 무엇입니까?

A. 사용자는 s3을 제외한 모든 작업을 수행할 수 있습니다.MFA(Multi-factor Authentication)가 활성화된 경우 PutObject를 입력합니다.

B. 사용자는 s3을 제외한 모든 작업이 허용됩니다.MFA(Multi-factor Authentication)가 활성화되지 않은 경우 PutObject를 입력합니다.

C. 사용자는 s3을 제외한 모든 작업이 거부됩니다.MFA(Multi-factor Authentication)가 활성화된 경우 PutObject를 입력합니다.

D. 사용자는 s3을 제외한 모든 작업이 거부됩니다.MFA(Multi-factor Authentication)가 활성화되지 않은 경우 PutObject를 입력합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

워크로드 고객 대면 애플리케이션이나 백엔드 프로세스 같이 비즈니스 가치를 창출하는 리소스 및 코드 모음을 말합니다. 워크로드는 단일 리소스의 하위 집합으로 구성되거나 여러 리소스에 걸친 여러 리소스의 모음일 수 있습니다.

사용자는 s3을 제외한 모든 작업이 거부됩니다.<br>
MFA(Multi-factor Authentication)가 활성화되지 않은 경우 PutObject를 입력합니다.<br>

사용자는 모든 리소스에 대한 S3의 PutObject의 작업을 제외하고 거부. 만약 MFA가 false면

"Effect": "Deny"<br>
\* = All resources<br>
"NotAction": "S3:PutObject" = S3:PutObject 제외하고<br>
"Condition": "aws:MultiFactorAuthPresent": "false" = If MFA is not enabled

</div>
</details>

<hr/>

## Prob. 13 

실시간 처리를 허용하려면 웹 애플리케이션이 Amazon S3에 주문 데이터를 유지해야 합니다.
솔루션 설계자는 확장 가능하고 내결함성이 있는 아키텍처를 설계해야 합니다.

어떤 솔루션이 이러한 기준을 충족합니까? (2개를 선택하세요.)

A. 주문 이벤트를 Amazon DynamoDB 테이블에 기록합니다. DynamoDB Streams를 사용하여 페이로드를 구문 분석하고 Amazon S3에 데이터를 쓰는 AWS Lambda 함수를 트리거합니다.

B. 주문 이벤트를 Amazon Simple Queue Service(Amazon SQS) 대기열에 기록합니다. 대기열을 사용하여 페이로드를 파싱하고 Amazon S3에 데이터를 쓰는 AWS Lambda 함수를 트리거합니다.

C. 아마존 심플 알림 서비스(Amazon SNS) 항목에 주문 이벤트를 작성합니다. SNS 항목을 사용하여 페이로드를 구문 분석하고 데이터를 Amazon S3에 쓰는 AWS Lambda 함수를 트리거합니다.

D. 주문 이벤트를 Amazon Simple Queue Service(Amazon SQS) 대기열에 기록합니다. Amazon EventBridge(Amazon CloudWatch Events) 규칙을 사용하여 페이로드를 구문 분석하고 데이터를 Amazon S3에 쓰는 AWS Lambda 함수를 트리거합니다.

E. 아마존 심플 알림 서비스(Amazon SNS) 항목에 주문 이벤트를 작성합니다. Amazon EventBridge(Amazon CloudWatch Events) 규칙을 사용하여 페이로드를 구문 분석하고 데이터를 Amazon S3에 쓰는 AWS Lambda 함수를 트리거합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A, B

해설 : 

내결함성이란 시스템의 일부 구성 요소가 작동하지 않더라도 계속 작동할 수 있는 기능이고 확장 가능이란 말그대로 입니다.
페이로드(payload)는 사용에 있어서 전송되는 데이터로 함께 전송되는 헤더와 메타데이터와 같은 데이터는 제외한다. 컴퓨터 보안에서 페이로드는 멀웨어의 일부를 뜻함
파싱(parsing)은 구문 분석을 뜻함

DynamoDB Streams에 대한 변경된 데이터 캡처(Change data capture for DynamoDB Streams)는 NoSQL DB로 테이블에서 시간 순서에 따라 항목 수준 수정을 캡처하고 이 정보를 최대 24시간 동안 로그에 저장합니다. 로그와 데이터 항목은 변경 전후 거의 실시간으로 나타나므로 애플리케이션에서 이러한 로그와 데이터에 액세스 가능, 암호화는 실시간이란 요소에 적합
SQS는 서로 다른 서비스간에 연결이 끊겨서 장애 발생하더라도 작동 가능하게 하는 내결합성이란 요소에 적합
SNS는 Amazon EventBridge(Amazon CloudWatch Events)와 같은 역할로 알림에 대한 요소로 적합하지 않는 것 같습니다.

</div>
</details>

<hr/>

## Prob. 14 

us-east-1 지역의 비즈니스에서 사진 호스팅 서비스를 제공합니다. 많은 국가의 사용자가 프로그램을 사용하여 이미지를 업로드하고 탐색할 수 있습니다. 일부 사진은 몇 달 동안 조회수가 높은 반면 다른 사진은 일주일 미만 동안 조회수가 적습니다. 이 프로그램은 최대 20MB 크기의 사진 업로드를 지원합니다. 서비스는 사진 정보를 기반으로 각 사용자에게 어떤 사진을 보여줄지 결정합니다.

적합한 사용자에게 가장 비용 효율적인 액세스를 제공하는 옵션은 무엇입니까?

A. 사진을 Amazon DynamoDB에 저장합니다. 자주 보는 항목을 캐시하려면 DAX(DynamoDB Accelerator)를 켜십시오.

B. 사진을 Amazon S3 Intelligent-Tiering 스토리지 클래스에 저장합니다. 사진 메타데이터와 S3 위치를 DynamoDB에 저장합니다.

C. 사진을 Amazon S3 Standard 스토리지 클래스에 저장합니다. 30일 이상 지난 사진을 S3 Standard-Infrequent Access(S3 Standard-IA) 스토리지 클래스로 이동하기 위해 S3 라이프사이클 정책을 설정합니다. 메타데이터를 추적하려면 개체 태그를 사용하십시오.

D. 사진을 Amazon S3 Glacier 스토리지 클래스에 저장합니다. 30일이 지난 사진을 S3 Glacier Deep Archive 스토리지 클래스로 이동하기 위한 S3 Lifecycle 정책을 설정합니다. 사진 메타데이터와 해당 S3 위치를 Amazon Elastic Search Service(Amazon ES)에 저장합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

A -> NoSQL DB로 비정형 데이터에 적합
DAX는 Amazon DynamoDB를 위한 가용성이 뛰어난 완전관리형 인-메모리 Cache로서 최대 10배의 성능을 제공합니다. 개발자가 캐시 무효화, 클러스터 관리 또는 데이터 집단을 관리할 필요 없이 DAX가 DynamoDB 테이블에 인-메모리 가속화를 추가하는 데 필요한 모든 작업을 수행(프로비저닝한 용량에 대해서만 비용을 지불)

B -> 지능형 계층화 S3로 데이터를 `가장 비용 효율적인 계층`으로 자동 이동하여 스토리지 비용을 최적화 하도록 설계됨

C -> 자주 액세스하는 데이터에 적합(비싼 스토리지 요금/저렴한 트래픽 요금)하고 30일 이후에는 사용 빈도가 다소 낮은 데이터에 적합(스토리지 요금은 저렴/트래픽 요금은 비싸짐)
객체 태그 지정을 이용하여 스토리지를 분류합니다. 각 태그는 키-값 페어입니다.

D -> 사용 빈도가 극히 낮은 데이터에 적합(스토리지는 많이 저렴/트래픽은 많이 비싸짐) 30일이 이후에는 일년에 한두 번 액세스(복원할 수 있는 장기 데이터 아카이브용)
Elastic Search는 Apache Lucene에 구축되어 배포된 검색 및 분석 엔진으로 로그 분석, 전체 텍스트 검색, 보안 인텔리전스, 비즈니스 분석 및 운영 인텔리전스 사용 사례에 일반적으로 사용
(신속한 가치 실현-스키마 없는 JSON 문서/고성능-데이터를 병렬로 처리/무료 도구 및 플러그인-유명 시각화 및 보고서 도구/실시간에 가까운 운영/쉬운 애플리케이션 개발)

</div>
</details>

<hr/>

## Prob. 15

한 비즈니스에서 Amazon S3 버킷에 정적 사진을 저장할 웹 사이트를 만들고 있습니다. 회사의 목표는 모든 향후 요청에 대한 대기 시간과 비용을 줄이는 것입니다.

솔루션 설계자는 서비스 구성을 어떻게 제안해야 합니까?

A. Amazon S3 앞에 NAT 서버를 구축합니다.

B. Amazon S3 앞에 Amazon CloudFront를 배포합니다.

C. Amazon S3 앞에 네트워크 로드 밸런서를 배포합니다.

D. 웹 사이트의 용량을 자동으로 조정하도록 자동 배율을 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

A -> NAT는 네트워크 주소 변환으로 IP패킷에 있는 출발지 및 목적지의 IP주소와 TCP/UDP포트 숫자 등을 바꿔 재기록하면서 네트워크 트래픽 기술임.
IP주소 절약 - 하나의 공인IP로 여러대의 호스트가 인터넷 접속(공유기에 NAT기능이 있음)
보안 - 라우터(또는 공유기) 외부로 트래픽이 나갈때 사설에서 공인IP주소로 바뀌어 최종 목적지로의 사설IP를 몰라서 내부 네트워크 및 호스트들을 보호 가능(특성상 IP를 숨김)

B -> CloudFront는 짧은 지연 시간과 빠른 전송 속도로 전 세계 고객에게 안전하게 전송하는 고속 콘텐츠 전송 네트워크(CDN) 서비스임.
정적/동적 컨텐츠 모두 최적화 Cloudfront + S3 = Static Website

C -> Elastic Load Balancing은 둘 이상의 가용 영역에서 EC2 인스턴스, 컨테이너, IP 주소 등 여러 대상에 걸쳐 수신되는 트래픽을 자동으로 분산합니다. 등록된 대상의 상태를 모니터링하면서 상태가 양호한 대상으로만 트래픽을 라우팅함
(애플리케이션/네트워크/게이트웨이/클래식이 있음)

D -> 용량을 자동 배율을 구성해서 트래픽에 대한 요구 불만족

</div>
</details>

<hr/>

## Prob. 16

전자 상거래 웹 사이트의 데이터베이스 계층의 경우 회사는 처리량이 제공되는 Amazon DynamoDB를 사용합니다. 플래시 판매 기간 동안 데이터베이스가 트랜잭션 볼륨을 관리할 수 없을 때 클라이언트는 지연 기간에 직면할 수 있습니다. 결과적으로 비즈니스는 거래를 잃게 됩니다. 데이터베이스는 정규 시간 동안 정상적으로 작동합니다.

어떤 접근 방식이 회사의 성과 문제를 해결합니까?

A. 플래시 영업 중에 DynamoDB를 온디맨드 모드로 전환합니다.

B. 빠른 메모리 성능을 위해 DynamoDB Accelerator를 구현합니다.

C. Amazon Kinesis를 사용하여 트랜잭션을 DynamoDB로 대기열에 넣습니다.

D. 트랜잭션을 DynamoDB로 대기열에 넣으려면 Amazon SQS(Amazon Simple Queue Service)를 사용하십시오.


<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

Discussion에서의 한 유저는 B. DAX의 경우 Read에만 영향을 주며, 트랜잭션 볼륨을 관리할 수 없는 이유로 용량(capacity)를 꼽았다. 그렇기 때문에 답이 A라고 주장

하지만 다른 유저는 DAX는 Read 뿐만 아니라 Write(Put)에도 영향을 주며, DynamoDB는 용량(capacity)가 부족할 경우 자동으로 확장할 수 있기 때문에 답이 B라고 주장

A -> 플래시 영업은 경영 제한된 시간 동안 한정된 수량을 선착순으로 할인 판매 하고 품절되면 자동으로 종료되는 판매 형태로 온디맨드 모드 전환하여 트랜잭션당 요금이 아닌 사용된 초로 계산하는 것이 적합하다고 생각

B -> DAX는 Read/Write 활동이 모두 캐시에 반영되지만 쓰기에서 더 효과적으로 설명되어 있음 그리고 DynamoDB(NoSQL) 프로비저닝 IOPS/Auto Scaling/백업이 적용되어 있지만 문제에서 플래시 판매 기간 동안이라고 하여 부적합하다고 생각

C -> Amazon Kinesis는 실시간 스트리밍 데이터를 손쉽게 수집, 처리 및 분석할 수 있으므로 적시에 통찰력을 확보하고 새로운 정보에 신속하게 대응(실시간/완전관리형/확장성)

D -> Amazon SQS는 서로 다른 서비스간에 장애를 해결하기 위한 대기열

</div>
</details>

<hr/>

## Prob. 17

중요한 미디어 회사는 AWS를 사용하여 웹 애플리케이션을 호스팅합니다. 회사는 전 세계 소비자에게 신뢰할 수 있는 액세스를 제공하기 위해 비밀 미디어 파일 캐싱을 시작할 계획입니다. Amazon S3 버킷은 자료를 저장하는 데 사용됩니다. 조직은 요청의 출처에 관계없이 신속하게 자재를 공급해야 합니다.
어떤 솔루션이 이러한 기준을 충족할까요?

A. AWS DataSync를 사용하여 S3 버킷을 웹 응용 프로그램에 연결합니다.

B. AWS Global Accelerator를 배포하여 S3 버킷을 웹 응용 프로그램에 연결합니다.

C. Amazon CloudFront를 배포하여 S3 버킷을 CloudFront 엣지 서버에 연결합니다.

D. S3 버킷을 웹 응용 프로그램에 연결하려면 Amazon Simple Queue Service(Amazon SQS)를 사용하십시오.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

A -> Data Sync는 온-프레미스에서 AWS로 데이터를 옮길 때 사용

B -> Global Accelerator는 캐싱이 아닌 network latency를 낮추는데 사용

C -> CloudFront는 짧은 지연 시간과 빠른 전송 속도로 전 세계 고객에게 안전하게 전송하는 고속 콘텐츠 전송 네트워크(CDN) 서비스임. (엣지 로케이션/캐시/CDN/보안)
정적/동적 컨텐츠 모두 최적화(S3/EC2)

CloudFront OAI(Origin Access Identity)로 CloudFront가 S3에 저장된 Private 객체에 액세스(`비밀 캐싱`에 도움) 할 수 있도록 하는 특별한 식별자임.
외부 사용자가 S3 Endpoint를 통한 직접적인 요청이 아닌 CF의 배포를 통해 접근하도록 구성하고 싶다면 OAI를 고려

OAI는 IAM과 성격이 비슷해 보이지만 다름. IAM 사용자를 생성하지도 않을뿐더러, 정책을 직접 연결할 수 없다는 점에서 조금 다르며 반대로 IAM도 CloudFront Distribution에 할당될 수 없음. OAI는 S3 정책안에 'Principal'를 통해 참조되어 사용되며, 단순히 S3 Origin 보안 강화를 위해 요청을 식별하는 데 사용되는 S3만을 위한 CloudFront 서비스

D -> Amazon SQS는 서로 다른 서비스간에 장애를 해결하기 위한 대기열으로 문제와 상관이 없는 솔루션

</div>
</details>

<hr/>

## Prob. 18

AWS 클라우드에는 웹 애플리케이션이 배포됩니다. 웹 및 데이터베이스 계층으로 구성된 2계층 설계입니다. 웹 서버에서 XSS(교차 사이트 스크립팅) 공격이 가능합니다.

솔루션 설계자가 취약점을 해결하기 위해 취해야 하는 최선의 조치는 무엇입니까?

A. 클래식 로드 밸런서를 생성합니다. 로드 밸런서 뒤에 웹 계층을 배치하고 AWS WAF를 활성화합니다.

B. 네트워크 로드 밸런서를 생성합니다. 로드 밸런서 뒤에 웹 계층을 배치하고 AWS WAF를 활성화합니다.

C. 애플리케이션 로드 밸런서를 생성합니다. 로드 밸런서 뒤에 웹 계층을 배치하고 AWS WAF를 활성화합니다.

D. 애플리케이션 로드 밸런서를 생성합니다. 로드 밸런서 뒤에 웹 계층을 놓고 AWS Shield Standard를 사용합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

Elastic Load Balancing(ELB)은 하나 이상의 가용 영역(AZ)에 있는 여러 대상 및 가상 어플라이언스에서 들어오는 애플리케이션 트래픽을 자동으로 분산합니다.
AWS WAF(Web Application Firewall)는 CLB가 아닌 ALB(애플리케이션 로드 밸런서)와 통합되어 사용

A -> CLB는 AWS WAF를 사용 불가
B -> NLB는 AWS WAF를 사용 불가
C -> ALB + WAF = Protection from XSS
D -> AWS Shield는 애플리케이션을 보호하는 관리형 분산 서비스 거부(DDoS) 보호 서비스로 Standard와 Advanced가 있으며 추가 비용 없이 모든 인프라(계층 3 및 4) 공격에 대해 포괄적인 가용성 보호/추가 보호 및 완화, 실시간에 가까운 공격에 대한 가시성, 웹 애플리케이션 방화벽 AWS WAF와의 통합을 제공

</div>
</details>

<hr/>

## Prob. 19

웹사이트에서 기업은 검색 가능한 물건을 보관합니다. 데이터는 Amazon RDS for MySQL 데이터베이스의 천만 개 이상의 행이 있는 테이블에 저장됩니다. 데이터베이스는 2TB 범용 SSD(gp2) 어레이에 저장됩니다. 매일 회사 웹 사이트는 이 데이터에 대한 수백만 건의 변경 사항을 수신합니다. 조직은 특정 작업에 10초 이상이 소요된다는 사실을 발견하고 병목 현상이 데이터베이스 스토리지 성능이라는 결론을 내렸습니다.

성능 요구 사항을 충족하는 옵션은 무엇입니까?

A. 스토리지 유형을 Provisioned IOPS SSD(io1)로 변경합니다.

B. 인스턴스를 메모리에 최적화된 인스턴스 클래스로 변경합니다.

C. 인스턴스를 버스터블 성능 DB 인스턴스 클래스로 변경합니다.

D. MySQL 기본 비동기 복제로 Multi-AZ RDS 읽기 복제본을 사용합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

병목 현상은 데이터 I/O에 따른 스토리지 성능 개선이 필요함

A -> Provisioned IOPS SSD 솔루션의 이상적인 상황

B -> 높은 처리 성능이 요구되는 데이터베이스용이며, 더 많은 데이터를 저장할 수 있어 쿼리 시간이 빨라짐

C -> 순간 확장 가능한 인스턴스로 개발, 테스트, 다른 비프로덕션 데이터베이스를 위한 인스턴스

D -> 복제로 Multi-AZ을 사용하면 장애시 가용성이 좋아지고 읽기 트래픽도 처리

</div>
</details>

<hr/>

## Prob. 20

기업은 Amazon S3를 사용하여 민감한 데이터를 저장할 준비가 되어 있습니다. 규정 준수를 위해 데이터를 암호화해야 합니다. 암호화 키 사용에 대한 감사가 필요합니다. 매년 키를 교체해야 합니다.

어떤 솔루션이 이러한 매개변수를 충족하며 운영 효율성 측면에서 가장 최적입니까?

A. 고객이 제공한 키를 사용한 서버 측 암호화(SSE-C)

B. Amazon S3 관리 키를 사용한 서버 측 암호화(SSE-S3)

C. 수동 회전을 통한 AWS KMS(SSE-KMS) 고객 마스터 키(CMK)를 통한 서버 측 암호화

D. 자동 회전을 통한 AWS KMS(SSE-KMS) 고객 마스터 키(CMK)를 통한 서버 측 암호화

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

고객이 관리하는 CMK에 대해 자동 키 순환을 활성화하면 AWS KMS는 CMK에 대한 새로운 암호화 자료를 매년 생성함 수동 키 순환을 활성화하면 지정해서 생성함

A -> 서버 측 암호화는 저장된 데이터를 보호하기 위한 것입니다. 서버 측 암호화는 객체 메타데이터가 아닌 객체 데이터만 암호화합니다. 고객 제공 암호화 키(SSE-C)로 서버 측 암호화를 사용하여 자체 암호화 키를 저장할 수 있습니다.

B -> Amazon S3는 각 객체를 고유한 키로 암호화합니다. 또한 추가 보안 조치로 주기적으로 바뀌는 키를 사용하여 키 자체를 암호화합니다.

C -> 암호화 키에 대한 감사와 키 순환 모두 AWS-KMS에서만 가능하며 수동은 지정하여 생성

D -> 암호화 키에 대한 감사와 키 순환 모두 AWS-KMS에서만 가능하며 자동은 매년 생성

</div>
</details>

<hr/>

* Ref
  - [ExamTopics](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate-saa-c02/view/2)