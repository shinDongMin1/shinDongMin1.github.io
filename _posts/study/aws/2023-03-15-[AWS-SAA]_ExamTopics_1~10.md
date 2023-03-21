---
layout: post
title: "[AWS-SAA] Examtopics 1~10"
subtitle: AWS
date: '2023-03-15 00:00:01 +0900'
category: study
tags: aws aws-saa
image:
  path: /assets/img/study_AWS/saa-co2_logo.png
---

SAA Examtopics 1~10번 문제를 풀어보자.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## Prob. 1 

한 회사가 새로운 serverless 워크로드를 배치하려고 합니다.
솔루션 아키텍트는 AWS Lambda 함수를 호출하기 위한 권한을 구성해야 합니다.
함수는 Amazon EventBridge (Amazon CloudWatch Events) 규칙에 따라 트리거 될 것입니다.
권한은 최소 권한 원칙을 사용하여 구생되어야 합니다.

어떤 솔루션이 요구사항을 충족합니까?

A. 람다를 사용하여 함수에 실행 역할을 추가합니다:작업으로 함수를 호출하고 주체로 *를 호출합니다.

B. 람다를 사용하여 함수에 실행 역할을 추가합니다:작업으로 Function을 호출하고 주체로 Service:amazonaws.com 을 호출합니다.

C. 람다:'*를 액션으로, Service:events.amazonaws.com 을 주체로 하여 리소스 기반 정책을 함수에 추가합니다.

D. 람다를 사용하여 리소스 기반 정책을 함수에 추가합니다:작업으로 Function을 호출하고 주체로 Service:events.amazonaws.com 을 호출합니다.

<br>
<hr/>
<br>

<details>
<summary>영문 보기</summary>
<div markdown="1">
<br>

A. Add an execution role to the function with lambda:InvokeFunction as the action and * as the principal.

B. Add an execution role to the function with lambda:InvokeFunction as the action and Service:amazonaws.com as the principal.

C. Add a resource-based policy to the function with lambda:'* as the action and Service:events.amazonaws.com as the principal.

D. Add a resource-based policy to the function with lambda:InvokeFunction as the action and Service:events.amazonaws.com as the principal.

</div>
</details>

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

Add a resource-based policy to the function with lambda:InvokeFunction as the action and Service:events.amazonaws.com as the principal.

Amazon EventBridge로 Lambda함수를 호출하려면 아래와 같은 문구가 필요하다.

    "Action": "lambda:InvokeFunction" 
    "Principal": {
      "Service": "events.amazonaws.com"
    }

</div>
</details>

<hr/>

## Prob. 2-1 

한 회사는 Amazon EBS(Amazon Elastic Block Store)가 지원하는 Amazon EC2 인스턴스에서 애플리케이션을 실행합니다.
인스턴스는 매일 12시간 사용 가능해야합니다.
이 회사는 애플리케이션에 필요한 창 밖으로 인스턴스를 만들어 비용을 절감하고자 합니다. 
그러나 인스턴스를 사용할 수 없을 때마다 메모리의 내용을 보존해야 합니다.

솔루션 아키텍트는 해당 요구사항을 충족시키기 위해서 무엇을 해야합니까?

A. 응용 프로그램의 가용성 창 밖에서 인스턴스를 중지합니다. 필요한 경우 인스턴스를 다시 시작합니다.

B. 응용 프로그램의 가용성 창 밖에서 인스턴스를 최대 절전 모드로 전환합니다. 필요한 경우 인스턴스를 다시 시작합니다.

C. 자동 스케일링을 사용하여 응용 프로그램의 가용성 창 밖에서 인스턴스를 축소합니다. 필요한 경우 인스턴스를 확장합니다.

D. 응용 프로그램의 가용성 창 밖에서 인스턴스를 종료합니다. 필요한 경우 미리 구성된 AMI(Amazon 시스템 이미지)를 사용하여 인스턴스를 시작합니다.

<br>
<hr/>
<br>

<details>
<summary>영문 보기</summary>
<div markdown="1">
<br>

A. Stop the instance outside the application's availability window. Start up the instance again when required.

