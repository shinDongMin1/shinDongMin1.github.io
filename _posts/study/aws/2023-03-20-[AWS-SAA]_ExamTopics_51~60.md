---
layout: post
title: "[AWS-SAA] Examtopics 51~60"
subtitle: AWS
date: '2023-03-20 00:00:01 +0900'
category: study
tags: aws aws-saa
image:
  path: /assets/img/study_AWS/saa-co2_logo.png
---

SAA Examtopics 51~60번 문제를 풀어보자.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## Prob. 51

거대한 Amazon EC2 인스턴스 집합에서 기업은 애플리케이션을 실행합니다. 이 프로그램은 Amazon에서 호스팅하는 DynamoDB 데이터베이스에 항목을 읽고 씁니다. DynamoDB 데이터베이스의 크기는 정기적으로 증가하지만 애플리케이션에는 이전 30일 동안의 데이터만 필요합니다. 조직은 구현하기에 비용 효율적이고 시간 효율적인 솔루션이 필요합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. AWS CloudFormation 템플릿을 사용하여 전체 솔루션을 구축합니다. CloudFormation 스택을 30일마다 다시 배포하고 원래 스택을 삭제합니다.

B. AWS Marketplace에서 모니터링 응용 프로그램을 실행하는 EC2 인스턴스를 사용합니다. 테이블에 새 항목이 생성될 때 Amazon DynamoDB Streams를 사용하여 타임스탬프를 저장하도록 모니터링 응용 프로그램을 구성합니다. EC2 인스턴스에서 실행되는 스크립트를 사용하여 타임스탬프가 30일보다 오래된 항목을 삭제합니다.

C. 테이블에 새 항목이 생성될 때 AWS Lambda 함수를 호출하도록 Amazon DynamoDB Streams를 구성합니다. 30일이 지난 테이블의 항목을 삭제하도록 람다 기능을 구성합니다.

D. 응용 프로그램을 확장하여 현재 타임스탬프 값에 테이블에 생성되는 각 새 항목에 30일을 더한 속성을 추가합니다. 속성을 TTL 속성으로 사용하도록 DynamoDB를 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

이전 30일 동안의 데이터만 필요하여 비용 효율적이고 시간 효율적인 솔루션 문제 요점.

**AWS CloudFormation 템플릿** <BR>
AWS에서의 프로비저닝 및 관리를 단순화합니다. 원하는 서비스 또는 애플리케이션 아키텍처에 대한 템플릿을 생성하고 AWS CloudFormation이 그러한 템플릿을 사용하여 해당 서비스 또는 애플리케이션에 대한 신속하고 안정적인 프로비저닝을 수행하도록 할 수 있습니다(이를 "스택"이라고 함). 필요한 만큼 스택을 쉽게 업데이트하거나 복제 가능.

샘플 템플릿 모음은 AWS CloudFormation을 시작하고 자체 템플릿을 신속하게 구축하는 데 도움.

스택(아키텍처에 대한 템플릿) 리소스를 프로비저닝 및 구성하려면 JSON 또는 YAML 형식 텍스트 파일인 AWS CloudFormation 템플릿을 이해하고 있어야 함.

이 템플릿은 AWS CloudFormation 스택에서 프로비저닝할 리소스에 대해 설명합니다. AWS CloudFormation Designer 또는 텍스트 편집기를 사용하여 템플릿을 생성한 후 저장. <BR>
JSON 또는 YAML에 익숙하지 않은 경우 AWS CloudFormation Designer를 사용하면 AWS CloudFormation 템플릿을 시작하는 데 도움되게 템플릿을 시각적으로 생성하고 수정하기 위한 도구.

템플릿 코드 조각에서는 특정 리소스에 대한 템플릿을 쓰는 방법을 보여주는 예제를 제공. <BR>
예를 들어, Amazon EC2 인스턴스, Amazon S3 도메인, AWS CloudFormation 매핑 등에 대한 코드 조각.

**AWS Marketplace** <BR>
AWS Marketplace는 빌더부터 조달 책임자에 이르기까지 다양한 사용자의 요구 사항에 맞게 맞춤화된 기능을 제공. <BR>
서드 파티 소프트웨어, 서비스 및 데이터의 조달, 프로비저닝 및 거버넌스를 간소화. <BR>
간소화된 조달 및 제어 기능을 통해 원하는 서드 파티 소프트웨어를 쉽게 검색, 테스트, 구매 및 배포할 수 있도록 큐레이팅된 디지털 카탈로그.

클릭 몇 번이면 미리 구성된 소프트웨어를 빠르게 시작하고 Amazon Machine Image(AMI) 및 서비스형 소프트웨어(SaaS) 형식과 다른 형식의 소프트웨어 솔루션을 선택할 수 있습니다. 또한 데이터 제품을 찾아보고 구독. <BR>
무료 평가판, 시간당, 월별, 연간, 다년 및 기존 보유 라이선스 사용(BYOL) 모델과 같은 유연한 요금 옵션 중에서 선택.

맞춤형 약관, 볼륨 요금 및 유연한 지불 옵션을 사용하여 소프트웨어 조달. <BR>
표준화된 라이선스 약관을 통해 조직은 장기간이 소요되는 협상을 줄임. <BR>
소프트웨어 구매를 간소화하고, 비즈니스를 위한 혁신을 가속화. <BR>
Professional Services를 사용하면 소프트웨어 배포 및 관리에 도움이 되는 프리미엄 지원, 관리형 서비스, 평가, 교육 및 기타 서비스.

