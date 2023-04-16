---
layout: post
title: "[AWS-SAA] Examtopics 61~70"
subtitle: AWS
date: '2023-03-21 00:00:01 +0900'
category: study
tags: aws aws-saa
image:
  path: /assets/img/study_AWS/saa-co2_logo.png
---

SAA Examtopics 61~70번 문제를 풀어보자.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## Prob. 61

Amazon EC2에서 기업은 Amazon RDS 데이터베이스에 의해 백업되는 매우 안전한 애플리케이션을 운영하고 있습니다. 모든 개인 식별 정보(PII)는 규정 준수 표준을 준수하기 위해 저장 시 암호화되어야 합니다.

최소한의 인프라 변경으로 이러한 요구 사항을 달성하기 위해 솔루션 설계자는 어떤 솔루션을 제안해야 합니까?

A. AWS 인증서 관리자를 배포하여 인증서를 생성합니다. 인증서를 사용하여 데이터베이스 볼륨을 암호화합니다.

B. AWS 클라우드를 구축합니다.HSM을 사용하여 암호화 키를 생성하고 CMK(고객 마스터 키)를 사용하여 데이터베이스 볼륨을 암호화합니다.

C. AWS KMS CMK(키 관리 서비스 고객 마스터 키)를 사용하여 SSL 암호화를 구성하여 데이터베이스 볼륨을 암호화합니다.

D. AWS KMS(키 관리 서비스) 키를 사용하여 Amazon EBS(Amazon Elastic Block Store) 암호화 및 Amazon RDS 암호화를 구성하여 인스턴스 및 데이터베이스 볼륨을 암호화합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

전송과 저장 시 암호화 문제 요점.

**개인 식별 정보(PII)**
개인 식별 정보(PII)는 주민등록번호, 이름, 이메일 주소와 같이 특정한 개인과 연결되어 개인의 신원을 밝히는 데 사용할 수 있는 모든 정보입니다.

**인증서**
인터넷 상에서 발생하는 모든 전자거래를 안심하고 사용할 수 있도록 공인인증기관이 발행한 사이버 거래용 인감증명서.

**HSM**
하드웨어 보안 모듈(HSM)은 데이터의 암호화 및 암호 해독에 사용되는 키를 생성, 보호, 관리하고 디지털 서명 및 인증서를 생성하여 암호화 프로세스를 보호하는 강화된 변조 방지 하드웨어 장치.

**SSL/TLS**
SSL은 보안 소켓 계층(Secure Sockets Layer)/TLS는 전송 계층 보안(Transport Layer Security)으로 웹사이트와 브라우저 사이(또는 두 서버 사이)에 전송되는 데이터를 암호화하여 인터넷 연결을 보호하기 위한 표준 기술.

**AWS KMS**
Key Management Service 의 약자로, 데이터를 암호화 할때 사용되는 암호화 Key 를 안전하게 관리하는데 목적을 둔 서비스.
* AWS managed key - AWS 서비스들이 KMS 를 통해 Key를 서비스 받는 것으로, 내부적으로 자동으로 일어나게 되며 사용자가 직접적으로 제어가 불가능
* Customer managed key (CMK) - 사용자가 직접 key를 생성하고 관리하는 것, CMK 에 대한 제어는 IAM 을 통해 권한을 부여 받아 제어가 가능
* Custom key stores - AWS 에서 제공하는 또다른 key 관리형 서비스인 CloudHSM 을 활용한 Key 관리 형태를 의미.

AWS Key Management Service(KMS)는 AWS CloudHSM과 다른점?
KMS는 Shared 형태의 managed 서비스 이며, CloudHSM은 dedicated managed 서비스로 사용자 VPC의 EC2에 HSM(Hardware Security Module) 을 올려서 서비스되는 형태라고 보면 된다. 결국 CloudHSM이 조금 더 강력한 형태의 보안 안정성을 제공한다고 이해.

A 탈락 -> AWS 인증서 관리자로 생성하지만 인증서는 데이터 자체를 암호화해서 저장하는 것이 아니라 부적합.

B 탈락 -> 클라우드에 모듈과 DB볼륨을 새로 구축하는 것은 최소 인프라 변경도 아니라 부적합.

C 탈락 -> CMK는 적합하지 않으며 SSL은 인증서와 같이 데이터 자체를 암호화해서 저장하는 것이 아니라 부적합.

D 정답 -> KMS에서 암호화 키를 관리하며 EBS(EC2)와 DB볼륨(RDS)를 암호화하여 적합.

</div>
</details>

<hr/>

## Prob. 62

솔루션 설계자가 설정한 IAM 정책은 다음과 같습니다.

![prob_62](/assets/img/study_AWS/[SAA]_ExamTopics_61~70/prob_62.png)

정책에서 허용할 액션은 무엇입니까?