B. Hibernate the instance outside the application's availability window. Start up the instance again when required.

C. Use Auto Scaling to scale down the instance outside the application's availability window. Scale up the instance when required.

D. Terminate the instance outside the application's availability window. Launch the instance by using a preconfigured Amazon Machine Image (AMI) when required.

</div>
</details>

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

최대 절전 모드(Hiberate)를 사용하면 인스턴스의 메모리를 보존한 채로 인스턴스를 중지시킬 수 있다.

또한 인스턴스가 최대 절전 모드일 때는 EBS 볼륨과 Elastic IP 주소에 대한 요금만 지불한다.

</div>
</details>

<hr/>

## Prob. 2-2

한 온라인 사진 공유 회사가 us-west-1 Region에 있는 Amazon S3 버킷에 사진을 저장합니다. 
회사는 기존의 모든 사진과 새로운 사진의 복사본을 다른 지리적 위치에 저장해야 합니다.
운영 노력을 최소화하면서 이 요구 사항을 충족할 수 있는 솔루션은 무엇입니까?

A. us-east-1에 두 번째 S3 버킷을 만듭니다. 기존 S3 버킷에서 두 번째 S3 버킷으로 S3 지역 간 복제를 사용하도록 설정합니다.

B. 기존 S3 버킷의 CORS(크로스 오리진 리소스 공유) 구성을 생성합니다. CORS 규칙의 허용된 오리진 요소에서 us-east-1을 지정합니다.

C. 여러 가용성 영역에 걸쳐 us-east-1에 두 번째 S3 버킷을 생성합니다. S3 라이프사이클 관리 규칙을 만들어 두 번째 S3 버킷에 사진을 저장합니다.

D. us-east-1에 복제된 사진을 저장할 두 번째 S3 버킷을 만듭니다. AWS Lambda 함수를 호출하여 기존 S3 버킷에서 두 번째 S3 버킷으로 사진을 복사하는 개체 생성 및 업데이트 이벤트에 대한 S3 이벤트 알림을 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>영문 보기</summary>
<div markdown="1">
<br>

A. Create a second S3 bucket in us-east-1. Enable S3 Cross-Region Replication from the existing S3 bucket to the second S3 bucket.

B. Create a cross-origin resource sharing (CORS) configuration of the existing S3 bucket. Specify us-east-1 in the CORS rule's AllowedOrigin element.

C. Create a second S3 bucket in us-east-1 across multiple Availability Zones. Create an S3 Lifecycle management rule to save photos into the second S3 bucket.

D. Create a second S3 bucket in us-east-1 to store the replicated photos. Configure S3 event notifications on object creation and update events that invoke an AWS Lambda function to copy photos from the existing S3 bucket to the second S3 bucket.

</div>
</details>

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

엑셀 상에서의 답은 A이지만 이유를 모르겠다.
추후 검토 예정

</div>
</details>

<hr/>

## Prob. 3

회사는 회계 시스템을 온프레미스 데이터 센터에서 Amazon Web Services(AWS) 리전으로 마이그레이션하려고 합니다. 
데이터 보안과 변경 불가능한 감사 로그가 우선되어야 합니다. 
모든 AWS 활동은 규정 준수 감사를 받아야 합니다. 
비즈니스에서 AWS CloudTrail을 활성화했음에도 불구하고 이러한 요구 사항을 충족하는지 확인하려고 합니다.

CloudTrail을 보호하고 보호하기 위해 솔루션 설계자가 포함해야 하는 예방 조치 및 보안 절차는 무엇입니까? (2개 선택)

A. CloudTrail 로그 파일 유효성 검사를 사용합니다.

B. Cloud Trail Processing Library를 설치합니다.

C. CloudTrail에서 Insight 이벤트를 로깅할 수 있습니다.

D. 사내 리소스에서 사용자 지정 로깅을 사용합니다.

E. CloudTrail이 AWS KMS와 함께 서버 측 암호화를 사용하도록 구성되었는지 여부를 모니터링하는 AWS Config 규칙을 만듭니다

<br>
<hr/>
<br>

<details>
<summary>영문 보기</summary>
<div markdown="1">
<br>

