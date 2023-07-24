---
title: 새로운 아키텍처
description: 새로운 아키텍처로 이동하여 얻을 수 있는 이점에 대해 알아봅니다.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
source-git-commit: ddda796c9f32d22b1d679fc245eb11b92cd491cf
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# 새로운 아키텍처

[!DNL Adobe Commerce Intelligence] 제품 및 엔지니어링 팀은 지난 한 해 동안 가장 광범위하고 많이 요청된 개선 사항을 만드는 데 주력해 왔습니다. Adobe은 새로운 제품의 출시를 발표하게 되어 매우 기쁩니다 [!DNL Commerce Intelligence] 이러한 개선 사항을 실현하는 제품 아키텍처.

## 새로운 아키텍처의 이점

* SQL이 있는 계산된 열을 포함하여 Data Warehouse에 열 유형을 만듭니다.
* 새 열은 즉시 사용할 수 있습니다.
* 데이터 지연 시간이 획기적으로 개선되었습니다.

## 기술적 이점

주요 차이점은 위에 나열되어 있지만 주요 변경 사항은 업데이트 주기 동안 계산이 수행되는 방식입니다. 계산은 모든 업데이트 중에 더 이상 모든 열에서 실행되지 않습니다. 대신 시각적 Report Builder에서 온디맨드로 실행됩니다.

### 새 아키텍처로 이동

계정이 기본적으로 다르게 빌드되므로 Data Warehouse 또는 보고서를 새 아키텍처 계정으로 마이그레이션하는 자동 프로세스가 없습니다. 새 아키텍처로 이동하려면 기존 계정을 다시 구현해야 합니다.

### 새로운 아키텍처로의 전환 비용

추가 비용 없음! Adobe은 재구현을 시작할 수 있도록 이 새 계정을 만듭니다. 이 계정은 최소 1개월 동안 무료입니다. 이렇게 하면 재구현을 보다 쉽게 수행할 수 있도록 두 계정을 모두 열어 두고 팀에 서비스 공백이 생기지 않도록 할 수 있습니다.

### 새 아키텍처에서 계정을 재구현하는 데 필요한 시간

재구현 시간은 재구축할 내용에 따라 다릅니다. Adobe은 기존 계정에서 다음 단계를 수행하여 재구현과 관련된 사항을 파악하는 것을 권장합니다.

* 핵심 보고서/대시보드 세트를 식별합니다.
* 이러한 보고서를 작성하는 데 필요한 지표 및 차원을 식별합니다.
* 해당 지표 및 차원을 다시 만드는 데 필요한 열을 식별합니다.

이 작업이 완료되면 이러한 핵심 보고서를 다시 빌드하기 위해 새 아키텍처 Data Warehouse과 동기화해야 하는 데이터를 알 수 있습니다.

### 도움말 보기

다음 [!DNL Adobe Commerce Intelligence] [서비스 팀](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 은 추가 비용으로 재구현을 수행할 수 있습니다. 다음으로 연락 [Adobe 계정 팀](../../guide-overview.md#Submitting-a-Support-Ticket) 새 계정에서 만들기 전에 우선 순위를 지정할 대시보드/보고서 목록을 제공할 준비를 하십시오

### 기존 아키텍처 유지

이러한 기능이 중요하지 않은 경우 기존 계정을 고수할 수 있습니다. 기존 계정을 유지하는 데 추가 비용은 없습니다. Adobe은 변경 사항 없이 해당 계정을 계속 지원합니다.
