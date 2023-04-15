---
layout: post
title: "[AWS-SAA] Examtopics 171~180"
subtitle: AWS
date: '2023-03-27 00:00:01 +0900'
category: study
tags: aws aws-saa
image:
  path: /assets/img/study_AWS/saa-co2_logo.png
---

SAA Examtopics 171~180번 문제를 풀어보자.<br>

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## Prob. 171

기업은 여러 AWS 리전에서 ALB(Application Load Balancer)를 활용합니다. ALB는 일년 내내 변동하는 트래픽을 경험합니다. 회사의 네트워킹 담당자는 온프레미스 방화벽을 통해 ALB의 IP 주소를 허용하여 연결을 활성화해야 합니다.

어떤 솔루션이 가장 확장 가능하고 설정 변경이 가장 적게 필요합니까?

A. AWS Lambda 스크립트를 작성하여 서로 다른 영역에 있는 ALB의 IP 주소를 가져옵니다. 사내 방화벽의 규칙을 업데이트하여 ALB의 IP 주소를 허용합니다.

B. 서로 다른 영역의 모든 ALB를 NLB(네트워크 로드 밸런서)로 마이그레이션합니다. 온프레미스 방화벽의 규칙을 업데이트하여 모든 NLB의 Elastic IP 주소를 허용합니다.

C. AWS Global Accelerator를 시작합니다. 서로 다른 영역의 ALB를 액셀러레이터에 등록합니다. 가속기와 연결된 정적 IP 주소를 허용하도록 온프레미스 방화벽의 규칙을 업데이트합니다.

D. 한 리전에서 NLB(네트워크 로드 밸런서)를 시작합니다. 다른 리전에 있는 ALB의 개인 IP 주소를 NLB에 등록합니다. 사내 방화벽의 규칙을 업데이트하여 NLB에 연결된 Elastic IP 주소를 허용합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

가장 확장 가능하고 설정 변경이 가장 적게 필요 문제 요점.

여러 AWS 리전에서 각각 ALB(Application Load Balancer)를 활용.
온프레미스 방화벽을 통해 ALB의 IP 주소를 허용하여 연결을 활성화.

**AWS Global Accelerator**
AWS 글로벌 네트워크를 사용하여 애플리케이션의 가용성, 성능, 보안을 개선합니다.
퍼블릭 애플리케이션의 가용성, 성능 및 보안을 개선하는 데 유용한 네트워킹 서비스입니다. Global Accelerator는 애플리케이션 엔드포인트로의 고정 진입점 역할을 하는 두 개의 글로벌 정적 공용 IP(예: Application Load Balancer, Network Load Balancer, Amazon Elastic Compute Cloud(EC2) 인스턴스 및 탄력적 IP)를 제공.

* 글로벌 트래픽 관리자 - 트래픽 다이얼을 사용하여 트래픽을 가장 가까운 리전으로 라우팅하거나 리전 간에 빠른 장애 조치를 지원.
* API 가속화 - 엣지에서 TCP 종료를 활용하여 API 워크로드를 최대 60%까지 가속화.
* 글로벌 정적 IP - 엔터프라이즈 방화벽 및 IoT 사용 사례에서 허용 목록 생성을 간소화.
* 지연 시간이 짧은 게임 및 미디어 워크로드 - 맞춤형 라우팅을 사용하여 트래픽을 EC2 인스턴스 플릿으로 최종 라우팅.
리전 대신 엣지에서 DDoS 공격으로부터 애플리케이션을 보호.
DNS 캐시 종속성을 제거하여 결정형 라우팅이 가능.
GA는 방화벽에서 바인딩할 수 있는 정적 IP를 제공하고 GA는 ALB와 연결할 수 있습니다.

**ALB**
ALB는 L7단의 로드 밸런서를 지원합니다.
ALB는 HTTP/HTTPS 프로토콜의 헤더를 보고 적절한 패킷으로 전송합니다.
ALB는 IP주소 + 포트번호 + 패킷 내용을 보고 스위칭합니다.
ALB는 IP 주소가 변동되기 때문에 Client에서 Access 할 ELB의 DNS Name을 이용해야 합니다.
ALB는 L7단을 지원하기 때문에 SSL 적용이 가능합니다.