A. Enable CloudTrail log file validation.

B. Install the CloudTrail Processing Library.

C. Enable logging of Insights events in CloudTrail.

D. Enable custom logging from the on-premises resources.

E. Create an AWS Config rule to monitor whether CloudTrail is configured to use server-side encryption with AWS KMS 

</div>
</details>

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A, E

해설 : 

A<br>
CloudTrail 로그 파일 유효성 검사를 실행한다.

E<br>
다음 보안 모범 사례에서는 CloudTrail의 데이터 보호도 해결한다 :<br>
AWS KMS 관리 키(SSE-KMS)로 CloudTrail 로그 파일 암호화<br>
CloudTrail에 대한 Amazon S3 버킷 정책<br>
CloudTrail 로그 파일 무결성에 대한 유효성 검토<br>
AWS 계정 간에 CloudTrail 로그 파일 공유

</div>
</details>

<hr/>

## Prob. 4-1

 한 회사가 최근 의료 영상과 관련된 새로운 서비스를 출시했습니다. 
 회사는 이미지를 스캔하고 Amazon EC2 인스턴스에 대한 AWS Direct Connect 연결을 통해 온프레미스 데이터 센터에서 이미지를 보냅니다. 
 처리가 완료되면 이미지가 Amazon S3 버킷에 저장됩니다. 
 회사 요구 사항에 따르면 EC2 인스턴스는 인터넷을 통해 액세스할 수 없습니다. 
 EC2 인스턴스는 아웃바운드 인터넷 액세스를 위해 온프레미스 데이터 센터로 돌아가는 기본 경로가 있는 프라이빗 서브넷에서 실행됩니다. 
 새로운 서비스의 활용도가 급격히 증가하고 있습니다. 
 솔루션 설계자는 회사의 요구 사항을 충족하고 Direct Connect 요금을 줄이는 솔루션을 추천해야 합니다. 

 어떤 솔루션이 이러한 목표를 가장 비용 효율적으로 달성합니까?

A. Amazon S3에 대한 VPC 끝점을 구성합니다. S3 끝점에 대한 개인 서브넷의 경로 테이블에 항목을 추가합니다.

B. 공용 서브넷에서 NAT 게이트웨이를 구성합니다. NAT 게이트웨이를 사용하도록 개인 서브넷의 경로 테이블을 구성합니다.

C. Amazon S3를 EC2 인스턴스에 파일 시스템 마운트 지점으로 구성합니다. 마운트를 통해 Amazon S3에 액세스합니다.

D. EC2 인스턴스를 공용 서브넷으로 이동합니다. 인터넷 게이트웨이를 가리키도록 공용 서브넷 경로 테이블을 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>영문 보기</summary>
<div markdown="1">
<br>

A. Configure a VPC endpoint for Amazon S3. Add an entry to the private subnet's route table for the S3 endpoint.

B. Configure a NAT gateway in a public subnet. Configure the private subnet's route table to use the NAT gateway.

C. Configure Amazon S3 as a file system mount point on the EC2 instances. Access Amazon S3 through the mount.

D. Move the EC2 instances into a public subnet. Configure the public subnet route table to point to an internet gateway.

</div>
</details>

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : Discussion에서 A와 B를 두고 대치. 답 A가 맞는듯 

해설 : 

</div>
</details>

<hr/>

## Prob. 4-2

회사는 웹사이트에서 검색 가능한 항목 목록을 유지 관리합니다. 
데이터는 천만 개 이상의 항목이 있는 테이블의 MySQL용 Amazon RDS 데이터베이스에 저장됩니다. 
데이터베이스는 2TB 범용 SSD(gp2) 어레이에 보관됩니다. 
이 회사의 웹사이트는 매일 수백만 건의 데이터 업데이트를 받습니다. 
기업은 일부 작업이 10초 이상 소요된다는 사실을 발견하고 병목 현상이 데이터베이스 스토리지 성능이라고 판단했습니다.

다음 중 성능 요구 사항을 충족하는 옵션은 무엇입니까?

A. 스토리지 유형을 프로비저닝된 IOPS SSD(io1)로 변경합니다.

