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

Amazon EventBridge로 Lambda함수를 호출하려면 아래와 같은 문구가 필요합니다.

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

A. 응용 프로그램의 가용성 윈도우 외에는 인스턴스를 중지합니다. 필요한 경우 인스턴스를 다시 시작합니다.

B. 응용 프로그램의 가용성 윈도우 외에는 인스턴스를 최대 절전 모드로 전환합니다. 필요한 경우 인스턴스를 다시 시작합니다.

C. 자동 스케일링을 사용하여 응용 프로그램의 가용성 윈도우 외에는 인스턴스를 축소합니다. 필요한 경우 인스턴스를 확장합니다.

D. 응용 프로그램의 가용성 윈도우 외에는 인스턴스를 종료합니다. 필요한 경우 미리 구성된 AMI(Amazon 시스템 이미지)를 사용하여 인스턴스를 시작합니다.

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

최대 절전 모드(Hiberate)를 사용하면 인스턴스의 메모리를 보존한 채로 인스턴스를 중지시킬 수 있습니다.
(응용 프로그램의 가용성 윈도우 외에는 = 매일 12시간 외에는)

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

A -> 간단하게 운영 노력을 최소화하는 것은 지역간 복제
B -> CORS(Cross-Origin 리소스 공유)는 한 도메인에서 로드되어 다른 도메인에 있는 리소스와 상호 작용하는 클라이언트 웹 애플리케이션에 대한 방법을 정의,브라우저가 웹서버에 다른 출처에서 요청한 콘텐츠를 표시하도록 허용하는 HTTP기능
C, D -> A에서 라이프사이클 관리 규칙/이벤트 알림 등의 추가적인 작업

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

A(변경 불가능한 감사 로그) <br>
CloudTrail(계정) 로그 파일 무결성에 대한 유효성 검사를 실행

E(데이터 보안) <br>
다음 보안 모범 사례에서는 CloudTrail의 데이터 보호도 해결하고 <br>
AWS KMS 관리 키(SSE-KMS)로 CloudTrail 로그 파일 암호화

그 외에도 <br>
CloudTrail에 대한 Amazon S3 버킷 정책 <br>
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

A. Amazon S3에 대한 VPC 엔드포인트을 구성합니다. S3 엔드포인트에 대한 프라이빗 서브넷의 경로 테이블에 항목을 추가합니다.

B. 퍼블릭 서브넷에서 NAT 게이트웨이를 구성합니다. NAT 게이트웨이를 사용하도록 프라이빗 서브넷의 경로 테이블을 구성합니다.

C. Amazon S3를 EC2 인스턴스에 파일 시스템 마운트 지점으로 구성합니다. 마운트를 통해 Amazon S3에 액세스합니다.

D. EC2 인스턴스를 퍼블릭 서브넷으로 이동합니다. 인터넷 게이트웨이를 가리키도록 퍼블릭 서브넷 경로 테이블을 구성합니다.

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
Answer : A

해설 : 

A -> VPC 엔드포인트 보안 강화/비용 절감/서비스 제약/VPC 종속/권한 제어 이점

VPC 엔드포인트는 VPC 내 Resource들이 VPC 외부의 서비스(S3, Dynamo DB, Cloudwatch) 등에 접근할 때 Internet Gateway(직접), NAT Gateway(간접) 등의 외부 인터넷 전송 서비스를 타지 않고 내부 네트워크를 통해 접근할 수 있도록 지원하는 서비스

AWS VPC는 사설 네트워크로 이루어진 사용자 정의 네트워크로
VPC 내 EC2, RDS, ELB 등을 탑재하고 ENI(Elastic Network Interface)에 사설 IP 혹은 공인 IP를 부여하여 사용
다른 AWS 서비스 S3, Cloudwatch, Cloudfront, Dynamo DB, API Gateway 등은 Region 내에 존재하지만, VPC 내부에 설치하는 서비스들이 아님(즉, 따로 공인 IP를 가지고 외부에서 접근하는 서비스)

![1](/assets/img/study_AWS/[SAA]_ExamTopics_1~10/1.PNG)
VPC 내부 Resource와 기타 AWS Service Endpoint와 통신 시 외부 인터넷에 공개적으로 연결되며 트래픽이 노출(VPC 밖에서 들어오는 트래픽에는 추가 과금)