Target Group을 Instance ID로 지정 - ALB는 인스턴스에 대한 연결이 로드 밸런서에서 설정되므로 웹 서버 액세스 로그에는 로드 밸런서의 IP 주소가 캡처.
따라서 Client의 IP를 얻기 위해서는 X-Forwarded-For헤더를 사용.

**NLB**
NLB는 L4단의 로드 밸런서를 지원합니다.
NLB는 TCP/IP 프로토콜의 헤더를 보고 적절한 패킷으로 전송합니다.
NLB는 IP + 포트번호를 보고 스위칭합니다.
NLB는 할당한 Elastic IP를 Static IP로 사용이 가능하여 DNS Name과 IP주소 모두 사용이 가능합니다.
NLB는 SSL 적용이 인프라 단에서 불가능하여 애플리케이션에서 따로 적용해 주어야 합니다.

Target Group을 Instance ID로 지정 - Instance ID로 지정한 Target Group의 경우 DSR(Direct Server Return) 방식으로 동작하여 Response 시에 EC2 Instance는 직접 Client에게 패킷을 전달.
따라서 Server단에서 Client의 ip를 확인.
Target Group을 IP로 지정 - IP로 지정한 Target Group의 경우 기존 방식대로 Request/Response가 모두 LB를 경유하기 때문에 아웃바운드 통신이 되지 않는 Private 구간에서도 NLB를 이용하여 서비스가 가능.
따라서 Server단에서 LoadBalancer의 ip를 확인.

ALB는 기본적으로 IP가 변경되기 때문에 고정 IP를 가질 수 있는 NLB를 앞에 둠으로서 적용이 가능.
앞에 NLB를 두지만 CloudWatch와 Lambda함수를 이용하여 ALB의 IP가 변경되는 시점마다 변경된 IP에 맞게 설정해주는 작업이 추가적으로 필요.

ALB
Target Group을 Instance ID로 지정

A 탈락 -> 람다 스크립트로 ALB들의 IP주소를 가져오고 방화벽에 업데이트 설정을 하여 부적합.

B 탈락 -> ALB를 모두 NLB로 변경해야해서 부적합.

C 정답 -> GA를 사용해서 ALB들을 모아두고 방화벽에서 허용하여 적합.

D 탈락 -> 고정IP를 갖는 NLB를 앞에 둠으로써 허용하지만 ALB의 IP는 계속 변경되기에 CloudWatch와 Lambda함수를 이용하여 추가 작업하여 부적합.

</div>
</details>

<hr/>

## Prob. 172

매달 기업은 판매 보고서를 작성해야 합니다. 매월 1일에 보고 절차가 20개의 Amazon EC2 인스턴스를 시작합니다. 절차는 7일 동안 지속되며 일시 중지할 수 없습니다. 회사는 비용을 낮게 유지하기를 원합니다.

기업은 어떤 가격 전략을 추구해야 합니까?

A. Reserved Instances

B. Spot Block Instances

C. On-Demand Instances

D. Scheduled Reserved Instances

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

비용을 낮게 유지하기를 원함 문제 요점.

매달 기업은 판매 보고서를 작성.
매월 1일에 보고 절차가 20개의 Amazon EC2 인스턴스를 시작.
7일 동안 지속되며 일시 중지할 수 없음.

예약된 예약 인스턴스를 사용하면 매일, 매주 또는 반복되도록 예약된 용량을 예약할 수 있습니다. 1년 기간 동안 지정된 시작 시간 및 기간과 함께 매월. 완료 후 구매 지정, 인스턴스는 귀하가 구매한 기간 동안 시작할 수 있습니다.

지금은 Scheduled Reserved Instances를 구입할 수 없습니다. AWS에는 Scheduled Reserved Instances에 사용할 수 있는 용량이 없거나 향후 사용할 계획이 없습니다. 용량을 예약하려면 온디맨드 용량 예약을 대신 사용하십시오. 할인된 요금의 경우 할인 혜택을 이용하십시오.

A 탈락 -> Reserved Instance는 일주일 정도의 짧은 기간에는 맞지 않는 스토리지 클래스로 계획에 맞는 용량을 예약하여 할인된 가격으로 장기간 사용하여 부적합.

B 탈락 -> Spot Block Instances는 기간이 정의된 스팟 인스턴스로 40퍼 활인인데 더이상 제공되지 않고 기간이 없는 스팟인 경우 중단이 일어날 수 있어 부적합.

C 정답 -> 가장 비용면에서는 낮지 않지만 조건을 만족하기에 적합.