관리형 권한 부여는 고객이 AWS License Manager를 통해 AWS Marketplace에서 획득한 소프트웨어 라이선스 권한을 배포하고 활성화하고 추적할 수 있도록 하는 기능. <BR>
Private Marketplace는 AWS Marketplace에서 구매할 수 있는 승인된 소프트웨어 및 데이터 제품의 맞춤형 디지털 카탈로그를 제공. <BR>
범주화, 할당 및 성능 비용 보고에 비용 할당 태깅을 사용.

Independent Software Vendor(ISV), 데이터 공급자 및 컨설팅 파트너가 수백만 AWS 고객에게 AWS Marketplace의 소프트웨어, 서비스 및 데이터를 판매.

**DynamoDB Streams** <BR>
DynamoDB Streams는 DynamoDB 테이블에서 시간 순서에 따라 항목 수준 수정을 캡처하고 이 정보를 최대 24시간 동안 로그에 저장. <BR>
로그와 데이터 항목은 변경 전후 거의 실시간으로 나타나므로 애플리케이션에서 이러한 로그와 데이터에 액세스.

유휴 시 암호화는 DynamoDB Streams의 데이터를 암호화.

테이블에서 스트림을 활성화하면 DynamoDB가 테이블 데이터 항목의 모든 수정에 대한 정보를 캡처.

**Amazon DynamoDB** <BR>
TTL(Amazon DynamoDB Time to Live)을 사용하면 항목별 타임스탬프를 정의하여 항목이 더 이상 필요하지 않은 시기를 결정할 수 있습니다. <BR>
지정한 타임스탬프의 날짜 및 시간이 지나면 DynamoDB는 쓰기 처리량을 사용하지 않고 테이블에서 항목을 삭제합니다. TTL은 워크로드 요구사항에 맞게 최신 상태로 유지되는 항목만 유지하여 저장된 데이터 볼륨을 줄이기 위한 수단으로 추가 비용 없이 제공됩니다.

TTL은 특정 시간 후에 관련성이 손실된 항목을 저장할 때 유용합니다. 다음은 TTL 사용 사례의 예입니다.

응용 프로그램에서 1년 동안 사용하지 않은 사용자 또는 센서 데이터를 제거합니다.

만료된 항목을 Amazon DynamoDB Streams 및 AWS Lambda를 통해 Amazon S3 데이터 레이크에 아카이브합니다.

계약 또는 규제 의무에 따라 중요한 데이터를 일정 기간 동안 보관합니다.<BR>
[링크](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/TTL.html)https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/TTL.html

![1](/assets/img/study_AWS/[SAA]_ExamTopics_51~60/1.PNG)

A 탈락 -> AWS CloudFormation 템플릿으로 아키텍처를 구축하는데 사용되는데 데이터에 대한 30일 제한이 아니라 부적합.

B 탈락 -> AWS Marketplace은 AWS에 대한 요구사항에 맞는 기술을 판매하는 곳으로 이미 시스템이 구축된 곳에서 사용하기에 부적합.

C 탈락 -> 보통 Amazon DynamoDB Streams를 호출하여 AWS Lambda 함수를 구성하며 Streams은 데이터 보존에 대한 로그를 24시간 저장하는 기술로 부적합.

D 정답 -> 비용은 들지 않으며 시간도 적게 사용하는 DynamoDB의 TTL기능을 사용하면 적합.

</div>
</details>

<hr/>

## Prob. 52

이전에는 기업에서 데이터 웨어하우징 솔루션을 AWS로 이전했습니다. 또한 회사에는 AWS Direct Connect 연결이 있습니다. 회사 사무실의 사용자는 시각화 도구를 사용하여 데이터 웨어하우스를 쿼리할 수 있습니다. 데이터 웨어하우스에서 응답하는 각 쿼리의 크기는 평균 50MB인 반면 시각화 도구에서 제공하는 각 웹 페이지의 크기는 약 500KB입니다. 데이터 웨어하우스는 반환하는 결과 집합을 캐시하지 않습니다.

회사의 가장 낮은 발신 데이터 전송 비용을 초래하는 접근 방식은 무엇입니까?

A. 사내에서 시각화 도구를 호스팅하고 인터넷을 통해 직접 데이터 웨어하우스를 쿼리합니다.

B. 시각화 도구를 데이터 웨어하우스와 동일한 AWS 영역에 호스팅합니다. 인터넷을 통해 접속합니다.

C. 사내에서 시각화 도구를 호스팅하고 동일한 AWS 영역에 있는 Direct Connect 연결을 통해 직접 데이터 웨어하우스를 쿼리합니다.

D. 시각화 도구를 데이터 웨어하우스와 동일한 AWS 영역에 호스팅하고 동일한 영역의 위치에 있는 DirectConnect 연결을 통해 액세스합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

가장 낮은 발신 데이터 전송 비용 문제 요점.

**데이터 웨어하우스** <BR>
데이터 웨어하우스는 POS 트랜잭션, 마케팅 자동화, 고객 관계 관리 시스템 등의 여러 소스에서 가져온 구조화된 데이터와 반구조화된 데이터를 분석하고 보고하는 데 사용되는 엔터프라이즈 시스템입니다. 데이터 웨어하우스는 임시 분석과 커스텀 보고서 생성에 적합.

시각적 도구(온-프레미스) --(Direct Connect, 쿼리)--> 데이터 웨어하우스(AWS)