![2](/assets/img/study_AWS/[SAA]_ExamTopics_1~10/2.PNG)
만일 내부 사용자(관리자)가 사용하는 형태라면, 보안을 위해 외부로 나가지 말고 내부 네트워크로 접근해서 사용하자는 취지

* Interface Endpoint : ENI(Elastic Network Interface)를 이용하여 Private IP를 만들어서 서비스로 연결해줌 (SQS, SNS, Kinesis, Sagemaker 등 많은 서비스를 지원)
* Gateway Endpoint : 라우팅 테이블에서 경로의 대상으로 지정하여 사용(S3, DynamoDB 일부만 지원)

C -> 마운트는 파일 시스템이나 다른 디스크HW 등을 디렉토리에 연결하는 것으로 내부적으로 직접 지정(PnP기능은 자동적)

B, D -> 퍼블릭 서브넷에 대한 이야기여서 제외

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

C. 인스턴스를 버스터블 성능 DB 인스턴스 클래스로 변경합니다.

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

DB에서 클래스/스토리지/다중 AZ 설정를 선택할 수 있는데 
클래스는 Standard/메모리 최적화/버스터블이 있고,
스토리지는 범용/IOPS/프로비저닝된 IOPS/마그네틱
문제상 병목 현상이 발생하는 이유는 스토리지 성능입니다.

A -> 범용 SSD보다 더 성능이 좋은 프로비전된 IOPS SSD를 사용하면 병목 현상이 해결

B -> 높은 처리 성능이 요구되는 데이터베이스용이며, 더 많은 데이터를 저장할 수 있어 쿼리 시간이 빨라짐

C -> 순간 확장 가능한 인스턴스로 개발, 테스트, 다른 비프로덕션 데이터베이스를 위한 인스턴스

D -> 다중 AZ 배포를 통해 여러 가용 영역에 데이터베이스 인스턴스 여러 개를 배포하여 기본/예비 인스턴스를 두어 중단되면 대략 2분 이내 장애 조치가 수행하여 계속 운영 (만든 후에 다중 AZ를 구성할 수 있으나 이 경우 성능이 상당히 떨어지므로 유지 관리 주기를 짧게함)

스토리지는 IOPS(Input/Output Operations Per Second)를 사용해 스토리지의 속도를 측정하는데, 초기 설정값이 임계값이 되어 그 성능을 초과할 수 없음
단일 Input/Output 작업에서 전송할 수 있는 데이터의 양은 페이지 크기에 달려있으며, 필요한 디스크 처리량을 알아야합니다. (MySQL/MariaDB 16KB 나머지 8KB)

프로비저닝된 IOPS SSD는 순간 확장 개념이 없고 사용 여부와 관계없이 일정한 성능이 제공되고 그에 따른 비용이 청구되므로, 일관된 짧은 지연 시간에 성능이 필요한 OLTP 데이터베이스에 유용

마그네틱은 구형 인스턴스의 호환성을 위해 마그네틱 스토리지를 제공하며, 최대 크기는 4TB, 최대 성능은 1,000 IOPS

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

A -> 재해 상황이므로 데이터는 한 번 수집 후 말 것이기 때문에, Snowball Edge device(엣지 컴퓨팅 및 데이터 전송 디바이스)면 외진 환경에서의 로컬 데이터 프로세싱 및 수집을 지원하기에 충분

AWS Snow Family 콘솔에서 Snowball Edge Compute Optimized 또는 Snowball Edge Storage Optimized 중 원하는 디바이스를 선택합니다. Amazon S3 버킷으로 작업을 생성하고 추적을 위해 Amazon Simple Notification Service(Amazon SNS)를 선택한 다음 Amazon EC2 AMI 및 GPU와 같은 옵션을 구성

디바이스가 도착하면 전원을 켜고 AWS OpsHub를 사용하여 잠금 해제합니다. LAN에 연결하고 AWS OpsHub를 사용하여 디바이스 관리, 데이터 전송 또는 EC2 인스턴스 실행 등의 작업을 수행합니다. 완료되면 디바이스 전원을 끄고 AWS에 디바이스를 반환