D 탈락 -> Scheduled Reserved Instances는 매일/매주 단위로 예약하는 클래스인데 더이상 제공되지 않아 부적합.

</div>
</details>

<hr/>

## Prob. 173

기업은 모든 모바일 장치에서 사용할 수 있도록 비디오 자료를 업로드하고 트랜스코딩하는 온라인 서비스를 제공합니다. 애플리케이션 설계는 Amazon Elastic File System(Amazon EFS) 표준을 사용하여 수많은 Amazon EC2 Linux 인스턴스에서 처리할 수 있도록 영화를 수집하고 저장합니다. 서비스의 인기가 높아짐에 따라 스토리지 비용이 엄청나게 비쌌습니다.

가장 저렴한 스토리지 옵션은 무엇입니까?

A. AWS Storage Gateway for files를 사용하여 비디오 콘텐츠를 저장하고 처리할 수 있습니다.

B. AWS Storage Gateway for volumes를 사용하여 비디오 콘텐츠를 저장하고 처리합니다.

C. 비디오 콘텐츠를 저장하려면 Amazon EFS(Amazon Elastic File System)를 사용합니다. 처리가 완료되면 Amazon Elastic Block Store(Amazon EBS)로 파일을 전송합니다.

D. 비디오 콘텐츠를 저장하기 위해 Amazon S3를 사용합니다. 처리할 파일을 서버에 연결된 Amazon EBS(Amazon Elastic Block Store) 볼륨으로 임시 이동합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D (or A) // D
Discussion에서 엄청 갈리는데 마지막 줄이 경험상 가장 중요한 판단 요인이기 때문에, 답을 D로 생각하도록 함.

해설 : 

가장 저렴한 스토리지 옵션 문제 요점.

Amazon EFS 표준을 사용하여 수많은 Amazon EC2 Linux 인스턴스에서 처리할 수 있도록 영화를 수집하고 저장.

트랜스코딩은 이미 압축된 파일(일반적으로 오디오 또는 비디오)을 다른 파일 형식으로 변환하는 프로세스

A, B 탈락 -> Storage Gateway는 하이브리드 환경 서비스로 클라우드에 있는 스토리지에 백업을 하고 분석 용도로 사용하여 S3 분석용으로 NFS(Linux, EFS)/SMB(Windows, FSx)마운트 포인트로 전송받는 파일 게이트웨이와 EBS 백업용으로 Stored(모든 데이터를 로컬에 저장)/Cached(자주 사용되는 데이터만 로컬에 저장)/VTL인 iSCSI 프로토콜로 전달받는 볼륨/테이프 게이트웨이는 비용적으로 부적합.

C 탈락 -> EFS로 컨텐츠를 저장하지만 처리가 완료되면 EBS로 저장할 필요가 없어 부적합.

D 정답 -> S3 스토리지에 저장하고 처리할 파일을 임시로 EBS에 이동시켜 작업하여 적합.

</div>
</details>

<hr/>

## Prob. 174

기업은 매일 단일 공장에 있는 많은 기계에서 10테라바이트의 계측 데이터를 얻습니다. 데이터는 공장 온프레미스 데이터 센터 내부의 SAN(Storage Area Network)에서 JSON 파일로 저장됩니다. 조직은 이 데이터를 Amazon S3에 업로드하여 중요한 거의 실시간 분석을 수행하는 다른 여러 시스템에서 액세스할 수 있도록 하려고 합니다. 데이터는 민감한 것으로 간주되기 때문에 안전한 전송이 중요합니다.

가장 안전한 데이터 전송 방법을 제공하는 옵션은 무엇입니까?

A. AWS DataSync over public internet

B. AWS DataSync over AWS Direct Connect

C. AWS Database Migration Service (AWS DMS) over public internet

D. AWS Database Migration Service (AWS DMS) over AWS Direct Connect

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : B

해설 : 

가장 안전한 데이터 전송 문제 요점.

1) 이 회사는 이 데이터를 Amazon S3로 전송하여 중요한 실시간에 가까운 분석을 제공하는 여러 추가 시스템을 통해 액세스할 수 있기를 원합니다. -> DataSync는 S3(모든 스토리지 클래스)와 동기화할 수 있습니다.

2) 매일 10TB의 계측 데이터 -> DataSync를 사용하여 시간별, 일별, 주별로 복제 작업을 예약할 수 있습니다.