A. AWS 람다 기능은 모든 네트워크에서 삭제할 수 있습니다.

B. AWS 람다 함수는 모든 네트워크에서 만들 수 있습니다.

C. AWS 람다 기능은 100.220.0.0/20 네트워크에서 삭제할 수 있습니다.

D. 220.100.16.0/20 네트워크에서 AWS 람다 기능을 삭제할 수 있습니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

정책 문제 요점.

사용자는 모든 리소스에 대한 람다 함수 작업 허용.
사용자는 모든 리소스에 대한 람다 기능인 생성/삭제 작업 거부. 만약 220.100.16.0/20 네트워크면

0 : 네트워크 어드레스<br>
1 : VPC Router<br>
2 : DNS<br>
3 : Future use<br>
4 : Broadcast<br>

A 탈락 -> 람다 기능은 특정 네트워크에서 삭제 불가하여 부적합.

B 탈락 -> 람다 기능은 특정 네트워크에서 생성 불가하여 부적합.

C 정답 -> 람다 기능은 100.220.0.0/20 네트워크에서 삭제 가능하여 적합.

D 탈락 -> 특정 네트워크에서 람다 기능의 삭제 불가하여 부적합.

</div>
</details>

<hr/>

## Prob. 63

Amazon Aurora에서 기업은 데이터베이스를 운영하고 있습니다. 매일 밤 데이터베이스는 비활성화됩니다. 사용자 트래픽이 이른 시간에 급증하면 데이터베이스에서 많은 양의 읽기를 수행하는 애플리케이션이 성능 문제에 직면하게 됩니다. 이러한 피크 시간 동안 데이터베이스에서 읽을 때 프로그램에서 시간 초과 문제가 발생합니다. 전담 운영 인력이 없기 때문에 조직은 성능 문제를 해결하기 위한 자동화된 솔루션이 필요합니다.

데이터베이스가 증가하는 읽기 로드에 자동으로 조정되도록 솔루션 설계자가 취해야 하는 활동은 무엇입니까? (2개를 선택하세요.)

A. 데이터베이스를 Aurora Serverless로 마이그레이션합니다.

B. Aurora 데이터베이스의 인스턴스 크기를 늘립니다.

C. Aurora 복제본으로 Aurora 오토 스케일링을 구성합니다.

D. 데이터베이스를 Aurora Multi-Master 클러스터로 마이그레이션합니다.

E. MySQL Multi-AZ 배포를 위해 데이터베이스를 Amazon RDS로 마이그레이션합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A, C

해설 : 

증가하는 읽기 로드에 자동으로 조정 문제 요점.

- 여기서 문제는 트래픽 급증 시 읽기 크기를 자동으로 조정하는 것입니다

**AWS Aurora Serverless**
Amazon Aurora의 온디맨드 Auto Scaling 구성.
요구 사항을 기반으로 자동으로 시작 및 종료하고 용량을 확장 또는 축소.
데이터베이스 용량을 관리하지 않거나 미리 프로비전을 않해도 클라우드에서 실행
Single AZ/Multi-AZ Failover/기본적으로 암호화됨/Replica 불가능/VPC 밖에서 액세스 불가능/클로닝 불가능/Backtrack 불가능/Region VPC Peering 불가능.
Request Router - Instance Layer - Storage Layer.

A 정답 -> DB를 Aurora Serverless로 데이터 이동을 하여 오토 스케일링되어 적합. <br>
https://aws.amazon.com/rds/aurora/serverless/

B 탈락 -> 사용량이 적은 기간에는 초과 용량이 사용되지 않아 부적합.

C 정답 -> Aurora 복제본을 사용하여 Aurora 오토 스케일링하여 적합.<br>
https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Integrating.AutoScaling.html

D 탈락 -> 데이터베이스를 Aurora 다중 마스터 클러스터로 데이터 이동해도 쓰기 성능만 증가하여 부적합.<br>

이는 읽기가 아닌 쓰기 확장에 도움이 됩니다. - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-multi-master.html

E 탈락 -> MySQL Multi-AZ 배포를 위해 데이터베이스를 Amazon RDS로 데이터 이동해도 장애에 대한 가용성이 증가하여 부적합.<br>

이는 가용성 및 재해 복구를 위한 것이지 읽기 확장을 위한 것이 아닙니다. <br>
대기 인스턴스는 읽기 또는 쓰기를 제공하는 데 사용되지 않습니다. <br>
액티브-패시브 페일오버가 채택되었습니다.<br>
https://aws.amazon.com/rds/features/multi-az/

</div>
</details>

<hr/>

## Prob. 64