디바이스가 AWS 리전에 도착하면 사용자의 온보드(내장) 버킷에 저장된 모든 데이터가 S3 버킷으로 이동되며 디바이스를 로드하는 데 걸리는 것과 비슷한 시간 안에 확인됩니다. 그런 다음 모든 데이터는 장치에서 안전하게 지워지고 모든 고객 정보는 삭제

디바이스를 사용하여 엄청난 양의 데이터를 Amazon S3로 또는 Amazon S3에서 외부로 이동 가능

B -> 하나의 서비스에서 다른 서비스로 메시지를 안전하게 전달하기 위한 서비스로
느슨한 연결 Failover가 가능하며 더 적은 API 호출을 실시하여 더 높은 처리량을 보여주는 자주 사용되는 시스템

C -> 스트리밍 데이터 파이프라인은 실시간 스트리밍 데이터를 안정적으로 캡처하고 전환하여 데이터 레이크, 데이터 스토어, 분석 서비스에서 AWS 서비스 및 스트리밍 대상(S3 및 Redshift)으로 전달하는 추출, 전환, 적재(ETL) 서비스

D -> 또한 Storage Gateway는 거의 무제한의 클라우드 스토리지 액세스를 온프레미스에 제공하는 하이브리드 클라우드 스토리지 서비스 세트임 그리고 compute(EC2)가 없지만 Snowball에는 있음

</div>
</details>

<hr/>

## Prob. 6

회사에서 데이터 저장을 위해 Amazon DynamoDB 테이블을 사용할 계획입니다. 
회사는 비용 최적화에 대해 우려하고 있습니다. 
이 테이블은 대부분의 아침 저녁에 사용되지 않습니다. 
읽기 및 쓰기 트래픽은 종종 예측할 수 없습니다. 
트래픽 스파이크(다양한 트래픽 패턴)가 발생하면 매우 빠르게 발생합니다.

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

DynamoDB는 NoSQL 기반 데이터베이스로 테이블 생성이 단순하고 신속/자동으로 스토리지를 늘리고 클러스터를 확장하여 데이터를 분산/읽기와 쓰기 처리량(Read/Write Throughput) 직접 지정으로 프로비저닝된 처리량/리소스 사용률 및 성능 지표 모니터링/복제하여 고가용성과 데이터 내구성을 제공/암호화로 중요한 데이터 보호/보조 인덱스와 SSD로 빠른 조회 속도를 제공/온디맨드 백업으로 특정 시점으로 복구/키 값 데이터 모델 사용/데이터 유지 시간(TTL)으로 자동 삭제 등의 특징

검색을 하려면 기본 키로 인덱스를 생성하며 기본 키는 테이블 생성시 반드시 지정하는데 이것을 테이블 인덱스라고함 그리고
Hash 형식 기본 키는 단일키
Hash + Range 형식 기본 키는 복합키

테이블 인덱스 이외에 보조 인덱스 유형 생성으로 검색 성능을 높일 수 있음
로컬 보조 인덱스(Local Secondary Index)은 해시 기본 키와 범위 기본 키를 사용하고 있을 때만 생성 가능하며 해시 키 -> 해시 기본 키(테이블 인덱스와 같음), 범위 키 -> 목적에 따라 다르게 설정
글로벌 보조 인덱스(Global Secondary Index)은 해시 키 -> 테이블 인덱스와 다르게 설정, 범위 키 -> 테이블 인덱스와 다르게 설정(생략 가능)

A -> 점심에만 활발하게 사용되는게 온디맨드에 매우 적합한 상황
B -> 글로벌 보조 인덱스는 검색 성능만을 높일 수 있음
C -> DynamoDB는 기본적으로 프로비저닝과 자동 확장이 있음
D -> 글로벌 테이블

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

Elastic Load Balancing(ELB)은 둘 이상의 가용 영역에서 EC2 인스턴스, 컨테이너, IP 주소 등 여러 대상에 걸쳐 수신되는 트래픽을 자동으로 분산하고 등록된 대상의 상태를 모니터링하면서 상태가 양호한 대상으로만 트래픽을 라우팅합니다. Elastic Load Balancing은 수신 트래픽이 시간이 지남에 따라 변경됨에 따라 로드 밸런서를 확장합니다. 대다수의 워크로드에 맞게 자동으로 조정 가능
유형으로는 Application Load Balancers/Network Load Balancers/Gateway Load Balancers/Classic Load Balancer 지원