B. 인스턴스를 메모리에 최적화된 인스턴스 클래스로 변경합니다.

C. 인스턴스를 버스트 가능 성능 DB 인스턴스 클래스로 변경합니다.

D. MySQL 기본 비동기식으로 Multi-AZ RDS 읽기 복제본 사용 복제.

<br>
<hr/>
<br>

<details>
<summary>영문 보기</summary>
<div markdown="1">
<br>

A. Change the storage type to Provisioned IOPS SSD (io1).

B. Change the instance to a memory-optimized instance class.

C. Change the instance to a burstable performance DB instance class.

D. Enable Multi-AZ RDS read replicas with MySQL native asynchronous 
replication.

</div>
</details>

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

문제상 병목 현상이 발생하는 이유는 스토리지 성능이다.<br>
범용 SSD보다 더 성능이 좋은 프로비전된 IOPS SSD를 사용하면 병목 현상이 해결될 것이다.

</div>
</details>

<hr/>

## Prob. 5

재난 대응 팀이 드론을 사용하여 최근 폭풍 피해의 이미지를 수집하고 있습니다. 
대응팀의 노트북에는 이미지를 전송하고 데이터를 처리할 수 있는 스토리지 및 컴퓨팅 용량이 부족합니다. 
팀에는 처리용 Amazon EC2 인스턴스와 저장용 Amazon S3 버킷이 있지만 네트워크 연결이 간헐적이고 안정적이지 않습니다. 
이미지는 손상을 피할 수 있도록 처리되어야 합니다. 

솔루션 아키텍트는 무엇을 추천해야 합니까?

A. AWS Snowball Edge 장치를 사용하여 이미지를 처리하고 저장합니다.

B. EC2 인스턴스에 간헐적으로 연결하는 동안 Amazon SQS(Simple Queue Service)에 이미지를 업로드합니다.

C. 스토리지용 S3 버킷과 이미지 처리용 EC2 인스턴스를 별도로 대상으로 하는 여러 전송 스트림을 생성하도록 Amazon Kinesis Data Firehose를 구성합니다.

D. 하드웨어 장치에 미리 설치된 AWS Storage Gateway를 사용하여 연결이 사용 가능해지면 Amazon S3에서 이미지를 처리할 수 있도록 이미지를 로컬로 캐시합니다.

<br>
<hr/>
<br>

<details>
<summary>영문 보기</summary>
<div markdown="1">
<br>

A. Use AWS Snowball Edge devices to process and store the images.

B. Upload the images to Amazon Simple Queue Service (Amazon SQS) during intermittent connectivity to EC2 instances.

C. Configure Amazon Kinesis Data Firehose to create multiple delivery streams aimed separately at the S3 buckets for storage and the EC2 instances for processing the images.

D. Use AWS Storage Gateway pre-installed on a hardware appliance to cache the images locally for Amazon S3 to process the images when connectivity becomes available.

</div>
</details>

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

재해 상황이므로 데이터는 한 번 수집 후 말 것이기 때문에, Snowball Edge device면 충분하다.<br>
또한 Storage Gateway에는 compute가 없지만 Snowball에는 있다는 말이 있음.

</div>
</details>

<hr/>

## Prob. 6

회사에서 데이터 저장을 위해 Amazon DynamoDB 테이블을 사용할 계획입니다. 
회사는 비용 최적화에 대해 우려하고 있습니다. 
이 테이블은 대부분의 아침 저녁에 사용되지 않습니다. 
읽기 및 쓰기 트래픽은 종종 예측할 수 없습니다. 
트래픽 스파이크가 발생하면 매우 빠르게 발생합니다.

솔루션 아키텍트는 무엇을 추천해야 합니까?

A. 온디맨드 용량 모드에서 DynamoDB 테이블을 생성합니다.

B. 글로벌 보조 인덱스를 사용하여 DynamoDB 테이블을 만듭니다.

C. 프로비저닝된 용량과 자동 확장 기능을 갖춘 DynamoDB 테이블을 생성합니다.

D. 프로비저닝된 용량 모드에서 DynamoDB 테이블을 생성하고 글로벌 테이블로 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>영문 보기</summary>
<div markdown="1">
<br>

