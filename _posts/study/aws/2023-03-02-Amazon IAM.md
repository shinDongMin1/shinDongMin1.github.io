---
layout: post
title: "[AWS] Amazon IAM"
subtitle: AWS
date: '2023-03-02 00:00:01 +0900'
category: study
tags: aws
image:
  path: /assets/img/study_AWS/aws_logo.png
---

# AWS IAM 이해
AWS에서 제공하는 **Amazon IAM**를 이해해보자.

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc}

<hr/>

## AWS IAM 개요

AWS의 IAM에 대한 설명을 보면
> **AWS Identity and Access Management(IAM)**은 `AWS 리소스에 대한 액세스`를 안전하게 **제어**할 수 있는 아마존 웹 서비스입니다. <br>
> `IAM을 사용하여` 리소스를 사용하도록 **인증(로그인)** 및 **권한 부여(권한 있음)**된 대상을 **제어**합니다.

**IAM**은 육하원칙 중 "왜"를 제외한 **누가 언제 어디서 무엇을 어떻게**를 `설정할 수 있고 제어`할 수 있는 서비스라고 할 수 있습니다.

<hr/>

## AWS IAM 기능

* **AWS 어카운트 관리** 및 **리소스/사용자/서비스의 권한 제어**
    + 서비스 사용을 위한 `인증 정보 부여`

* **사용자의 생성** 및 **관리** 및 **계정의 보안**
    + 사용자의 `패스워드 정책 관리`(일정 시간마다 패스워드 변경 등)

* **다른 계정과의 리소스 공유**
    + `Identify Federation`(Facebook 로그인, 구글 로그인 등)

* 계정에 **별명** 부여 가능 -> `로그인 주소 생성 가능`

* IAM은 **글로벌 서비스**(Region별 서비스가 아님)

<hr/>

## AWS IAM 구성

IAM은 `총 4가지의 요소`로 이루어져있다.

1. **사용자**
    * `실제 AWS를 사용`하는 **사람** 혹은 **어플리케이션**을 의미

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

<hr/>

다음은 **IAM의 구성도**입니다.

![IAM_Config](/assets/img/study_AWS/[AWS]_IAM_이해/IAM_config.png)

<hr/>

다음은 사용자가 S3를 사용하고 싶을 경우의 **IAM 권한 검증 절차**입니다.

![IAM_permission_verification](/assets/img/study_AWS/[AWS]_IAM_이해/IAM_permission_verification.png)

먼저 `사용자에게 => 그룹 => 역할` 순으로 `정책이 부여되어 있는지`를 파악하고 `권한을 검증`합니다.

<hr/>

다음은 **리소스(Lambda)**에 역할이 부여되어 있을 경우의 `권한 검증 절차`입니다.

![IAM_permission_verification_resource](/assets/img/study_AWS/[AWS]_IAM_이해/IAM_permission_verification_resource.png)

<hr/>

## 사용자의 종류(콘솔 로그인)

* **루트 사용자**
    + **결제 관리를 포함한 계정의 모든 권한**을 가지고 있음
    + `관리 목적 이외`에 **다른 용도로 사용하지 않는 것을 권장**
    + 탈취 되었을때 `복구가 매우 어려움` -> **MFA**를 설정하는 것을 권장
        - **MFA(Multi-factor authentication)** : `일회용 패스워드`를 생성하여 로그인`(OTP)`

* **IAM 사용자**
    + `IAM을 통해 생성해서 사용하는 사용자`
    + **한 사람** 혹은 **하나의 어플리케이션**을 의미
    + 설정 시 `콘솔 로그인 권한 부여 가능`
    + 설정 시 `AWS 서비스를 이용할 수 있음`
        - **Access Key ID** (유저 이름에 해당)
        - **Secret Access Key** (비밀번호에 해당)
    + **AdminAccess(모든 기능)**를 부여하더라도 `루트 사용자`로 별도의 `설정을 하지 않으면` **Billing(결제)**기능을 `사용할 수 없음`

<hr/>

## 자격 증명 보고서

IAM의 `현재 상황을 보여주는 보고서`라고 할 수 있습니다.

* **계정의 모든 사용자와 암호, 액세스 키, MFA 장치등의 증명 상태를 나열하는 보고서를 생성하고 다운로드 가능**

* **4시간에 한 번씩 생성 가능**하며, **생성한 후 최대 4시간 동안 저장**됨

*` AWS 콘솔, CLI, API`에서 생성 `요청 및 다운로드` 가능

포함되는 정보는 아래와 같습니다.

![IAM_report](/assets/img/study_AWS/[AWS]_IAM_이해/IAM_report.png)

<hr/>

## IAM 모범 사용 사례

* **루트 사용자는 사용하지 않기**

* **불필요한 사용자는 만들지 않기**

* 가능하면 **그룹**과 **정책**을 사용하기

* 최소한의 권한만을 허용하는 습관을 들이기(**최소 권한 원칙**, Principle of least privilege)

* **MFA**를 활성화하기

* **AccessKey 대신 역할**을 사용하기

* **IAM 자격 증명 보고서(Credential Report)** 활용하기

<hr/>

* Ref
  - [AWS IAM Userguide](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/introduction.html)
  - [Youtube](https://youtu.be/hb_4Tf6bAtY)