Application Load Balancer 구성 요소
로드 밸런서 -> 클라이언트에 대한 단일 접점 역할을 수행
리스너 -> 구성한 프로토콜 및 포트를 사용하여 클라이언트의 연결 요청을 확인
대상 그룹 -> EC2 인스턴스 같은 하나 이상의 등록된 대상으로 요청을 라우팅

Application Load Balancer는 개방형 시스템 간 상호 연결(OSI) 모델의 일곱 번째 계층인 애플리케이션 계층에서 작동합니다. 로드 밸런서는 요청을 받으면 우선 순위에 따라 리스너 규칙을 평가하여 적용할 규칙을 결정한 다음, 규칙 작업의 대상 그룹에서 대상을 선택합니다. 애플리케이션 트래픽의 콘텐츠를 기반으로 다른 대상 그룹에 요청을 라우팅하도록 리스너 규칙을 구성할 수 있습니다. 대상이 여러 개의 대상 그룹에 등록이 된 경우에도 각 대상 그룹에 대해 독립적으로 라우팅이 수행됩니다. 대상 그룹 레벨에서 사용되는 라우팅 알고리즘을 구성할 수 있습니다. 기본 라우팅 알고리즘은 라운드 로빈입니다. 
그 대신 최소 미해결 요청 라우팅 알고리즘을 지정할 수 있습니다.

A -> Security Group은 구성요소에 없음
B -> EC2 인스턴스의 Security Group을 수정으로 인바운드 및 아웃바운드 트래픽을 제어하는 가상 방화벽 역할하는데 일부 국가에 대한 제한은 모르겠음
C -> 저작권 등의 이유로 접속하는 국가에 따라 컨텐츠를 제한해야할 경우, CloudFront의 `지리적 제한` 기능을 사용하여 해당 국가로부터의 액세스를 제한
D -> ALB 수신기 규칙은 트래픽을 분산하고 모니터링

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

Route53는 AWS에서 제공하는 DNS(Domain Name Service)로 일반 DNS동작 과정은 도메인을 IP로 변환하여 IP 네트워크 통신하여 목적지를 찾아가는 것인데 다른점은
1. PC -> 기본 UDP 53으로 질의/응답 -> Cache DNS -> ROOT -> .com ROOT -> 네임서버(AWS Route53)으로 Route53에서 네임서버 등록시 순서가 다름
즉, 일반적으로 도메인 등록 시, 등록대행기관에 네임서버를 지정 / Route53에서는 NS레코더를 할당받은후 네임서버 정보를 도메인 등록대행기관(가비아, 아이네임즈, 후이즈) 사이트에 접속해 네임서버를 지정
2. Route53은 퍼블릭 호스트 존/프라이빗 호스트 존이 있음
즉, 퍼블릭 존은 일반 네임 서버로 글로벌하게 동작 / 프라이빗 존은 AWS내에서만 동작
3. Route53 특이 레코더, ALIAS(별칭)이 있음
즉, www가 없어도 IP만으로 응답 가능함
이고 기능으로 DNS(네임서버), 모니터링, L4(Failover), GSLB(글로벌 서버 로드 밸런싱)를 제공

레코드를 생성할 때 라우팅 정책을 선택하게 되는데, 이는 Amazon Route 53이 쿼리에 응답하는 방식을 결정합니다.

* `단순 라우팅 정책`(Simple routing policy) - 도메인에 대해 특정 기능을 수행하는 하나의 리소스만 있는 경우(예: example.com 웹 사이트의 콘텐츠를 제공하는 하나의 웹 서버)에 사용합니다. 단순 라우팅을 사용하여 프라이빗 호스팅 영역에서 레코드를 생성할 수 있습니다.

* 장애 조치 라우팅 정책(Failover routing policy) - 액티브-패시브 장애 조치를 구성하려는 경우에 사용합니다. 장애 조치 라우팅을 사용하여 프라이빗 호스팅 영역에서 레코드를 생성할 수 있습니다.