A. Create a DynamoDB table in on-demand capacity mode.

B. Create a DynamoDB table with a global secondary Index.

C. Create a DynamoDB table with provisioned capacity and auto scaling.

D. Create a DynamoDB table in provisioned capacity mode, and configure it as a global table.

</div>
</details>

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

상황이 온디맨드에 매우 적합한 상황이다.

</div>
</details>

<hr/>

## Prob. 7

기업은 AWS 애플리케이션을 사용하여 전 세계 구독자에게 콘텐츠를 제공합니다. 
수많은 Amazon EC2 인스턴스가 애플리케이션용 Application Load Balancer(ALB) 뒤의 프라이빗 서브넷에 배포됩니다. 
CIO(최고 정보 책임자)는 최근 저작권 규정 변경으로 인해 일부 국가에 대한 액세스를 제한하고자 합니다.

이러한 기준을 충족하는 조치는 무엇입니까?

A. 차단된 국가에서 들어오는 트래픽을 거부하도록 ALB Security Group을 수정합니다.

B. 차단된 국가에서 들어오는 트래픽을 거부하도록 EC2 인스턴스의 Security Group을 수정합니다.

C. Amazon CloudFront를 사용하여 응용 프로그램을 서비스하고 차단된 국가에 대한 액세스를 거부합니다.

D. ALB 수신기 규칙을 사용하여 차단된 국가의 수신 트래픽에 대한 액세스 거부 응답을 반환합니다.

<br>
<hr/>
<br>

<details>
<summary>영문 보기</summary>
<div markdown="1">
<br>

A. Modify the ALB security group to deny incoming traffic from blocked countries.

B. Modify the security group for EC2 instances to deny incoming traffic from blocked countries.

C. Use Amazon CloudFront to serve the application and deny access to blocked countries.

D. Use ALB listener rules to return access denied responses to incoming traffic from blocked countries.

</div>
</details>

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

저작권 등의 이유로 접속하는 국가에 따라 컨텐츠를 제한해야할 경우, CloudFront의 `지리적 제한` 기능을 사용하여 해당 국가로부터의 액세스를 제한할 수 있다.

</div>
</details>

<hr/>

## Prob. 8

7개의 Amazon EC2 인스턴스를 사용하여 기업은 AWS에서 웹 애플리케이션을 실행합니다. 
조직은 DNS 쿼리가 모든 정상 EC2 인스턴스의 IP 주소를 제공하기를 원합니다.

이 규정을 준수하려면 어떤 정책을 사용해야 합니까?

A. 단순 라우팅 정책

B. 지연 시간 라우팅 정책

C. 다중값 라우팅 정책

D. 지리 위치 라우팅 정책

<br>
<hr/>
<br>

<details>
<summary>영문 보기</summary>
<div markdown="1">
<br>

A. Simple routing policy

B. Latency routing policy

C. Multi-value routing policy

D. Geolocation routing policy

</div>
</details>

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

Multi-value routing policy를 사용하여 DNS 응답을 여러 리소스에 분산할 수 있다.<br>
에를 들어 라우팅 레코드를 Route53 상태 점검과 연결하려면 Multi-value routing policy를 사용해야 한다.

즉, DNS를 분산 시키려면 Multi-value 를 사용해야 하며, A. Single은 health check를 할 수 없지만 Multi-value는 가능하다.

</div>
</details>

<hr/>

## Prob. 9

매일 기업은 수백만 명의 소비자로부터 약 1'에 달하는 데이터를 수집합니다. 
회사는 고객에게 지난 12개월 동안의 사용 기록을 제공합니다. 
규제 및 감사 표준을 충족하려면 모든 사용 데이터를 최소 5년 동안 보관해야 합니다.

가장 저렴한 스토리지 옵션은 무엇입니까?

A. 데이터를 Amazon S3 Standard에 보관합니다. 1년 후 데이터를 S3 Glacier Deep Archive로 전환하는 라이프사이클 규칙을 설정합니다. 5년 후 데이터를 삭제하도록 수명 주기 규칙을 설정합니다.