Amazon EC2 인스턴스 기반 애플리케이션은 Amazon DynamoDB 데이터베이스에 대한 액세스 권한이 필요합니다. EC2 인스턴스와 DynamoDB 테이블은 모두 동일한 AWS 계정으로 관리됩니다. 권한은 솔루션 설계자가 구성해야 합니다.

DynamoDB 테이블에 대한 EC2 인스턴스 최소 권한 액세스를 제공하는 접근 방식은 무엇입니까?

A. DynamoDB 테이블에 대한 액세스를 허용하는 적절한 정책을 사용하여 IAM 역할을 만듭니다. 인스턴스 프로필을 생성하여 이 IAM 역할을 EC2 인스턴스에 할당합니다.

B. DynamoDB 테이블에 대한 액세스를 허용하는 적절한 정책을 사용하여 IAM 역할을 만듭니다. EC2 인스턴스를 신뢰 관계 정책 문서에 추가하여 역할을 수행할 수 있도록 합니다.

C. DynamoDB 테이블에 대한 액세스를 허용하는 적절한 정책을 사용하여 IAM 사용자를 만듭니다. 자격 증명을 Amazon S3 버킷에 저장하고 애플리케이션 코드 내에서 직접 읽습니다.

D. DynamoDB 테이블에 대한 액세스를 허용하는 적절한 정책을 사용하여 IAM 사용자를 만듭니다. 응용 프로그램이 IAM 자격 증명을 로컬 스토리지에 안전하게 저장하고 이를 사용하여 DynamoDB를 호출하는지 확인합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

최소 권한 액세스 문제 요점.

모든 인증 시스템은 나는 누구인가?/무엇을 할 수 있습니까?라는 핵심 부분이 있음.
IAM을 사용하면 사용자가 액세스할 수 있는 AWS 리소스를 제어하는 권한을 중앙에서 관리 가능. -> 인증(로그인) 및 권한 부여(권한 있음)된 대상을 제어
* IAM 사용자는 단순히 "나는 누구인가?". -> 사용자, 그룹
* IAM 역할은 단순히 "무엇을 할 수 있습니까?". -> 리소스
* 이러한 것을 정의한 JSON문서 -> 정책

역할은 사용자, Amazon 서비스 및 EC2 인스턴스와 같이 "내가 누구인가?"를 정의하는 다른 보안 주체가 "가정"하도록 설계되었습니다.<br>
그러나 인스턴스 프로필은 "나는 누구인가?"를 정의합니다 IAM 사용자가 사용자를 나타내는 것처럼 인스턴스 프로필은 EC2 인스턴스를 나타냅니다. <br>
https://medium.com/devops-dudes/the-difference-between-an-aws-role-and-an-instance-profile-ae81abd700d#:~:text=Roles%20are%20designed%20to%20be,instance%20profile%20represents%20EC2%20instances.

정책은 자격 증명 또는 리소스에 연결될 때 해당 권한을 정의하는 AWS의 객체.
자격 증명 기반 정책 또는 리소스 기반 정책을 선택.
* 자격 증명 기반 정책 - IAM 사용자, 그룹 또는 역할에 연결/관리형 권한 또는 인라인 권한.
* 리소스 기반 정책 - 리소스에 연결/인라인만 있고 관리형은 없음.

**IAM 역할**
IAM 역할은 계정에 생성할 수 있는, 특정 권한을 지닌 IAM 자격 증명입니다. AWS에서 자격 증명이 할 수 있는 것과 없는 것을 결정하는 권한 정책을 갖춘 AWS 자격 증명이라는 점에서 IAM 역할은 IAM 사용자와 유사.
일반적으로 조직의 AWS 리소스에 대한 액세스 권한이 없는 사용자나 서비스에 액세스 권한을 위임.

사용 권한 컬렉션을 정의하는 메커니즘을 제공합니다. 관리형 정책과 인라인 정책을 역할에 할당하여 작업 권한을 부여합니다. 그러나 역할은 그 자체로 특정한 사람이나 사물이 아닙니다. 역할은 "나는 누구인가?"를 정의하지 않음.

**IAM 사용자**
* 루트 사용자
결제 관리를 포함한 계정의 모든 권한**을 가지고 있음.
관리 목적 이외에 다른 용도로 사용하지 않는 것을 권장.
탈취 되었을때 복구가 매우 어려움 -> MFA를 설정하는 것을 권장.
MFA(Multi-factor authentication) - 일회용 패스워드를 생성하여 로그인(OTP).

* IAM 사용자
IAM을 통해 생성해서 사용하는 사용자.
한 사람 혹은 하나의 애플리케이션을 의미.
설정 시 콘솔 로그인 권한 부여 가능.
설정 시 AWS 서비스를 이용할 수 있음.
Access Key ID (유저 이름에 해당).
Secret Access Key (비밀번호에 해당).
AdminAccess(모든 기능)를 부여하더라도 루트 사용자로 별도의 설정을 하지 않으면 Billing(결제)기능을 사용할 수 없음.