* `지리 위치 라우팅 정책`(Geolocation routing policy) - 사용자의 위치에 기반하여 트래픽을 라우팅하려는 경우에 사용합니다. 지리적 위치 라우팅을 사용하여 프라이빗 호스팅 영역에서 레코드를 생성할 수 있습니다.

* 지리 근접 라우팅 정책(Geoproximity routing policy) - 리소스의 위치를 기반으로 트래픽을 라우팅하고 필요에 따라 한 위치의 리소스에서 다른 위치의 리소스로 트래픽을 보내려는 경우에 사용합니다.

* `지연 시간 라우팅 정책` - 여러 AWS 리전에 리소스가 있고 최상의 지연 시간을 제공하는 리전으로 트래픽을 라우팅하려는 경우에 사용합니다. 지연 시간 라우팅을 사용하여 프라이빗 호스팅 영역에서 레코드를 생성할 수 있습니다.

* IP 기반 라우팅 정책 - 사용자의 위치에 기반하여 트래픽을 라우팅하고 트래픽이 시작되는 IP 주소가 있는 경우에 사용합니다.

* `다중 응답 라우팅 정책`(Multivalue answer routing policy) - Route 53이 DNS 쿼리에 무작위로 선택된 최대 8개의 정상 레코드로 응답하게 하려는 경우에 사용합니다. 다중 값 응답 라우팅을 사용하여 프라이빗 호스팅 영역에서 레코드를 생성할 수 있습니다.

* 가중치 기반 라우팅 정책(Weighted routing policy) - 사용자가 지정하는 비율에 따라 여러 리소스로 트래픽을 라우팅하려는 경우에 사용합니다. 가중치 라우팅을 사용하여 프라이빗 호스팅 영역에서 레코드를 생성할 수 있습니다.

A -> 단순히 하나의 웹 서버에만 접근
B -> 오래걸리는 작업을 하는 리소스에 대한 접근
C -> Multi-value routing policy를 사용하여 DNS 응답을 여러 리소스에 분산할 수 있다.<br>
예를 들어 라우팅 레코드를 Route53 상태 점검과 연결하려면 Multi-value routing policy를 사용해야 함
즉, DNS를 분산 시키려면 Multi-value 를 사용해야 하며, A. Single은 health check를 할 수 없지만 Multi-value는 가능
D -> 사용자의 위치에 기반하여 접근

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

S3는 최고의 확장성, 데이터 가용성, 보안 및 성능을 제공하는 객체 스토리지 서비스으로 클래스 유형으로
* 스탠다드(Standard) -> 가장 일반적인 요금제/비싼 스토리지 요금, 저렴한 트래픽 요금/자주 액세스하는 데이터에 적합

* 스탠다드-IA(Standard Infrequent Access) -> 스탠다드에 비해서 스토리지 요금은 저렴하나 트래픽 요금은 비싸짐/사용 빈도가 다소 낮은 데이터에 적합/ex) 추후에 기사가 이슈화

* 단일 영역-IA(One Zone-IA) -> 스탠다드-IA에 비해서 스토리지 요금이 더 저렴하고 트래픽 요금은 같음/사용 빈도가 낮고 중요도가 떨어지는 데이터에 적합/ex) 트래픽 로그와 같은 많이 발생하지만 없어져도 당장의 큰 영향을 주지 않는 데이터

* 지능형 계층화(Intelligent-Tiering) -> 주로 예측할 수 없는 워크로드에 사용됨/데이터를 가장 비용 효율적인 계층으로 자동 이동하여 스토리지 비용을 최적화 하도록 설계됨/약간의 월별 객체 모니터링 및 자동화 요금이 지불됨

* 글래시어(Glacier) -> 위 클래스들보다도 더 저렴한 스토리지 요금을 갖지만 훨씬 비싼 트래픽 요금을 가짐/사용 빈도가 극히 낮은 데이터에 적합/Instant Retrieval(분기에 한 번 액세스하는 장기 아카이브 데이터용),Flexible Retrieval(장기 백업 및 아카이브용),Deep Archive(일년에 한두 번 액세스하고 장기 데이터 아카이브용)

* 증복성 감소(Reduced Redundancy) -> 중요하지 않은 데이터 보관용/해당 스토리지는 사용하지 않는 것 Standard가 비용 대비 효과적이라고 함