3) 이것은 데이터베이스 마이그레이션 시나리오가 아닌 이동 데이터 시나리오입니다.

SAN(Storage Area Network) - 여러 서버 또는 컴퓨터에서 액세스할 수 있는 스토리지 디바이스 네트워크로, 스토리지 공간의 공유 풀을 제공합니다. 네트워크의 각 컴퓨터는 컴퓨터에 직접 연결된 로컬 디스크처럼 SAN 스토리지에 액세스.

네트워크 연결 스토리지(NAS) - 직원들이 네트워크를 통해 효과적으로 협업할 수 있도록 데이터를 지속적으로 사용할 수 있게 하는 파일 전용 스토리지 디바이스입니다. 모든 컴퓨터 네트워크에는 서버에 요청을 전송하는 상호 연결된 서버 시스템과 클라이언트 시스템이 있음.

SAN과 NAS 비교
SAN과 NAS(네트워크 연결 스토리지)는 네트워크로 연결된 공유 스토리지 솔루션의 두 가지 유형입니다. SAN은 여러 기기로 이루어진 로컬 네트워크인 반면, NAS는 LAN(Local Area Network)에 연결되는 단일 스토리지 디바이스입니다.

A 탈락 -> 인터넷을 사용하여 보안적으로 부적합.

B 정답 -> 비용도 싸고 직접 연결하여 보안적으로 적합.

C, D 탈락 -> 그냥 데이터를 마이그레이션하는 것이지 DMS로 DB를 옮기는게 아니라 부적합.

</div>
</details>

<hr/>

## Prob. 175

데이터 과학 팀은 야간에 로그를 분석하기 위해 스토리지가 필요합니다. 로그의 양과 수는 불명확하나, 24시간 동안 보관됩니다.

어떤 접근 방식이 가장 비용 효율적입니까?

A. Amazon S3 Glacier

B. Amazon S3 Standard

C. Amazon S3 Intelligent-Tiering

D. Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA)

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

야간에 로그를 분석하기 위해 스토리지가.
24시간 동안 보관.

C는 최소 지불 단위가 30일이다.<br>
즉, 24시간 동안만 접근되는 데이터에는 맞지 않다.<br>

A 탈락 -> Glacier는 오래 접근이 안될 데이터를 대상으로 부적합.

B 정답 -> 시간단위로 계산하기 때문에 하루 사용으로 적합.

C 탈락 -> 비용적으로 가장 적합하나 30일 기준으로 지불하여 부적합.

D 탈락 -> 가용성인 복제를 포기하여 싸서 사용 빈도가 낮고 중요도가 떨어지는 데이터인 트래픽 로그에 적합하지만 이것은 백업용으로 오래 사용하는 듯하거나 로그 분석에 당장 사용해야하니 부적합.

</div>
</details>

<hr/>

## Prob. 176

개발 팀이 AWS에서 신제품을 출시하고 있으며 출시의 일환으로 AWS Lambda를 사용하고 있습니다. Lambda 함수 중 하나를 위해 팀은 512MB의 RAM을 할당합니다. 이 메모리 할당으로 함수는 2분 안에 완료됩니다. 함수는 월간 수백만 번 실행되고 개발 팀은 비용에 대해 걱정하고 있습니다. 팀은 다양한 Lambda 메모리 할당이 함수 비용에 미치는 영향을 확인하기 위해 실험을 수행합니다.

어떤 조치로 제품의 Lambda 비용이 감소합니까? (2개를 선택하세요.)

A. 이 변경으로 인해 각 기능의 실행 시간이 1분 미만이 되면 람다 함수에 대한 메모리 할당을 1,024MB로 늘립니다.

B. 이 변경으로 인해 각 기능의 실행 시간이 90초 미만이 되면 람다 함수에 대한 메모리 할당을 1,024MB로 늘립니다.

C. 이 변경으로 인해 각 기능의 실행 시간이 4분 미만이면 람다 함수에 대한 메모리 할당을 256MB로 줄입니다.

D. 이 변경으로 인해 각 기능의 실행 시간이 1분 미만이 되면 람다 함수에 대한 메모리 할당을 2,048MB로 늘립니다.

E. 이 변경으로 인해 각 기능의 실행 시간이 5분 미만이면 람다 함수에 대한 메모리 할당을 256MB로 줄입니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A, C

해설 : 

Lambda 비용이 감소 문제 요점.