**인스턴스 프로필**
인스턴스 프로필은 "나는 누구인가?"를 정의.
IAM 사용자가 개인을 나타내는 것처럼 인스턴스 프로필은 EC2 인스턴스를 나타냅니다. EC2 인스턴스 프로필이 가진 유일한 권한은 역할을 수임하는 권한.

따라서 EC2 인스턴스는 EC2 인스턴스 프로필에서 실행되며 인스턴스가 "누구"인지 정의합니다. 그런 다음 IAM 역할을 "가정"하여 궁극적으로 모든 실질적인 힘을 부여합니다.

**신뢰 관계 정책**
역할을 수임하도록 신뢰하는 보안 주체를 정의하는 JSON 정책 문서.
신뢰 정책은 역할을 위임하도록 허용된 신뢰할 수 있는 계정 멤버를 지정.
신뢰하는 계정의 역할에 연결되어 있고 권한의 절반에 해당합니다. 나머지 절반은 사용자에게 역할 전환 또는 위임을 허용하는 신뢰받는 계정의 사용자에게 연결된 권한 정책.
임시로 역할을 위임하는 사용자는 자신의 고유 권한을 포기하고 대신 해당 역할의 권한을 위임.
IAM의 역할에 연결된 필수 리소스 기반 정책입니다. 신뢰 정책에서 지정할 수 있는 보안 주체에는 사용자, 역할, 계정 및 서비스가 포함.

A 정답 -> IAM 역할(DB에 대한 권한)을 만들어 해당 인스턴스 프로필(누구인지)에 할당하여 적합.

B 탈락 -> IAM 역할(DB에 대한 권한)을 만들었지만 신뢰 관계 정책은 권한을 원래 있던 것을 다른 보안 주체에게 위임하는 것이라 부적합.

C 탈락 -> IAM 사용자(DB 자체)를 만들며 자격 증명을 S3에 저장하여 코드 내에서 직접 읽으면 보안적으로 부적합.

D 탈락 -> IAM 사용자(DB 자체)를 만들며 자격 증명을 로컬에 저장하여 부적합.

</div>
</details>

<br>
<hr/>
<hr/>

## Prob. 65

비즈니스는 Amazon EC2 인스턴스를 사용하여 API 기반 인벤토리 보고 애플리케이션을 운영합니다. 이 프로그램은 Amazon DynamoDB 데이터베이스를 사용하여 데이터를 저장합니다. 기업의 물류 센터는 API와 통신하는 온프레미스 배송 애플리케이션을 사용하여 배송 라벨을 생성하기 전에 인벤토리를 업데이트합니다. 매일 조직은 애플리케이션 중단으로 인해 트랜잭션이 누락되는 것을 목격했습니다.

솔루션 설계자는 애플리케이션의 탄력성을 높이기 위해 무엇을 제안해야 합니까?

A. 로컬 데이터베이스에 쓰도록 발송 응용 프로그램을 수정합니다.

B. AWS Lambda를 사용하여 서버 없이 실행되도록 애플리케이션 API를 수정합니다.

C. EC2 인벤토리 애플리케이션 API를 호출하도록 Amazon API Gateway를 구성합니다.

D. Amazon Simple Queue Service(Amazon SQS)를 사용하여 인벤토리 업데이트를 보내도록 응용 프로그램을 수정합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

중단으로 인해 트랜잭션이 누락 문제 요점.

사용자(클라이언트) -> API(인벤토리 업데이트 트랜잭션) -> 웹서버 -> DB

앱 사용자는 API로 해당 작업 트랜잭션을 웹서버로 보내는데 도중에 연결이 끊기거나 중단되면 장애가 발생하고 작업이 진행되지 않음.
앱의 탄력성을 높이기 위해 장애 극복을 해야함.

A 탈락 -> 로컬 DB에 발송해도 결국 앞에서 시행되는 트랜잭션이 중단되면 소용 없기 때문에 부적합.

B 탈락 -> 서버리스 Lambda를 앱 API를 수정해도 결국 도중에 중단되면 소용 없기 때문에 부적합.

C 탈락 -> API Gateway를 구성해 API를 호출해도 연결을 위한 것이지 결국 서버가 중단되면 소용 없기 때문에 부적합.

D 정답 -> SQS는 서로 다른 서비스 간에 메시지를 잠시 저장하는 용도로 쓰기 데이터를 캡처하여 트랜잭션이 완료될 때까지 메시지를 보관하기 때문에 장애가 발생해도 다시 시도하여 적합.

</div>
</details>

<hr/>

## Prob. 66 

프라이빗 서브넷에서 Amazon EC2 인스턴스는 애플리케이션을 실행하는 데 사용됩니다. 
애플리케이션은 Amazon DynamoDB의 테이블에 액세스해야 합니다.