A -> 1년 후에는 규제 및 감사 표준만을 목적으로 데이터를 저장하는 것이기 때문에 거의 접근하지 않을 것이므로 Glacier Deep Archive에 보관하는것이고
또한 매일 수백만명의 소비자로부터 데이터를 수집하고, 고객이 얼마나 자신의 사용 기록을 조회할 지 모르기 때문에 스토리지 요금은 더 비싸지만 요청 및 데이터 검색 요금이 Standard-IA보다 더 싼 Standard를 선택하는 것이 맞음
B -> 매일 수백만의 소비자에게 트래픽에 대한 요금이 비쌈
C, D -> 1년 후에는 데이터를 보관하는 것에 초점이라 Glacier 유형에서 찾아야함, 없다면 스토리지 요금이 싸기 때문에 단일보단 스탠다드가 더 좋을듯

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

D. 하나의 가용성 영역에서 DB 인스턴스를 구성하고 AWS DMS(AWS Database Migration Service) CDC(Change Data Capture) 작업을 구성합니다.

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
Answer : A

해설 : 

Amazon RDS는 쉽게 설정, 운영 및 확장할 수 있는 웹 서비스로 AWS 클라우드의 관계형 데이터베이스를 비용 효율적이고 크기 조정 가능한 용량 관리 작업을 하는 완전관리형 서비스 그리고 `Amazon RDS`이외의 `Amazon Aurora 데이터베이스 엔진`을 다룹니다. 이점으로는
* 이미 익숙한 데이터베이스 제품을 사용가능
* 백업, 소프트웨어 패치, 자동 장애 감지 및 복구
* 자동 백업을 켜거나 수동으로 백업 가능(스냅샷으로 증분식)
* 기본 인스턴스와 동기식으로 고가용성을 얻음
* 데이터베이스 패키지의 보안 외에도 사용자를 제어하는 데 도움
AWS 리전 및 가용 영역/Multi-AZ/보안/모니터링/프록시 등을 지원

Amazon RDS 사용자 지정 for Oracle 및 Microsoft SQL Server은 액세스 권한을 부여하는 RDS 관리 유형(환경)이며 운영 체제/데이터베이스를 오프로드(작업량을 적절히 분배)/Amazon RDS의 자동화를 결합하고 Amazon EC2의 유연성을 제공

Amazon RDS on AWS Outposts는 RDS for SQL Server/MySQL/PostgreSQL 데이터베이스 AWS 아웃포스트(프로비저닝?) 환경으로 확장

A -> Multi-AZ를 사용하면 RPO를 1초미만을 보장한다고 하는데, 이를 뒷받침하는 어떠한 공식 문서도 찾을 수 없음. Aurora Global Database에서는
**1초의 RPO(Recovery Point Objective, 복구 목표 지점)** - 1초 전까지의 데이터는 안전이 보장됩니다. <br>
**1분 미만의 RTO(Recovery Time Objective, 복구 목표 시간)** - 1분 내에 복구가 보장됩니다.

B -> 자동 확장 기능으로는 RPO는 결국 같은 가용 영역 보장 못함 
C -> 읽기에 대한 복제본은 처리량을 늘리기 위한 것임
D -> Aurora라면 1초 미만의 RPO를 보장하지만 RDS는 그럴 수 없다는 말이 있음

아래는 공식 문서에서의 DMS에 대한 설명입니다.
  * AWS DMS는 `자동 페일오버를 제공`합니다.
    어떤 이유로든 주 복제 서버에 `장애가 발생`할 경우 `백업 복제 서버`가 서비스를 중단하지 않고 `대신 사용`할 수 있습니다.

+ 추가.<br>
[링크](https://aws.amazon.com/ko/blogs/database/managed-disaster-recovery-with-amazon-rds-for-sql-server-using-cross-region-automated-backups/)를 보면 RPO와 RTO 테이블이 나와있다. <br>
다만 SQL Server 환경이다. 만약 RDS Postgre와 SQL Server의 차이가 없다면 답은 A가 확정일 것입니다.

</div>
</details>

<hr/>

* Ref
  - [ExamTopics](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate-saa-c02/view/)