Lambda 함수 중 하나를 위해 팀은 512MB의 RAM을 할당.
이 메모리 할당으로 함수는 2분 안에 완료.
함수는 월간 수백만 번 실행되고 개발 팀은 비용에 대해 걱정.
다양한 Lambda 메모리 할당이 함수 비용에 미치는 영향을 확인.

A를 선택하면 사용된 메모리가 두 배가 되지만 완료 시간은 2분이 아니라 2분 미만입니다. 결과적으로 B, D보다 효율적이다.<br>
답 C가 답 E보다 더 낫고 효율적이다.

A 정답 -> 메모리를 2배로 늘렸으며 그 만큼 속도도 1/2배가 되어 적합.

B 탈락 -> 메모리를 2배로 늘렸지만 속도는 30초 밖에 안되서 부적합.

C 정답 -> 메모리를 1/2배로 줄였으며 그만큼 속도도 2배가 되어 적합.

D 탈락 -> 메모리를 4배로 늘렸지만 속도는 1/2배 밖에 안되서 부적합.

E 탈락 -> 메모리를 1/2배로 줄였지만 속도도 2배이상이 되어 부적합.

</div>
</details>

<hr/>

## Prob. 177

기업은 중앙 집중식 Amazon Web Services 계정을 사용하여 많은 Amazon S3 버킷에 로그 데이터를 저장하고 있습니다. S3 버킷에 데이터를 업로드하기 전에 솔루션 설계자는 데이터가 암호화되어 있는지 확인해야 합니다. 또한 데이터는 전송 중에 암호화되어야 합니다.

어떤 솔루션이 이러한 기준을 충족합니까?

A. 클라이언트 측 암호화를 사용하여 S3 버킷에 업로드 중인 데이터를 암호화합니다.

B. 서버측 암호화를 사용하여 S3 버킷에 업로드 중인 데이터를 암호화합니다.

C. S3 업로드용 S3 관리 암호화 키(SSE-S3)를 사용하여 서버 측 암호화를 사용해야 하는 버킷 정책을 생성합니다.

D. 기본 AWS KMS(키 관리 서비스) 키를 사용하여 S3 버킷을 암호화하려면 보안 옵션을 실행하십시오.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

보안 기준 문제 요점.

많은 Amazon S3 버킷에 로그 데이터를 저장.
데이터가 암호화되어 있는지 확인.
데이터는 전송 중에 암호화.

전송 중 보호 = SSL(보안 소켓 계층)/TLS(전송 계층 보안) 또는 클라이언트 측 암호화 데이터를 보호.
AWS Docs에서는 "데이터 보호란 전송 중(Amazon S3로 오가는 동안) 및 유휴 상태(Amazon S3 데이터 센터의 디스크에 저장되는 동안) 데이터를 보호하는 것을 의미합니다. SSL/TLS(Secure Socket Layer/Transport Layer Security) 또는 클라이언트 측 암호화를 사용하여 전송 중인 데이터를 보호할 수 있습니다."

서버측 암호화 – 개체를 데이터 센터의 디스크에 저장하기 전에 암호화한 다음 개체를 다운로드할 때 암호를 해독하도록 Amazon S3에 요청합니다.

클라이언트 측 암호화 – 클라이언트 측 데이터를 암호화하고 암호화된 데이터를 Amazon S3에 업로드합니다. 이 경우 암호화 프로세스, 암호화 키 및 관련 도구를 관리합니다.

A 정답 -> 클라이언트측 암호화는 전송 전에 암호화해서 보내고 저장하여 적합.

B 탈락 -> 서버측 암호화는 전송 중에는 암호화를 안하여 S3에만 적용 부적합.

C 탈락 -> 암호화 키에 대한 SSE-S3로 지정해도 결국 서버측 암호화로 부적합.

D 탈락 -> KMS서비스로 키를 관리하며 S3만 암호화하여 부적합.

</div>
</details>

<hr/>

## Prob. 178

비즈니스에서는 Microsoft Windows 기반 애플리케이션을 AWS로 마이그레이션해야 합니다. 이 프로그램은 수많은 Amazon EC2 Windows 시스템에 연결된 공유 Windows 파일 시스템을 활용합니다.

솔루션 설계자는 이를 달성하기 위해 어떤 조치를 취해야 합니까?