트래픽이 AWS 네트워크를 나가는 것을 허용하지 않고 테이블에 액세스하는 가장 안전한 방법은 무엇입니까?

A. DynamoDB에 VPC 엔드포인트을 사용합니다.

B. 퍼블릭 서브넷에서 NAT 게이트웨이를 사용합니다.

C. 프라이빗 서브넷에서 NAT 인스턴스를 사용합니다.

D. VPC에 연결된 인터넷 게이트웨이를 사용합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

AWS 네트워크를 나가는 것을 허용하지 않음 문제 요점.

**NAT**
네트워크 주소 변환은 IP패킷에 있는 출발지 및 목적지의 IP주소와 TCP/UDP포트 숫자 등을 바꿔 재기록하면서 네트워크 트래픽을 주고 받게하는 기술.
중간 지점 역할로 위치 정보를 바꿔서 특정 IP를 모르게하여 보안성을 가지며 공인IP 하나로도 맥주소를 다르게 하여 여러 디바이스가 인터넷을 사용하게하는 기술.
ex) 공유기에 NAT 기능이 있어서 외부에서 공유기 내부에 있는 IP로 공격을 못함.

**VPC endpoint(AWS PrivateLink)**
VPC는 네트워크로 바로 접근을 막기 때문에 인터넷 게이트웨이로 퍼블릭 서브넷의 내부 리소스들에게 접근.
그중에 인터넷에서 프라이빗 서브넷을 접근하는 방법도 있는데 인터넷 게이트웨이 -> 퍼블릭 서브넷 -> NAT 게이트웨이 -> 프라이빗 서브넷순서로 변환하면서 접근.
endpoint는 프라이빗 서브넷에서 클라우드 외의 서비스(S3/DynamoDB 등)로는 인터넷 회선으로 나가야하는데 문제가 될 수 있으니 프라이빗 서브넷에서 해당 서비스와 직접 연결.

A 정답 -> 프라이빗 서브넷에서 VPC외부의 서비스 인스턴스에 접근할려면 인터넷 회선으로 나가게 되는데 이걸 막기 위해 endpoint라는 것으로 직접 연결하여 적합.

B 탈락 -> 퍼블릭 서브넷에서 NAT 게이트웨이를 사용하여 프라이빗 서브넷에 접근하는 것이지 반대로 나갈때는 인터넷 회선을 사용하여 부적합.

C 탈락 -> 서브넷에 NAT 인스턴스는 퍼블릭에만 한개 있는 것으로 부적합.

D 탈락 -> VPC가 인터넷과 연결하기 위해 사용하는 것이라 부적합.

</div>
</details>

<hr/>

## Prob. 67

단일 Amazon EC2 인스턴스에서 기업은 ASP.NET MVC 애플리케이션을 실행합니다.최근 애플리케이션 사용량이 급증했기 때문에 점심 시간에는 사용자의 응답 시간이 느려지고 있습니다.회사는 가능한 최소한의 설정을 사용하여 이 문제를 해결해야 합니다.

이러한 요구 사항을 충족하기 위해 솔루션 설계자는 어떤 권장 사항을 제시해야 합니까?

A. 애플리케이션을 AWS Elastic Beanstalk로 이동합니다. 점심 시간 동안 스케일링을 처리할 수 있도록 로드 기반 자동 스케일링 및 시간 기반 스케일링을 구성합니다.

B. 애플리케이션을 Amazon Elastic Container Service(Amazon ECS)로 이동합니다. 점심시간 동안 스케일링을 처리할 AWS Lambda 함수를 만듭니다.

C. 애플리케이션을 Amazon Elastic Container Service(Amazon ECS)로 이동합니다. 점심 시간 동안 AWS 애플리케이션 자동 스케일링에 대한 예약된 스케일링을 구성합니다.

D. 응용프로그램을 AWS Elastic Beanstalk로 이동합니다. 부하 기반 자동 스케일링을 구성하고 점심 시간 동안 스케일링을 처리할 AWS Lambda 함수를 만듭니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

사용량이 급증했기 때문에 점심 시간에는 사용자의 응답 시간이 느려짐을 최소한 설정 문제 요점.

로드 -> 용량
트래픽(부하) -> 처리 속도
시간 -> 스케줄링

**Elastic Beanstalk**
애플리케이션을 실행하는 인프라에 대해 자세히 알지 못해도 AWS 클라우드에서 애플리케이션을 신속하게 배포하고 관리.
선택 또는 제어에 대한 제한 없이 관리 복잡성을 줄일 수 있습니다. 애플리케이션을 업로드하기만 하면 Elastic Beanstalk에서 용량 프로비저닝, 로드 밸런싱, 조정, 애플리케이션 상태 모니터링에 대한 세부 정보를 자동으로 처리.