**Direct Connect** <BR>
[링크](https://aws.amazon.com/directconnect/pricing/)https://aws.amazon.com/directconnect/pricing/ <br>
[링크](https://aws.amazon.com/blogs/aws/aws-data-transfer-prices-reduced/)https://aws.amazon.com/blogs/aws/aws-data-transfer-prices-reduced/

"Direct Connect를 통한 데이터 전송 가격이 인터넷을 통한 데이터 전송 가격보다 낮습니다."

AWS에서 사내로 전송하는 것이 AWS에서 AWS로 전송하는 것보다 비용이 더 많이 들기 때문에 C보다 D를 사용할 것입니다.

AWS Direct Connect
![2](/assets/img/study_AWS/[SAA]_ExamTopics_51~60/2.PNG)
![3](/assets/img/study_AWS/[SAA]_ExamTopics_51~60/3.PNG)

AWS Direct Connect + AWS Transit Gateway
![4](/assets/img/study_AWS/[SAA]_ExamTopics_51~60/4.PNG)

AWS Direct Connect + VPN
![5](/assets/img/study_AWS/[SAA]_ExamTopics_51~60/5.PNG)

A, B 탈락 -> 시각화 도구가 사내/AWS에 있던 인터넷으로 데이터 전송을 하면 더 비싸서 부적합.

C 탈락 -> 지금 아키텍처 그대로 사용하는 것인데 AWS에서 사내로 데이터 전송을 하는 것은 부적합.

D 정답 -> 시각화 도구를 AWS로 옮기는 것인데 AWS에서 AWS로 전송하는 것이 비용적으로 적게 들기 때문에 적합.

</div>
</details>

<hr/>

## Prob. 53

비즈니스에서 많은 마이크로서비스로 구성된 애플리케이션을 개발 중입니다. 조직은 컨테이너 기술을 통해 AWS에 소프트웨어를 배포하기로 결정했습니다. 비즈니스에는 유지 관리 및 성장을 위해 지속적인 작업이 거의 필요하지 않은 솔루션이 필요합니다. 추가 인프라는 비즈니스에서 관리할 수 없습니다.

이러한 요구 사항을 충족하기 위해 솔루션 설계자는 어떤 단계를 함께 수행해야 합니까? (2개를 선택하세요.)

A. Amazon ECS(Elastic Container Service) 클러스터를 배포합니다.

B. 여러 가용성 영역에 걸쳐 있는 Amazon EC2 인스턴스에 Kubernetes 컨트롤 플레인을 배포합니다.

C. Amazon EC2 시작 유형이 있는 Amazon ECS(Amazon Elastic Container Service) 서비스를 배포합니다. 2보다 크거나 같은 작업 번호 수준을 지정합니다.

D. Fargate 시작 유형이 있는 Amazon ECS(Elastic Container Service) 서비스를 배포합니다. 2보다 크거나 같은 작업 번호 수준을 지정합니다.

E. 여러 가용성 영역에 걸쳐 있는 Amazon EC2 인스턴스에 Kubernetes 작업자 노드를 배포합니다. 각 마이크로 서비스에 대해 둘 이상의 복제본을 지정하는 배포를 만듭니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A, D

해설 : 

마이크로서비스와 지속적인 작업이 거의 필요하지 않은 솔루션이 필요 문제 요점.

A와 D여야 합니다. <br>
이 질문은 인프라 관리가 옵션이 되어서는 안 된다는 것을 반복적으로 언급하고 있으므로 EC2는 주제에서 벗어나 있습니다. <br>
또한 마이크로 서비스를 통해 사용자가 문제 없이 패러게이트할 수 있습니다.

[링크](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/deploy-java-microservices-on-amazon-ecs-using-aws-fargate.html)https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/deploy-java-microservices-on-amazon-ecs-using-aws-fargate.html

관리형 : EC2<br>
완전 관리형 : RDS, DynamoDB, ElastiCache, Redshift, SNS

**Amazon ECS 클러스터** <br>
Amazon ECS 클러스터는 작업과 서비스를 그룹화하고 공유 용량과 공통 구성을 허용. <br>
Amazon ECS 클러스터는 태스크 또는 서비스의 논리적 그룹입니다. 태스크와 서비스는 클러스터에 등록된 인프라에서 실행됩니다. 인프라 용량은 AWS Fargate에서 제공. <br>
AWS가 관리하는 서버리스 인프라나 스스로 관리하는 Amazon EC2 인스턴스, 온프레미스 서버 또는 원격으로 관리하는 가상 머신(VM)입니다. 대부분의 경우 Amazon ECS 용량 공급자는 클러스터의 태스크가 사용하는 인프라를 관리하는 데 사용할 수 있음.

클러스터는 AWS 리전별로 고유합니다. <br>
클러스터는 다음 상태 중 하나일 수 있습니다. (ACTIVE/PROVISIONING/DEPROVISIONING/FAILED/INACTIVE)

작업은 시작 유형 또는 용량 공급자 전략으로 클러스터는 AWS Fargate, Amazon EC2 인스턴스 또는 외부 인스턴스에서 호스팅되는 작업이 섞여 있을 수 있음. <br>
(Amazon EC2 Auto Scaling 그룹의 용량을 추적하거나 조정하지 않음) <br>
클러스터에 오토 스케일링 용량 공급자와 Fargate 용량 공급자가 혼합되어 있을 수 있습니다. 그러나 용량 공급자 전략을 지정할 때는 둘 중 하나만 포함. <br>
사용자 지정 IAM 정책을 생성하여 특정 클러스터에 대한 사용자 액세스를 허용하거나 제한. <br>
EC2 시작 유형이나 오토 스케일링 그룹 용량 공급자를 사용하는 작업의 경우 클러스터에는 서로 다른 여러 컨테이너 인스턴스 유형이 포함될 수 있습니다. 그러나 각 컨테이너 인스턴스는 한 번에 하나의 클러스터에만 등록. <br>
클러스터에 대한 기본 Service Connect 네임스페이스를 구성할 수 있습니다. 기본 Service Connect 네임스페이스를 설정한 후 Service Connect를 켜서 네임스페이스의 클라이언트 서비스로 클러스터에 생성된 모든 새 서비스를 추가.

**Kubernetes** <br>
Kubernetes는 대규모 컨테이너식 애플리케이션을 배포하고 관리하는 데 사용할 수 있는 오픈 소스 소프트웨어. <br>
Amazon Elastic Compute Cloud(EC2) 컴퓨팅 인스턴스의 클러스터를 관리하고 배포, 유지 관리 및 크기 조정의 프로세스를 통해 이러한 인스턴스에서 컨테이너를 실행. <br>
Kubernetes를 사용하면 온프레미스와 클라우드에서 같은 도구 세트를 사용하여 원하는 유형의 컨테이너식 애플리케이션을 실행할 수 있음. <br>
AWS에서는 확장 가능한 고가용성 가상 머신 인프라, 커뮤니티 기반 서비스 통합 및 Amazon Elastic Kubernetes Service(EKS)(Kubernetes 공인 관리형 서비스)를 통해 클라우드에서 손쉽게 Kubernetes를 실행 가능.

Kubernetes는 컴퓨팅 인스턴스 클러스터를 관리하고 가용 컴퓨팅 리소스와 각 컨테이너의 리소스 요구 사항을 기반으로 클러스터에서 실행되도록 컨테이너를 예약하는 방식으로 작동합니다. <br>컨테이너는 팟이라는 논리적 그룹으로 실행되며 하나 또는 여러 컨테이너를 팟으로 함께 실행하고 규모를 조정. <br>
`Kubernetes 컨트롤 플레인` 소프트웨어가 언제 어디에서 팟을 실행할지 결정하고, 트래픽 라우팅을 관리하고, 사용률 또는 사용자가 정의한 다른 지표를 기반으로 팟의 규모를 조정. <br>
인스턴스에 장애가 발생하면 팟을 자동으로 다시 시작. <br>
각 팟에는 IP 주소와 하나의 DNS 이름이 주어지며 Kubernetes는 이를 사용하여 서비스를 서로 연결하고 외부 트래픽과 연결.

Kubernetes 배포를 완전 관리. 강력한 인스턴스 유형을 선택하여 Kubernetes를 프로비저닝 및 실행. -> Amazon EC2 <br>
마스터 인스턴스 및 etcd를 프로비저닝하거나 관리할 필요 없이 Kubernetes를 실행. -> Amazon EKS <br>
빠른 배포를 위해 컨테이너 이미지를 저장, 암호화 및 관리. -> Amazon ECR

클러스터에 `작업자 노드` 및 구역 추가로 앱의 가용성을 높이기 위해 클러스터의 한 기존 구역 또는 다수의 기존 구역에 작업자 노드를 추가할 수 있습니다. 구역 장애로부터 앱을 보호하는 데 도움이 되도록 클러스터에 구역을 추가 가능. <br>
클러스터를 작성하면 작업자 노드가 작업자 풀에서 프로비저닝됨. <br>
풀에 작업자 노드를 더 추가할 수 있고 기본적으로 작업자 풀은 하나의 구역에 존재. -> 단일 구역 클러스터(single zone cluster) <br>
클러스터에 구역을 더 추가하면 작업자 풀이 구역 간에 존재 -> 다중 구역 클러스터(multizone cluster)

Amazon Elastic Kubernetes Service(EKS) 클러스터의 관리형 작업자 노드를 프로비저닝하고, Amazon EKS 관리 콘솔, API 또는 CLI를 사용하여 노드를 최신 상태로 유지 가능. <br>
Amazon EKS 관리형 노드 그룹을 사용하면 컴퓨팅 용량을 제공하는 EC2 인스턴스를 별도로 프로비저닝하거나 연결할 필요가 없음. <br>
AWS 계정에서 EKS에 최적화. <br>
가용성을 유지하기 위해 노드가 정상적으로 드레이닝.

**Fargate** <br>
서버를 관리하지 않고도 애플리케이션 구축에 초점을 맞출 수 있도록 지원하는 종량제 컨테이너에 적합한 서버리스 컴퓨팅 엔진, 마이크로서비스. <br>
AWS Fargate는 ECS 및 EKS 모두와 호환.

인프라가 아닌 애플리케이션 배포 및 관리 Fargate는 서버 크기 조정, 패치, 보안 및 관리의 운영 부담을 없애줌.

A 정답 -> 일단 컨테이너 기술을 통해 배포하기로 했기에 ECS 클러스터부터 먼저 배포하는 것이 적합.

B 탈락 -> EC2에 언제 어디에서 팟을 실행할지 결정하고 트래픽 라우팅을 관리하는 소프트웨어를 배포해도 EC2기반이라서 관리가 필요해서 부적합.

C 탈락 -> ECS를 사용하나 EC2기반이라서 부적합.

D 정답 -> 마이크로서비스에 편리한 Fargate로 배포하여 적합.

E 탈락 -> EC2에 가용성과 장애에서 보호하는 작업자 풀을 배포해도 EC2기반이라서 관리가 필요해서 부적합.

</div>
</details>

<hr/>

## Prob. 54

다음 정책은 Amazon EC2 관리자에 의해 개발되었으며 여러 사용자를 포함하는 IAM 그룹에 할당되었습니다.

![prob_54](/assets/img/study_AWS/[SAA]_ExamTopics_51~60/prob_54.png)

이 정책은 어떤 영향을 미칩니까?

A. 사용자는 us-east-1을 제외한 모든 AWS 영역에서 EC2 인스턴스를 종료할 수 있습니다.

B. 사용자는 us-east-1 영역에서 IP 주소가 10.100.100.1인 EC2 인스턴스를 종료할 수 있습니다.

C. 사용자의 원본 IP가 10.100.100.254일 때 사용자는 us-east-1 영역에서 EC2 인스턴스를 종료할 수 있습니다.

D. 사용자의 원본 IP가 10.100.100.254인 경우 사용자는 us-east-1 영역에서 EC2 인스턴스를 종료할 수 없습니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

![6](/assets/img/study_AWS/[SAA]_ExamTopics_51~60/6.PNG)

ex) <br>
"Action": "ec2:*" -> ec2의 모든 기능에 대해서 <br>
"Action": "ec2:StartInstances" -> ec2에서 인스턴스 시작만 된다. <br>
"NotAction": "s3:DeleteBucket" -> s3에서 DeleteBucket(버켓 삭제)를 제외하고

"Effect": "allow" <br>
\* = All resources <br>
"Action": "ec2:TerminateInstances" = ec2:TerminateInstances기능만 <br>
"Condition": "aws:SourceIP": "10.100.100.0/24" = If 주소가 10.100.100.0/24 네트워크면

사용자는 모든 리소스에 대한 EC2 종료 작업 허용. 만약 주소가 10.100.100.0/24이라면

"Effect": "Deny" <br>
\* = All resources <br>
"Action": "ec2:*" = ec2의 모든 기능 <br>
"Condition": "ec2:Region": "us-east-1" = If ec2지역이 us-east-1 이 아니라면

사용자는 모든 리소스에 대한 EC2 모든 기능의 작업을 제외하고 거부. 만약 EC2 지역이 us-east-1이라면

10.100.100.1은 예약된 IP 주소(0~4)이다.

0 : 네트워크 어드레스<br>
1 : VPC Router<br>
2 : DNS<br>
3 : Future use<br>
4 : Broadcast<br>

즉, us-east-1 지역에서 주소가 10.100.100.0/24 네트워크 대역이라면 종료 가능.

A 탈락 -> us-east-1를 제외한 지역에서는 EC2의 모든 작업이 불가능하여 부적합.

B 탈락 -> us-east-1 지역에서 EC2의 모든 작업이 가능해지는데 10.100.100.1는 라우터 디바이스라서  부적합.

C 정답 -> 10.100.100.254이며 us-east-1 지역이라서 적합.

D 탈락 -> 이것은 두 조건 다 만족하지만 작업을 할 수 없다고하여 부적합.

</div>
</details>

<hr/>

## Prob. 55

비즈니스의 웹 애플리케이션은 데이터를 Amazon RDS PostgreSQL 데이터베이스 인스턴스에 저장합니다. 회계사는 결산 기간 중 매월 초에 대량 쿼리를 수행하며 과도한 활용으로 인해 데이터베이스 성능에 부정적인 영향을 미칩니다. 비즈니스는 온라인 지원에 대한 보고의 영향을 줄이기를 원합니다.

가능한 한 최소한의 작업으로 데이터베이스의 영향을 최소화하기 위해 솔루션 설계자는 무엇을 해야 합니까?

A. 읽기 복제본을 작성하고 복제본에 직접 트래픽을 보고합니다.

B. Multi-AZ 데이터베이스를 만들고 트래픽을 대기 상태로 전송합니다.

C. 교차 영역 읽기 복제본을 작성하고 복제본에 직접 트래픽을 보고합니다.

D. Amazon Redshift 데이터베이스를 생성하고 트래픽을 Amazon Redshift 데이터베이스로 직접 보고합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

매월 초에 대량 쿼리를 수행하여 트래픽 문제 요점.

**읽기 복제본** <br>
RDS/Aurora 읽기 복제본 인스턴스는 업스트림에 위치한 기본("마스터") 데이터베이스 인스턴스의 비동기식 읽기 전용 복제본입니다. <br>
응용 프로그램에서 데이터를 변경할 필요가 없는 쿼리에 사용할 수 있으므로 마스터의 부하를 줄일 수 있습니다.

**교차 영역 읽기 복제본** <br>
교차 영역 읽기 복제본은 원본 인스턴스에서 작성된 실제 복제 슬롯을 사용합니다. 복제 슬롯은 WAL 파일을 보존하기 때문에 교차 영역 복제 지연은 원본 인스턴스에 WAL이 많이 축적되고 결국 스토리지 부족과 같은 심각한 문제를 야기할 수 있음. <br>
그리고 다른 리전에 읽기 복제본을 만드는 것이라서 같은 지역의 트래픽은 동일함.

**Amazon Redshift** <br>
클라우드 데이터 웨어하우징을 위한 최고의 가격 대비 성능. <br>
SQL을 사용하여 여러 데이터 웨어하우스, 운영 데이터베이스 및 데이터 레이크에서 정형 데이터 및 반정형 데이터를 분석하고 AWS가 설계한 하드웨어 및 기계 학습을 사용해 어떤 규모에서든 최고의 가격 대비 성능을 지원. <br>
데이터 이동이나 데이터 변환 없이 클릭 몇 번으로 모든 데이터에서 실시간 인사이트(통찰)와 예측 인사이트(통찰)를 얻고 데이터 사일로를 없앨 수 있음. <br>
재무 및 수요 예측 개선/협업 및 데이터 공유/비즈니스 인텔리전스 최적화/개발자 생산성 향상.

A 정답 -> 읽기 복제본으로 트래픽을 나눠서 처리하기 때문에 부하를 줄일 수 있어 적합.

B 탈락 -> Multi-AZ은 장애시 가용성을 위한 복제본으로 마스터가 계승될 때 사용하여 부적합.

C 탈락 -> 읽기 복제본은 같은 지역의 다른 가용 영역에 트래픽을 나눠야하는데 교차 영역은 다른 지역으로 복제를 하는 것이라서 부적합.

D 탈락 -> Amazon Redshift는 데이터 웨어하우징 기술로 DB의 데이터를 분석하는 것이라 부적합.

</div>
</details>

<br>
<hr/>
<hr/>

## Prob. 56 유념

한 기업이 Amazon RDS에 MySQL 데이터베이스를 구현했습니다. 데이터베이스 지원팀은 트랜잭션 증가로 인해 DB 인스턴스에 대한 읽기 지연이 발생했다고 보고하고 읽기 전용 복제본을 설치할 것을 권고하고 있습니다.

솔루션 설계자는 이 변경 사항을 배포하기 전에 어떤 활동을 수행해야 합니까? (2개를 선택하세요.)

A. RDS primary 노드에서 binlog 복제를 사용하도록 설정합니다.

B. 원본 DB 인스턴스에 대한 장애 조치 우선 순위를 선택합니다.

C. 원본 DB 인스턴스에서 장시간 실행되는 트랜잭션을 완료할 수 있게 허가합니다.

D. 글로벌 테이블을 만들고 테이블을 사용할 AWS 영역을 지정합니다.

E. 백업 보존 기간을 0이 아닌 값으로 설정하여 원본 인스턴스에서 자동 백업을 실행하십시오.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C, E

해설 : 

읽기 전용 복제본을 설치할 것을 권고 문제 요점.

"활성화된 장기간 실행되는 트랜잭션은 읽기 복제본 작성 프로세스를 지연시킬 수 있습니다. 읽기 복제본을 만들기 전에 장기간 실행 중인 트랜잭션이 완료될 때까지 기다리는 것이 좋습니다. 동일한 원본 DB 인스턴스에서 여러 개의 읽기 복제본을 병렬로 작성하는 경우 Amazon RDS는 첫 번째 작성 작업을 시작할 때 스냅샷을 하나만 작성합니다.

글로벌 테이블은 글로벌 규모의 Amazon DynamoDB를 기반으로 구축되어 완전관리형, 다중 리전, 다중 활성 데이터베이스를 제공하며, 이 데이터베이스는 대규모로 확장되는 글로벌 애플리케이션에 대해 빠른 로컬 읽기 및 쓰기 성능을 지원합니다. 글로벌 테이블은 선택한 AWS 리전에서 DynamoDB 테이블을 자동으로 복제.

읽기 복제본을 작성할 때 고려해야 할 몇 가지 사항이 있습니다. 먼저 백업 보존 기간을 0이 아닌 값으로 설정하여 원본 DB 인스턴스에서 자동 백업을 실행해야 합니다. 이 요구사항은 다른 읽기 복제본의 원본 DB 인스턴스인 읽기 복제본에도 적용됩니다." <br>
[링크](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html)https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html

A 탈락 -> RDS primary(원본) 노드에서 binlog 복제하는데 데이터 변경사항들에 대한 정보를 포함하는 로그 파일의 세트이지 읽기 지연을 해결하는게 아니라 부적합. <br>
(에러코드, 바이너리 로그 자체에 대한 메타데이터 등 다양한 데이터가 같이 포함)

B 탈락 -> A와 같이 장애에 대한 조치에 사항이라 부적합.

C 정답 -> 복제본을 만들기 전에 스냅샷을 생성하기 위해 모든 작업이 완료 되어야해서 적합.

D 탈락 -> 글로벌 테이블/글로벌 보조 인덱스/로컬 보조 인덱스는 DynamoDB에 대한 기능으로 전 지역/로컬에 대한 쿼리 성능은 높여주지만 읽기 복제가 아니라 트래픽은 여전히 한 곳에 집중되어 부적합.

E 정답 -> 백업 보존 기간을 늘려 자동 백업하게 만들어야 읽기 복제본을 업데이트하고 장애에도 도움이 되어 적합.

</div>
</details>

<hr/>

## Prob. 57

사용자는 회사 웹사이트에서 과거 실적 보고서를 받을 수 있습니다. 웹 사이트에는 회사의 전세계 웹 사이트 요구 사항에 맞게 확장할 수 있는 솔루션이 필요합니다. 솔루션은 비용 효율적이고 인프라 리소스 프로비저닝을 최소화하며 실현 가능한 가장 빠른 반응 시간을 제공해야 합니다.

솔루션 설계자는 이러한 요구 사항을 충족하기 위해 어떤 기술 조합을 제안할 수 있습니까?

A. Amazon CloudFront and Amazon S3

B. AWS Lambda and Amazon DynamoDB

C. Application Load Balancer with Amazon EC2 Auto Scaling

D. Amazon Route 53 with internal Application Load Balancers

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

전세계 웹 사이트 요구 사항에 맞게 확장하고 비용 효율적이고 프로비저닝을 최소화(캐시 사용-엣지 로케이션)하며 실현 가능한 가장 빠른 반응 시간을 제공 문제 요점.

A 정답 -> CloundFront와 S3의 조합으로 정적 컨텐츠 S3로 서버리스로 처리하여 비용 효율적이며 엣지 로케이션으로 프로비저닝 최소화 및 빠른 반응 시간을 제공하여 적합.

B 탈락 -> AWS Lambda함수와 Amazon DynamoDB는 관련 없어 부적합.

C 탈락 -> ALB와 함께 EC2 오토 스케일링하여 조건에 최적으로 만족하지 않아 부적합.

D 탈락 -> 국내에 대한 ALB으로 트래픽 분산과 함께 Amazon Route 53 도메인 서비스를 사용한다고 관련 없어 부적합.

</div>
</details>

<hr/>

## Prob. 58

솔루션 설계자는 Amazon Web Services(AWS) 클라우드에서 하이브리드 애플리케이션을 개발하고 있습니다. AWS Direct Link(DX)는 온프레미스 데이터 센터를 AWS에 연결하는 데 사용됩니다. AWS와 온프레미스 데이터 센터 간의 애플리케이션 연결은 매우 내구성이 있어야 합니다.

이러한 기준을 충족하려면 어떤 DX 설정을 사용해야 합니까?

A. VPN이 위에 있는 DX 연결을 구성합니다.

B. 여러 DX 위치에서 DX 연결을 구성합니다.

C. 가장 신뢰할 수 있는 DX 파트너를 사용하여 DX 연결을 구성합니다.

D. DX 연결 위에 여러 가상 인터페이스를 구성합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

온프레미스 데이터 센터 간의 애플리케이션 연결은 매우 내구성 문제 요점.

복원력이 뛰어나고 내결함성이 뛰어난 네트워크 연결은 잘 설계된 시스템의 핵심입니다. <br>
AWS는 물리적 위치 이중화를 위해 여러 데이터 센터에서 연결할 것을 권장합니다.

**AWS Direct Connect** <br>
클라우드 서비스는 AWS 리소스에 대한 최단 경로임. <br>
전송하는 동안 네트워크 트래픽은 AWS 글로벌 네트워크에 남아있으며 퍼블릭 인터넷에 닿지 않음. <br>
이렇게 하면 병목 현상이 발생하거나 대기 시간이 예기치 않게 증가할 가능성이 줄어듬.

새 연결을 생성할 때 AWS Direct Connect 제공 파트너가 제공하는 호스팅 연결을 선택하거나 AWS에서 전용 연결을 선택하고 전 세계 100개 이상의 AWS Direct Connect 위치에 배포할 수 있음.

AWS Direct Connect SiteLink를 사용하면 AWS Direct Connect 위치 간에 데이터를 전송하여 글로벌 네트워크의 데이터 센터와 사무실 사이에서 프라이빗 네트워크 연결을 생성 가능. <br>
하이브리드 네트워크 구축/기존 네트워크 확장/대규모 데이터 집합 관리

![7](/assets/img/study_AWS/[SAA]_ExamTopics_51~60/7.PNG)

A 탈락 -> STS VPN이 위에 있는 DX 연결은 무슨 말인지 모르겠음 서로 다른 연결인데 그래서 부적합.

B 정답 -> 여러 위치에 연결을 장애가 있어도 복원력/결합성이 좋아서 적합.

C 탈락 -> 가장 신뢰할 수 있다고 해도 보안 관련이지 내구성에 대한 것이 아니라 부적합.

D 탈락 -> 여러 가상 인터페이스를 구성하면 대역폭이 좋은 것이지 장애시 결국 한 곳에서 많이 연결한 것이라서 내구성이 좋지 않아 부적합.

</div>
</details>

<hr/>

## Prob. 59

금융 기관은 AWS를 사용하여 웹 애플리케이션을 호스팅합니다. 이 프로그램은 Amazon API Gateway 지역 API 엔드포인트를 사용하여 현재 주가를 검색합니다. 조직의 보안 직원이 API 쿼리의 급증을 감지했습니다. 보안 팀은 HTTP flood 공격으로 인해 애플리케이션이 작동하지 않을 수 있다고 우려하고 있습니다.
솔루션 설계자는 이러한 형태의 공격에 대한 방어책을 만들어야 합니다.

다음 중 운영 오버헤드가 가장 적은 이 기준을 충족하는 방법은 무엇입니까?

A. API Gateway Regional API 엔드포인트 앞에 최대 TTL이 24시간인 Amazon CloudFront 배포를 생성합니다.

B. 속도 기반 규칙을 사용하여 지역 AWS WAF 웹 ACL을 만듭니다. 웹 ACL을 API 게이트웨이 단계에 연결합니다.

C. Amazon CloudWatch 메트릭을 사용하여 카운트 메트릭을 모니터링하고 미리 정의된 속도에 도달하면 보안 팀에 알립니다.

D. API Gateway Regional API 끝점 앞에 Lambda@Edge를 사용하여 Amazon CloudFront 배포를 생성합니다. 미리 정의된 속도를 초과하는 IP 주소의 요청을 차단하는 AWS Lambda 함수를 만듭니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

운영 오버헤드가 가장 적은 기준 충족 문제 요점.

API 쿼리의 급증을 감지하여 HTTP flood(다수,대량) 공격으로 인해 애플리케이션이 작동하지 않을 수 있다고 우려. <br>
DDoS 보호에 대한 질문입니다. <br>
이것은 DDOS 보호의 한 형태입니다. 그래서 AWS WAF는 가장 적은 노력으로 최선을 다합니다.

**Amazon API Gateway** <br>
어떤 규모에서든 개발자가 API를 손쉽게 생성, 게시, 유지 관리, 모니터링 및 보안 유지할 수 있도록 하는 완전관리형 서비스. <br>
API는 애플리케이션이 백엔드 서비스의 데이터, 비즈니스 로직 또는 기능에 액세스할 수 있는 "정문" 역할.

API Gateway를 사용하면 실시간 양방향 통신 애플리케이션이 가능하도록 하는 RESTful API 및 WebSocket API를 작성. <br>
컨테이너식 서버리스 워크로드 및 웹 애플리케이션을 지원. <br>
트래픽 관리, CORS 지원, 권한 부여 및 액세스 제어, 제한, 모니터링 및 API 버전 관리 등 최대 수십만 개의 동시 API 호출.

API 게이트웨이는 기본적으로 요청을 조절합니다[링크](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html)https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html

우리는 AWS Shield 또는 WAF가 필요합니다 - [링크](https://aws.amazon.com/blogs/security/how-to-protect-dynamic-web-applications-against-ddos-attacks-by-using-amazon-cloudfront-and-amazon-route-53/)https://aws.amazon.com/blogs/security/how-to-protect-dynamic-web-applications-against-ddos-attacks-by-using-amazon-cloudfront-and-amazon-route-53/

**웹 액세스 제어 목록 (웹 ACL)** <br>
ACL은 개체나 개체 속성에 적용되어 있는 허가 목록. <br>
웹 ACL (웹 ACL) 을 사용하면 보호된 리소스가 응답하는 모든 HTTP (S) 웹 요청을 세부적으로 제어할 수 있습니다. 아마존 CloudFront, Amazon API Gateway, Application Load BalancerAWS AppSync, Amazon Cognito 및AWS App Runner 리소스를 보호 가능.
* 요청의 출처 IP 주소
* 요청의 출처 국가
* 요청의 일부로 포함된 문자열 일치 또는 정규 표현식(정규식) 일치
* 요청의 특정 부분의 크기
* 악성 SQL 코드 또는 스크립팅 감지

**Amazon CloudFront** <br>
AWS WAF(웹 애플리케이션 방화벽 보안 서비스), Lambda@Edge 등과 연동 가능.

**Lambda@Edge** <br>
CloudFront에서 `Origin에 도착 이전에 인증`. <br>
`커스텀` 에러 페이지. <br>
Cookie를 검사해 `다른 페이지`로 리다이렉팅.

A 탈락 -> 최대 TTL 24시간인 CF를 배포하여 DDOS를 막지 못하여 부적합.

B 정답 -> 속도 기반 규칙을 지역 AWS WAF 웹 ACL에 적용하여 DDOS에서 보호하는데 적합.

C 탈락 -> Amazon CloudWatch 메트릭으로 카운트를 모니터링하여 횟수를 체크해 보안팀에 알리는 것은 방어책이 아니라 부적합.

D 탈락 -> 이것으로 속도를 초과하면 IP주소 요청을 차단하는 함수를 만들 수 있는 모르겠으며 서로 다른 컨텐츠를 제공해주는 역할이라 부적합.

</div>
</details>

<hr/>

## Prob. 60

비즈니스에서 Amazon EC2 인스턴스의 보안 평가를 자동화하려고 합니다. 조직은 개발 프로세스가 보안 및 규정 준수 요구 사항을 준수하는지 확인하고 보여야 합니다.

이러한 기준이 충족되도록 솔루션 설계자는 어떤 조치를 취해야 합니까?

A. Amazon Macie를 사용하여 EC2 인스턴스를 자동으로 검색, 분류 및 보호할 수 있습니다.

B. Amazon GuardDuty를 사용하여 Amazon Simple Notification Service(Amazon SNS) 알림을 게시합니다.

C. Amazon CloudWatch와 함께 Amazon Inspector를 사용하여 Amazon Simple Notification Service(Amazon SNS) 알림 게시

D. Amazon EventBridge(Amazon CloudWatch Events)를 사용하여 AWS Trusted Advisor 확인의 상태 변화를 감지하고 대응합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

EC2 인스턴스의 보안 평가를 자동화 문제 요점.

**Amazon GuardDuty** <br>
목표는 로그 분석/위협 탐지입니다. <br>
-CloudTrail Logs: 비정상적인 API 호출, 무단 배포 <br>
-VPC 흐름 로그: 비정상적인 내부 트래픽, 비정상적인 IP 주소<br>
-DNS 로그: 손상된 EC2 인스턴스가 DNS 쿼리 내에서 인코딩된 데이터를 전송합니다.

암호화폐, 가상화폐((네트워크에서 안전한 거래를 위해 암호화된 디지털 화폐로 비트코인 등이 해당함)) CryptoCurrency 공격으로부터 보호할 수 있습니다(전용 "찾기"가 있음).<br>
그것은 기계 학습을 사용합니다.

**Amazon Macie** <br>
Macie는 PII(개인 식별 가능 정보)와 같은 중요한 데이터를 식별하고 이를 알려줍니다.<br>
S3에만 적용됩니다.

**Amazon Inspector** <br>
Inspector(검사자)는 EC2에만 해당됩니다.<br>
- EC2 인스턴스에 대한 자동 보안 평가를 제공합니다.<br>
- EC2 for Host에 에이전트를 설치해야 함(취약성 평가/모범 사례) 또는 에이전트를 설치하지 않고 EC2에 대해 NW 평가를 수행할 수 있음.

**AWS Trusted Advisor** <br> 
AWS Trusted Advisor는 AWS 모범 사례를 따르는 데 도움이 되는 권장 사항을 제공. <br>

A 탈락 -> 리소스와 기능 둘다 맞지 않고 중요한 데이터를 식별하는 것이라 부적합.

B 탈락 -> 로그를 분석하여 비정상적인 상황을 확인하는 것이라 부적합.

C 정답 -> Inspector는 EC2에 대한 자동 보안 평가를 제공하고 알림으로 보고받아 확인하여 적합.

D 탈락 -> 이벤트가 발생했을때 권장 사항 확인의 상태 변화를 감지하고 대응하는 것은 부적합.

</div>
</details>

<hr/>

* Ref
  - [ExamTopics](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate-saa-c02/view/6)