A. Amazon Elastic File System(Amazon EFS)을 사용하여 볼륨을 구성합니다. 각 윈도우즈 인스턴스에 EFS 볼륨을 마운트합니다.

B. 볼륨 게이트웨이 모드에서 AWS 스토리지 게이트웨이를 구성합니다. 각 윈도우즈 인스턴스에 볼륨을 마운트합니다.

C. 윈도우즈 파일 서버용 Amazon FSx를 구성합니다. Amazon FSx 볼륨을 각 윈도우즈 인스턴스에 마운트합니다.

D. 필요한 크기로 Amazon Elastic Block Store(Amazon EBS) 볼륨을 구성합니다. 각 EC2 인스턴스를 볼륨에 연결합니다. 볼륨 내의 파일 시스템을 각 윈도우즈 인스턴스에 마운트합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : C

해설 : 

Microsoft Windows 기반 애플리케이션을 AWS로 마이그레이션.
수많은 Amazon EC2 Windows 시스템에 연결된 공유 Windows 파일 시스템을 활용.

Windows = FSx

A 탈락 -> EFS는 NFS프로토콜로 리눅스에 대한 파일 시스템으로 파일(S3)을 저장하여 부적합.

B 탈락 -> 볼륨 게이트웨이는 Stored/Cached가 있는데 EBS에 증분식으로 백업되는 용도로 사용하여 부적합.

C 정답 -> FSx는 SMB으로 윈도우에 대한 파일 시스템으로 파일(S3)을 저장하여 적합.

D 탈락 -> EC2에 윈도우 파일 시스템으로 EBS 볼륨에 저장하지만 공유 파일 시스템적으로 동시성이 EBS는 최대 한계가 있어 부적합.

</div>
</details>

<hr/>

## Prob. 179

IAM 그룹은 다음 IAM 정책과 연결됩니다. 이것이 그 단체의 유일한 방침입니다.

![prob_179](/assets/img/study_AWS/[SAA]_ExamTopics_171~180/prob_179.png)

그룹 구성원에 대한 정책의 유효한 IAM 권한은 무엇입니까?

A. 그룹 구성원은 us-east-1 지역 내에서 Amazon EC2 작업을 수행할 수 있습니다. 허용 권한 이후의 문장은 적용되지 않습니다.

B. 그룹 구성원은 MFA(다중 요인 인증)로 로그인하지 않는 한 us-east-1 영역에서 Amazon EC2 사용 권한이 거부됩니다.

C. 그룹 구성원은 MFA(다중 요인 인증)로 로그인한 경우 모든 영역에 대한 ec2 인스턴스에 대한 중지/종료 권한이 허용됩니다.
그룹 구성원에게는 다른 모든 Amazon EC2 작업이 허용됩니다.

D. 그룹 구성원은 ec2:인스턴스 및 ec2 중지:종료 MFA(다중 요인 인증)로 로그인한 경우에만 us-east-1 영역에 대한 인스턴스 권한. 그룹 구성원은 us-east-1 지역 내에서 다른 모든 Amazon EC2 작업이 허용됩니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : D

해설 : 

유효한 IAM 권한 문제 요점.

추가) 디폴트로 IAM 사용자는 EC2를 생성하거나 변경할 수 없고, EC2 API를 사용한 태스크를 수행할 수 없다.<br>
이를 허용하기 위해서는 IAM 정책을 만들어서 IAM 사용자에게 권한 부여를 해주어야 한다.

원문)
https://docs.aws.amazon.com/AWSEC2/latest/APIReference/ec2-api-permissions.html<br>
기본적으로 AWS IAM(Identity and Access Management) 사용자에게는 Amazon EC2 리소스를 만들거나 수정하거나 Amazon EC2 API를 사용하여 작업을 수행할 수 있는 권한이 없습니다. IAM 사용자가 리소스를 만들거나 수정하고 작업을 수행할 수 있도록 하려면 IAM 사용자에게 사용할 특정 리소스 및 API 작업에 대한 사용 권한을 부여하는 IAM 정책을 만든 다음 해당 사용 권한이 필요한 IAM 사용자 또는 그룹에 정책을 연결해야 합니다.

정책의 첫 번째 부분은 us-east-1 지역에서 EC2의 모든 작업을 허용.
두 번째 부분은 MFA가 없는 사용자에 대해 모든 지역에서 중지 및 종료 거부.

A 탈락 -> 첫 번째 정책만 적용되고 나머지는 안된다는 것 같아서 부적합.