**Elastic Container Service(Amazon ECS)**
컨테이너화된 애플리케이션의 손쉬운 배포, 관리 및 크기 조정을 지원하는 완전관리형 컨테이너 오케스트레이션 서비스.
고도로 안전하고, 안정적이며, 확장 가능한 컨테이너 실행.
선호하는 지속적 통합 및 지속적 전달(CI/CD)과 자동화 도구를 사용하여 클라우드에서 수천 개의 컨테이너를 시작.
컨테이너에 맞게 AWS Fargate 서버리스 컴퓨팅을 최적화하여 제어 영역, 노드 및 인스턴스를 구성하고 관리할 필요가 없어짐.
자율 프로비저닝, 자동 크기 조정 및 종량제 요금을 통해 컴퓨팅 비용을 최대 50% 절감.
표준화된 AWS 관리 및 거버넌스 솔루션과 원활하게 통합.
하이브리드 환경에 배포/배치 처리 지원/웹 애플리케이션 크기 조정.

**데이터 거버넌스**
수집에서 사용, 폐기에 이르는 데이터 수명 주기 동안 데이터 관리에 사용되는 원칙적인 접근법.
데이터의 보안, 개인정보 보호, 정확성, 가용성, 사용성을 보장하기 위해 수행하는 모든 작업을 가리킵니다. 여기에는 사람이 취해야 하는 조치, 따라야 하는 프로세스, 데이터의 전체 수명 주기 동안 이를 지원하는 기술이 포함.

**비교**
- ECS는 여기서 최소한의 설정을 사용하는 대신, 예약된 확장으로 설정해야 합니다.
- Beanstalk vs. ECS - ECS로 이동하려면 Beanstalk(응용 프로그램 코드 업로드)보다 더 많은 구성/설정(작업 및 서비스 정의, ECS 컨테이너 에이전트 구성)이 필요합니다.
- Beanstalk는 Scheduled Scaling을 지원합니다.

A 정답 -> 설정을 덜해도 자동으로 해주는 Elastic Beanstalk이며 용량/시간 기반이라 적합.

B, C 탈락 -> 최소한의 설정을 사용하는 대신 예약된 확장하여 부적합.

D 탈락 -> 부하 기반 자동 스케일링과 굳이 람다가 안해도 되어 부적합.

</div>
</details>

<hr/>

## Prob. 68

기업이 온프레미스 애플리케이션을 AWS로 마이그레이션하는 과정에 있습니다. 프로그램 서버와 Microsoft SQL Server 데이터베이스가 응용 프로그램을 구성합니다. SQL Server 기능을 사용하는 응용 프로그램의 NET 코드로 인해 데이터베이스를 다른 엔진으로 전송할 수 없습니다. 회사의 목표는 운영 및 관리 비용을 줄이는 동시에 가용성을 극대화하는 것입니다. 

솔루션 설계자는 이를 달성하기 위해 어떤 조치를 취해야 합니까?

A. Multi-AZ 배포 환경의 Amazon EC2에 SQL Server를 설치합니다.

B. Multi-AZ 배포 환경에서 데이터를 Amazon RDS for SQL Server로 마이그레이션합니다.

C. Multi-AZ 복제본을 사용하여 Amazon RDS for SQL Server에 데이터베이스를 배포합니다.

D. 지역 간 Multi-AZ 배포 환경에서 데이터를 Amazon RDS for SQL Server로 마이그레이션합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

운영 및 관리 비용을 줄이는 동시에 가용성을 극대화 문제 요점.

온프레미스 -> AWS로 데이터 이동(마이그레이션)하는 과정.
프로그램 서버 - Microsoft SQL Server DB = 응용 프로그램(앱).
응용 프로그램의 NET 코드로 인해 데이터베이스를 다른 엔진으로 전송할 수 없음 = 구성 요소에서 처리되지 않은 예외가 발생.

cross region multi az란 서비스는 존재하지 않는다.
Multi-AZ 배포 환경은 가용성.
cross region multi az란 서비스는 존재하지 않는다.

A 탈락 -> Multi-AZ 배포로 가용성은 좋으나 EC2에 DB를 설치 및 관리하여 부적합.

B 정답 -> Multi-AZ 배포하고 데이터를 EBS기반의 RDS로 이동시키기 때문에 적합.

C 탈락 -> Multi-AZ 복제본으로 RDS를 배포한다는데 이전에 사용했던 데이터나 복제본이기 때문에 백업 목적인 것 같아 부적합.

D 탈락 -> 지역 간 Multi-AZ은 있는지 모르겠으나 해석한다면 서로 다른 리전에 복제하는 것 같은데 전세계에서 사용하는 것이면 처리 속도는 증가하나 한 지역에서의 가용성은 장담 못하여 부적합.