B. 데이터를 Amazon S3 OneZone-Infrequent Access(S3 OneZone-IA)에 저장합니다. 1년 후 데이터를 S3 Glacier로 전환하는 라이프사이클 규칙을 설정합니다. 5년 후 데이터를 삭제하도록 수명 주기 규칙을 설정합니다.

C. Amazon S3 Standard에 데이터를 저장합니다. 1년 후 데이터를 S3 Standard-Infrequent Access(S3 Standard-IA)로 전환하도록 라이프사이클 규칙을 설정합니다. 5년 후 데이터를 삭제하도록 수명 주기 규칙을 설정합니다.

D. Amazon S3 Standard에 데이터를 저장합니다. 1년 후 데이터를 S3 One Zone-Infrequent Access(S3 One Zone-IA)로 전환하도록 라이프사이클 규칙을 설정합니다. 5년 후 데이터를 삭제하도록 수명 주기 규칙을 설정합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

Discussion에서 A와 B를 두고 논쟁하고 있다.
A가 맞는 이유는, 1년 후에는 규제 및 감사 표준만을 목적으로 데이터를 저장하는 것이기 때문에 거의 접근하지 않을 것이므로 Glacier Deep Archive에 보관하는것이 맞다.
또한 매일 수백만명의 소비자로부터 데이터를 수집하고, 고객이 얼마나 자신의 사용 기록을 조회할 지 모르기 때문에 스토리지 요금은 더 비싸지만 요청 및 데이터 검색 요금이 Standard-IA보다 더 싼 Standard를 선택하는 것이 올바르다.

</div>
</details>

<hr/>

## Prob. 10

기업은 Amazon RDS for PostgreSQL 데이터베이스 인스턴스를 사용하여 웹 서버 집합을 관리합니다. 
정상적인 규정 준수 검토 후 회사는 모든 프로덕션 데이터베이스에 1초 미만의 RPO(복구 시점 목표)를 갖도록 요구하는 표준을 설정합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. DB 인스턴스에 대해 Multi-AZ 배포를 사용합니다.

B. 하나의 가용성 영역에서 DB 인스턴스에 대해 자동 확장을 사용합니다.

C. 하나의 가용성 영역에 DB 인스턴스를 구성하고 별도의 가용성 영역에 여러 개의 읽기 복제본을 작성합니다.

D. 하나의 가용성 영역에서 DB 인스턴스를 구성하고 AWS DMS(AWS DMS) CDC(Change Data Capture) 작업을 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>영문 보기</summary>
<div markdown="1">
<br>

A. Enable a Multi-AZ deployment for the DB instance.

B. Enable auto scaling for the DB instance in one Availability Zone.

C. Configure the DB instance in one Availability Zone, and create multiple read replicas in a separate Availability Zone.

D. Configure the DB instance in one Availability Zone, and configure AWS Database Migration Service (AWS DMS) change data capture (CDC) tasks.

</div>
</details>

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A or D(불확실). A 유력

해설 : 

Discussion에서 대다수가 A를 답으로 지목하며 Multi-AZ를 사용하면 RPO를 1초미만을 보장한다고 하는데, 이를 뒷받침하는 어떠한 공식 문서도 찾을 수 없었다.

반면 D가 정답이라고 하는 사람은 Aurora라면 1초 미만의 RPO를 보장하지만 RDS는 그럴 수 없다고 말했다.

아래는 공식 문서에서의 DMS에 대한 설명이다.

    AWS DMS는 자동 페일오버를 제공합니다.
    어떤 이유로든 주 복제 서버에 장애가 발생할 경우 백업 복제 서버가 서비스를 중단하지 않고 대신 사용할 수 있습니다.

+ 추가.<br>
[링크](https://aws.amazon.com/ko/blogs/database/managed-disaster-recovery-with-amazon-rds-for-sql-server-using-cross-region-automated-backups/)를 보면 RPO와 RTO 테이블이 나와있다. <br>
다만 SQL Server 환경이다. 만약 RDS Postgre와 SQL Server의 차이가 없다면 답은 A가 확정일 것이다.

</div>
</details>

<hr/>

* Ref
  - [ExamTopics](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate-saa-c02/view/)