B 탈락 -> EC2 사용 권한은 지역으로 허용되나 MFA 로그인이 아니라 중지/종료 작업은 거부되어 부적합.

C 탈락 -> 두 번째 정책만 만족하고 첫 번째 정책은 만족하지 않아 부적합.

D 정답 -> 모든 정책을 만족하여 적합.

</div>
</details>

<hr/>

## Prob. 180

한 비즈니스에서 아카이브된 뉴스 장면에서 생성된 비디오 아카이브를 AWS에 저장할 수 있는 솔루션을 찾고 있습니다. 기업은 비용을 절감해야 하며 이러한 데이터를 거의 복구할 필요가 없습니다. 파일이 필요한 경우 5분 이내에 제공해야 합니다.

어떤 접근 방식이 가장 비용 효율적입니까?

A. 비디오 아카이브를 Amazon S3 Glacier에 저장하고 Expedited 검색을 사용하십시오.

B. 비디오 아카이브를 Amazon S3 Glacier에 저장하고 Standard 검색어를 사용하십시오.

C. 비디오 아카이브를 Amazon S3 Standard-Infrequent Access(S3 Standard-IA)에 저장합니다.

D. 비디오 아카이브를 Amazon S3 One Zone-Infrequent Access(S3 One Zone-IA)에 저장합니다.

<br>
<hr/>
<br>

<details>
<summary>정답 및 해설 보기</summary>
<div markdown="1">
<br>
Answer : A

해설 : 

가장 비용 효율적 문제 요점.

아카이브된 뉴스 장면에서 생성된 비디오 아카이브를 AWS에 저장.
비용을 절감해야 하며 이러한 데이터를 거의 복구할 필요가 없음.
필요한 경우 5분 이내에 제공.

Expedited(촉진) 검색 - 아카이브 하위 집합에 대한 긴급 요청이 필요할 때 신속하게 데이터에 액세스할 수 있습니다. 최대 규모(250MB 이상)를 제외한 모든 아카이브의 경우 Expedited 검색을 사용하여 액세스하는 데이터를 일반적으로 1-5분 이내에 사용할 수 있습니다. Provisioned Capacity는 필요할 때 신속한 검색을 위한 검색 용량을 제공합니다. 자세한 내용은 프로비저닝된 용량을 참조하십시오.

Standard 검색 — 표준 검색을 사용하면 몇 시간 내에 모든 아카이브에 액세스할 수 있습니다. 표준 검색은 일반적으로 3-5시간 내에 완료됩니다. 이 옵션은 검색 옵션을 지정하지 않은 검색 요청의 기본 옵션입니다.

S3 스토리지 클래스에는 알 수 없거나 액세스 패턴이 변경되는 데이터에 대한 자동 비용 절감을 위한 S3 Intelligent-Tiering. 
자주 액세스하는 데이터를 위한 S3 Standard.
자주 액세스하지 않는 데이터를 위한 S3 Standard-Infrequent Access(S3 Standard-IA) 및 S3 One Zone-Infrequent Access(S3 One Zone-IA).
즉각적인 액세스가 필요한 아카이브 데이터를 위한 S3 Glacier Instant Retrieval.
즉각적인 액세스가 필요하지 않고 거의 액세스하지 않는 장기 데이터를 위한 S3 Glacier Flexible Retrieval(이전 S3 Glacier).
클라우드에서 가장 저렴한 스토리지로 몇 시간 만에 검색 가능한 장기간 아카이브 및 디지털 보존을 위한 Amazon S3 Glacier Deep Archive(S3 Glacier Deep Archive)가 포함.
기존 AWS 리전으로 해결할 수 없는 데이터 레지던시 요구 사항이 있다면 S3 Outposts 스토리지 클래스를 사용하여 S3 데이터를 온프레미스에 저장.

A 정답 -> S3 Glacier의 촉진 검색으로 하위 대상으로 1~5분 이내에 적합.

B 탈락 -> S3 Glacier의 표준 검색으로 전체를 대상으로 3~5시간 걸림 부적합.

C, D 탈락 -> S3 Standard/One Zone-Infrequent Access으로 자주 액세스하지 않는 데이터를 저장하기에 부적합.

</div>
</details>

<hr/>

* Ref
  - [ExamTopics](https://www.examtopics.com/exams/amazon/aws-certified-solutions-architect-associate-saa-c02/view/18)