</div>
</details>

<hr/>

## Prob. 69

회사는 Amazon Redshift으로 분석을 수행하고 고객 보고서를 생성하는 데 사용됩니다. 
회사는 고객에 대한 추가 50TB의 인구 통계 데이터를 얻었습니다. 이 데이터는 Amazon S3안 in.csv 파일에 저장됩니다. 조직에는 데이터를 효율적으로 병합하고 결과를 시각화하는 시스템이 필요합니다.

솔루션 설계자는 이러한 요구 사항을 충족하기 위해 어떤 권장 사항을 제시해야 합니까?

A. Amazon Redshift Spectrum을 사용하여 Amazon S3의 데이터를 직접 쿼리하고 해당 데이터를 Amazon Redshift의 기존 데이터와 결합합니다. Amazon QuickSight를 사용하여 시각화를 구축합니다.

B. Amazon Athena를 사용하여 Amazon S3의 데이터를 쿼리합니다. Amazon QuickSight를 사용하여 Athena의 데이터를 Amazon Redshift의 기존 데이터와 결합하고 시각화를 구축합니다.

C. Amazon Redshift 클러스터의 크기를 늘리고 Amazon S3에서 데이터를 로드합니다. Amazon EMR 노트북을 사용하여 데이터를 쿼리하고 Amazon Redshift에서 시각화를 작성합니다.

D. Amazon Redshift 클러스터의 데이터를 Amazon S3의 Apache Parquet 파일로 내보냅니다. Amazon ES(Amazon ES)를 사용하여 데이터를 쿼리합니다. 키바나를 사용하여 결과를 시각화합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

데이터를 효율적으로 병합하고 결과를 시각화 문제 요점.

**Amazon Athena**
오픈소스 프레임워크에 구축된 서버리스 대화형 분석 서비스로 개방형 테이블과 파일 형식을 지원.
상주 위치에서 분석하는 간소화되고 유연한 방식을 제공.
S3 데이터 레이크 및 온프레미스나 SQL 또는 Python을 사용하는 기타 클라우드 시스템을 포함하는 데이터 소스로부터 데이터를 분석하거나 애플리케이션을 구축.
Apache Spark 프레임워크로 구축되었으며 프로비저닝이나 구성 작업이 필요 없음.
페타바이트 규모 데이터를 상주 위치에서 쉽고 유연하게 분석.
연동 쿼리 실행/ML 모델을 위한 데이터 준비/분산된 빅 데이터 보정 엔진 구축/Google Analytics 데이터 분석.

**Amazon QuickSight**
가장 인기 있는 클라우드 네이티브 서비리스 BI 서비스.
다음을 제공하는 데 사용할 수 있는 클라우드 규모의 비즈니스 인텔리전스(BI) 서비스.
QuickSight Q로 모두를 위한 BI 지원/ML 인사이트로 고급 분석 수행/애플리케이션 차별화를 위해 분석 기능 임베딩.

**Amazon EMR 노트북**
노트북과 Apache Spark를 실행하는 Amazon EMR 클러스터를 함께 사용하여 Amazon EMR 콘솔 내에서 Jupyter 노트북과 JupyterLab 인터페이스를 생성하고 열 수 있음.
쿼리와 코드를 실행하는 데 사용할 수 있는 “서버리스” 노트북.

**Amazon ES**
Apache Lucene에 구축되어 배포된 검색 및 분석 엔진.
로그 분석, 전체 텍스트 검색, 보안 인텔리전스, 비즈니스 분석 및 운영 인텔리전스 사용 사례에 일반적으로 사용.
방대한 양의 데이터를 신속하게, 거의 실시간( NRT, Near Real Time )으로 저장, 검색, 분석.

Elasticsearch는 검색을 위해 단독으로 사용되기도 하며, ELK( Elasticsearch / Logstatsh / Kibana )스택으로 사용.
* Logstash
  + 다양한 소스( DB, csv파일 등 )의 로그 또는 트랜잭션 데이터를 수집, 집계, 파싱하여 Elasticsearch로 전달
* Elasticsearch
  + Logstash로부터 받은 데이터를 검색 및 집계를 하여 필요한 관심 있는 정보를 획득
* Kibana
  + Elasticsearch의 빠른 검색을 통해 데이터를 시각화 및 모니터링

**Amazon Redshift**
SQL을 사용하여 여러 데이터 웨어하우스, 운영 데이터베이스 및 데이터 레이크에서 정형 데이터 및 반정형 데이터를 분석하고 AWS가 설계한 하드웨어 및 기계 학습을 사용해 어떤 규모에서든 최고의 가격 대비 성능을 지원.
클라우드 데이터 웨어하우징을 위한 최고의 가격 대비 성능.

데이터 이동이나 데이터 변환 없이 클릭 몇 번으로 모든 데이터에서 실시간 인사이트(통찰)와 예측 인사이트를 얻고 데이터 사일로를 없앨 수 있음.
재무 및 수요 예측 개선/협업 및 데이터 공유/비즈니스 인텔리전스 최적화/개발자 생산성 향상.

AWS Redshift Spectrum
  - Redshift와 함께 기본 제공 기능
  - AWS Redshift Spectrum과 EXTERNAL 명령을 사용하여 S3에 저장된 CSV 파일에 대해 SQL 쿼리를 실행할 수 있다. 즉, 데이터를 Amazon Redshift 테이블에 로드할 필요 없이 Amazon S3 파일의 데이터를 쿼리.
  - Amazon Redshift는 Amazon Redshift 클러스터와 Amazon S3 데이터 레이크 모두에 저장된 매우 큰 데이터 세트의 빠른 온라인 분석 처리(OLAP)를 위해 설계된 SQL 기능 제공

AWS Redshift 테이블에 있는 데이터를 분석.

**아파치 파켓**
Apache Parquet은 Apache Hadoop 에코시스템의 무료 오픈 소스 열 지향 데이터 저장 형식.

**Kibana**
Kibana는 ElasticSearch 데이터를 시각화하고 Elastic Stack을 탐색하게 해주는 무료 오픈 소스 인터페이스.
Kibana: 데이터 탐색, 시각화, 발견.

A 정답 -> 특별한 작업 없이 S3의 데이터에 직접 쿼리해서 기존과 결합하고 QuickSight로 데이터 시각화하여 적합.

B 탈락 -> 새로운 데이터를 Athena로 분석하고 그것을 QuickSight로 기존 데이터와 결합하고 시각화하는 것은 굳이 Athena를 사용하는 것은 비효율적이고 기존 데이터와 결합할 수 있는지 모르겠어 부적합.

C 탈락 -> 클러스터 크기를 늘려 분석하여 결합할 필요 없지만 데이터 시각화는 부적합.

D 탈락 -> Redshift 클러스터에서 S3로 보내서 Redshift대신 S3의 파일을 ElasticSearch로 분석하고 전용 Kibana로 데이터 시각화하여 부적합.

</div>
</details>

<br>
<hr/>
<hr/>

## Prob. 70

매달 기업은 Amazon S3에 200GB의 데이터를 보관합니다. 매월 말에 회사는 이 데이터를 분석하여 전월 동안 각 판매 영역에서 판매된 물건 수를 계산해야 합니다.

비즈니스에 가장 비용 효율적인 옵션은 어떤 분석 접근 방식입니까?

A. Amazon ES(Amazon Elastic Search Service) 클러스터를 생성합니다. Amazon ES의 데이터를 쿼리합니다. 키바나를 사용하여 데이터를 시각화합니다.

B. AWS Glue 데이터 카탈로그에서 테이블을 생성합니다. Amazon Athena를 사용하여 Amazon S3의 데이터를 쿼리합니다. Amazon QuickSight에서 데이터를 시각화합니다.

C. Amazon EMR 클러스터를 생성합니다. Amazon EMR을 사용하여 데이터를 쿼리하고 결과를 Amazon S3에 저장합니다. Amazon QuickSight에서 데이터를 시각화합니다.

D. Amazon Redshift 클러스터를 만듭니다. Amazon Redshift에 있는 데이터를 조회하고 결과를 Amazon S3에 업로드합니다. Amazon QuickSight에서 데이터를 시각화합니다.

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

**AWS Glue**
AWS Glue는 Amazon Web Services의 일부로 Amazon에서 제공하는 이벤트 기반 서버리스 컴퓨팅 플랫폼입니다. 이벤트에 대한 응답으로 코드를 실행하고 해당 코드에 필요한 컴퓨팅 리소스를 자동으로 관리하는 컴퓨팅 서비스.

EMR 및 Redshfit은 Athena보다 높은 컴퓨팅 수준에서 작동합니다.
S3 → Glue → Athena → QuickSight.

A 탈락 -> 실시간 검색 및 분석 엔진으로 데이터 쿼리가 아닌 데이터 시각화를 위한 것이고 서버리스가 아니라 비용도 좋지 않아 부적합.
아마도 속도면에서 좋지 않을까? 생각.

B 정답 -> Athena가 데이터 병합은 완벽하지 않으나 서버리스 대화식이라 비용적으로는 효율적이라 적합.

C, D 탈락 -> 데이터를 분석하고 결과를 S3에 저장할 필요 없고 둘다  Athena보다 높은 컴퓨팅 수준에서 작동하여 부적합.

</div>
</details>

<hr/>

* Ref
  - [ExamTopics](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate-saa-c02/view/7)